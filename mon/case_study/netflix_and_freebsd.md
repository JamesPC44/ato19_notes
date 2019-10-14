# ATO19: Netflix and FreeBSD: Using Open Source to Deliver Streaming Video


*Jonathan Looney* -- the guy that writes the content cache OS.

https://allthingsopen.org/talk/netflix-and-freebsd-using-open-source-to-deliver-streaming-video/

* OpenConnect
	* Netflix's CDN
	* Global, efficient, and purpose built
	* > 100 Tb/s at peak
* Two compute environments
	* Cloud compute (not today)
		* User auth, profiles, etc.
		* Descriptions, listings, etc.
		* Analytics
	* CDN (this talk)
		* Static configuration code
		* Static images / preview trailers, etc. ("box art")
		* Video, audio, subtitles
		* Statically pre-generated previews for scrubbing
* OpenConnect Appliance
	* 40Gb/s storage appliance with 248TB storage in 2U.
	* There is also a 1U variant that runs at 100Gb/s and is flash based.
	* Almost entirely commodity hardware.
	* Runs almost entirely open source software
		* FreeBSD OS
		* NGinX
		* Python, Perl, Go
	* Integration between clients and CDN allows gathering of detailed
	  metrics on CDN performance
* OCA Workload
	* Disks -> CPU (encryption) -> Network
	* Achieve 90Gb/s with TLS on 55% CPU usage on a Xeon 6122 (16 core @
	  2.6GHz)
* OCA Operating System
	* A lightly customized variant of FreeBSD
	* FreeBSD release cycle
		* Development branch (head)
		* Periodically spike off stable / release branches
		* Occasional back-porting from head
	* OCA tracks FreeBSD head and tracks it's own release branches.
	    * 4-15 weeks turnaround from commits into FreeBSD head to deployment.
	    * ~ 5 weeks of development + 5 weeks testing & deployment per release
	    * Incremental / phased release to subsets of the OCA boxes at a time.
    * Features added
        * NUMA enhancements
            * dual socket 200Gb/s prototype in the works
        * Asynchronous sendfile
            * Allows all work to transmit file data to a TCP connection in kernelspace, without userland blocking
            * Avoids kernel to userspace and back to kernel copies
        * Kernel TLS
            * Allows the kernel to perform needed encryption without having to copy to userspace
        * Pbuf allocation enhancements
        * Unmapped mbufs
        * I/O scheduling
        * TCP algorithms
        * TCP logging infrastructure
    * Why track head?
        * Downstream users of OSS can be stuck in either vicious or virtuous cycles
        * In a vicious cycle, you merge infrequntly, resulting in many conflicts in regressions, slowing velocity, and leading to less frequent merges.
        * In a virtuous cycle, you merge frequently, but generall have few and easy to resolve conflicts, leading to faster velocity.
    * Why keep local diffs?
        * Information under NDA.
        * Feature still under development.
        * Features which aren't generalized.
* Common objections to running development code
    * It isn't stable (it usually is)
    * Why should you pay to find the bugs other will find while testing head? (often, others wouldn't find them)
    * Aren't there more security bugs? (rarely)
    * No on runs development branches. (other organizations do this too)
    * Pay monthly cost to do merges (yes, but you would have to merge eventually, and it would be more difficult)
* Questions?
    * How to recover from bricked boxes?
        * Don't test on those boxes.
        * By the time a release has been deployed to a site without physical accessibility, it has already been tested extensively.
        * If you brick a box you cant physically get to, be sad.
    * How did you get the OK from management?
        * Netflix has a very strong culture of "freedom and responsibility". Try to avoid telling people what specifically hey have to do, so long as you make your choices responsibly.
    * Why FreeBSD as the OS?
        * Primary driver at the time was licensing. There was consternation at the time over GPLv3
        * Not a compelling reason to leave
        * Ostensily better performance (periodically evaluated)
        * Like the community / upstream: insistanece on perfection
    * Are there other teams tracking head for other OSS projects?
        * Don't know.
    * Are older OS releases patched for security? How is this deployed?
        * The upstream does this with point releases.
        * Netflix does not use these internally, since they are running the latest dev version anyway.
        * Cherry-picking is sometimes done if needed.

