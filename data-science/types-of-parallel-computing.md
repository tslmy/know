---
description: A mindmap.
---

# Types of Parallel Computing

![](../.gitbook/assets/image%20%282%29.png)

## Multiple computers

### Grid Computing

* Generally, each node performs a different task/application
* Generally, more heterogeneous
  * Geolocationally, sometimes across regions / companies / institutions
  * In terms of hardware components
* \(job schedulers\)
  * Oracle Grid Engine / Sun Grid Engine \(SGE\) / Computing in Distributed Networked Environments \(CODINE\) / Global Resource Director \(GRD\)
  * Univa Grid Engine \(UGE\)

### Cluster Computing

* Generally, all nodes perform same/similar tasks
* Generally, more homogeneous
  * Usually connected by LAN
  * Geolocationally, often same server stack
* May be viewed as a single computer at times

## Single Computer

* **Multiprocessing**: Using &gt;1 \(Cores of\) CPUs
* **Multithreading**: Using only one \(core of\) CPU
  * Interleaved/Temporal multithreading
    * **Coarse-grained / block / cooperative multithreading**: Run till you need to wait \(say, for memory\), then I’ll let other thread run
    * **Interleaved multithreading**: you walk a step, then someone else, then you, then someone else…
  * **Simultaneous multithreading \(SMT\):** exploit parallelism available across multiple threads to decrease the waste associated with unused issue slots 
* **General-purpose computing on graphics processing units \(GPGPU\)**

