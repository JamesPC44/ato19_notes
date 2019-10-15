# ATO19: Using eBPF for Performance Analysis

*Peter Zaitsev*

https://allthingsopen.org/talk/2-for-1-the-future-of-linux-distros-in-the-cloud/

## eBPF Programs
- Kernel can load eBPF bytecode program.
- Programs verified before load.
- Clang has a backend for eBPF.
- Compilation of bytecode is kernel-dependent.
- Few need to write eBPF directly.

## Support in Linux Distros
- Not all distros have packages.
- Development work is quick-paced.
    - Many have outdated packages.
- Consider getting the newest/latest BPF packages.

## Tools
- biosnap
- ext4dist
- ext4slower - trace slow IO
- cachestat
- runqlat - cpu run queue latency
- execsnoop - trace program statistics
- tcpconnect - trace TCP connections
- tcpconnect - trace TCP connections
- tcpretrans - TCP retransmit details
- gethostlatency - DNS lookup latency
- Long list of tools in the BCC collection...

## Syscall probes
- No data. Presenter moved quickly.

## eBPF Bible
- http://www.brendangregg.com/ebpf.html
