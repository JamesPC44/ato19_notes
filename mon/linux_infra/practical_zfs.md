# ATO19: Practical ZFS

*Jim Salter*

https://allthingsopen.org/talk/practical-zfs/

* Mercenary sysadmin problems
    * Must work with many different machines
    * Very important not to lose data
    * ZFS snapshots are compelling
        * Ransomware is no longer a concern
* Best practices
    * `ashift=12` or higher
        * Minimum block size to be stored on the hardware
        * This is a power of 2 ($2^{12} = 4\text{k}$, i.e. don't write smaller than a $K block)
    * `compression=lz4`
    * `atime=off`
        * Access time is not usually very useful and creates lots of needless disk writes (creates a write for every single read)
        * You might want `relatime=on` which updates atime only from time to time. This is the default on newer ZFSs. You probably still want to turn atime off though.
    * don't store data in the pool root
        * discussed later
    * more vdevs is prefered to wider vdevs
        * more narrow vdevs are more performant, rather than one vdev with all your disks
* `ashift`: why and how
    * Default relies on drives not to lie
    * Windows XP wouldn't work with disks that had larger than 512B blocks, so many vendors fake this even though most drives are 4K or larger
    * Set on a per-vdev basis, rather than a per-pool basis
        * Must be updated when new disks added to the pool
    * Very little penalty set if it's too high
        * At worst, wastes some space
    * Extremely major penalty if it's too low
        * Each block (at the ZFS level) gets batched out to a separate write, even if they are all going to reside in the same block on disk
* Compression: why & when
    * lz4 is faster than any drive, even on underpowered CPUs
        * This was faster in a production system with an AMD A4 APU paired with two relatively fast SSDs
    * ZFS automatically recognizes uncompressible data
    * gzip can also be used, but is much less performant, so use with caution
        * This is probably only a good idea if you know all or most of your data will be very compressible
* `xattr=sa`
    * Linux only
    * Store extended attributes inside of the inode, rather than a separate small file
    * Less compatible (pool can still be exported and imported, but the attributes won't be accessible from pools on other OSes)
    * Considerable performance improvement
* Don't put data in the pool root
    * You can replicate from the pool root, but not to the pool root (i.e. you can't target a pool root with `zfs send`).
    * `zfs set mountpoint` and `zfs set canmount=no` can be used to replicate the effect that storing in pool root would give you, if you really need that.
    * Don't be complicated if you can avoid it.
* More vdevs is better than wider zdevs
    * d = 1 disk's IOPs
    * n = # of disks
    * v = # of vdevs
    * RAIDz: IOPS $\neq n \cdot d$, IOPS $\approx v\cdot d$
    * mirrors: READ $\approx n\cdot d$, WRITE = $\approx v \cdot d$
    * A RAIDz vdev will trend towards the IOPS of the slowest disk
    * Pools of mirrors perform much better than anything else.
    * Almost every workload is IOPS constrained
* Stay covered
    * Always have parity if possible (i.e. if you have a disk failure, fix it)
    * If more corruption or disk failures occur while recovering, you can't fix it
* Stay scrubbed
    * Scrubbing is important
    * ZOL creates a cronjob that does this automatically
* Consider mirror vdevs
    * IOPS: READ $\approx n \cdot d$, WRITE $\approx \frac{n}{2} \cdot d$
    * Must faster resliver, scrub, and upgrade
    * Many people feel fear that pools of mirrors are not resiliant to failures
        * While one disk will get you uncovered, your odds of survival are good, and you are only ever uncovered on one disk worth of data
    * Can upgrade pool storage without upgrading every single disk (just the disks in a given mirror)
    * Mirrors can be rebalanced in place (unlike RAIDz)
        * scrub first
        * break all vdevs with `zpool detach`
        * new pool of single disks
        * replicate from old to new
        * destroy the old pool
        * `zpool attach` disks to new
* recordsize tuning
    * recordsize is the maximum amount of data that ZFS writes in a single operation. Where possible, ZFS wants to write recordsize at a time.
    * Can be set on a per-dataset basis, default=128K
    * Default value is decent all-around, but not optimal for anything either
    * 64K is good for QEMU stuff, since it matches the block size of QCOW
    * 1M is the largest possible without patching ZFS
    * Too large of a recordsize increases throughput amplification and latency
    * Too small reduces compression efficiency^[compession is done on a per-record basis], increases fragmentation, and increses IOPS amplification
    * If you have lots of big files, you want 1M or over, including torrents
    * Match `cluster_size` for `.qcow2` VM images (you might want to tune that also)
    * Match page size for DB binaries
* `/etc/modprobe.d/zfs.conf` (ZFS tunables)
    * `options zfs zfs_txg_timeout=5` -- how frequently you flush TXGs^[transaction groups] to disk -- i.e. how long write-cached data is allowed to sit in memory before being written out to disk. TXG flush takes highest priority, so you want to avoid building up too much of a backlog. Especially on flash pools, you might want to bump up to ~ 30.
    * `options zfs zfs_prefetch_disable=1` -- read prefetch, default off, useful for spinning rust. On SSDs, you probably don't want this.
    * `options zfs zfs_vdev_async_write_max_active=10` -- how deep the IO queue goes, tunable for sync, async, read, and write. If it's too high you'll add latency, but if you set it too low for your IOPS, it can throttle your performance.
        * There also variants for `sync` and `read` variations.
    * `options zfs zfs_vdev_scrub_max_active=2` -- how deep the IO queue goes for scrub operations, basically helps scrubs go faster. However, this will reduce the performance of non-scrub performance.
* replication, not rsync
    * Replications are drastically faster
    * `rsync` must at least stat, and possibly read every file/block on both sides
    * Replication uses differential transfers, only has to transfer blocks, $O(1)$ on the remote machine
    * The downside is that you have to care about snapshots, do the replication manuall, etc.
    * syncoid makes all the ZFS replication things nice
