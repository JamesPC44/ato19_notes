# ATO19: Raspberry Pi is a Gateway Drug for GPUs

*Ray Hightower* of Bridgetown partners, LLC

rayhightower.com (should have slides)

Sponsored by industrial.io

**Parallelism**: boosting performance by executing at least two threads at the same time. At least two threads are executing simultaneously.

**Concurrency**: At least two threads are making progress.

**Why parallelism?**: Moore's Law is running out.

In other words, parallelism requires multiple things happening at once, while concurrency may just be time sharing of a serial processor.

How can parallelism be used? Embarrasingly parallel problems such as finding prime numbers.

*The speaker discusses their Pi cluster*.
Example of [mpi4py](https://bitbucket.org/mpi4py/mpi4py/src/master/) for finding prime numbers.

The **parallella** - a single board computer focusing on parallelism. 2x ARM cores, plus 16x Epipheny RISC cores in a 4x4 mesh arrangements. Bus architecture expandable up to 64x64 cores. The parent company Adaptiva ultimately went under and the Parallela is no longer manufactured.

Raspberry Pi is a gateway drug for GPUs in the sense that we can learn about parallelism by clustering Pis,and translate this knowledge into use with GPUs.

nVidia Jetson Nano 4x AR mcores, 128 CUDA cores. [pyCUDA](https://mathema.tician.de/software/pycuda/).
jetBots -- live demo with the Jetson Nano demonstrating real-time obstacle avoidance using deep learning.

**Parallelism accellerates deep learning**.

Resources
* Build Supercomputers with Raspbery Pi 3 -- Carlos R. Morrison
* CUDA by Example -- Jason Sanders 7 Edward Kandrot
* coco
* imagenet

Questions
* How to get started?
    * nVidia has a Jetson Nano intro page
    * there are Pi tutorials on rayhightower.com

