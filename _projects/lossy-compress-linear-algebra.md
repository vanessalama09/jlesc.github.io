---
layout: page_project
title: Effective Use of Lossy Compression for Numerical Linear Algebra Resilience and Performance 
date: 2019-01-22
updated: 2020-02-27
navbar: Research
subnavbar: Projects
project_url:
status: running
topics:
  - resilience
  - numerics
keywords:
head: calhoun_j
members:
  - altenbernd_m
  - speck_r
  - cappello_f
---

## Research topic and goals

Prior work has shown the effectiveness of using a multigrid hierarchy to
compress the iterative solution to reduce checkpoint size. Recently specially
designed floating-point lossy compression algorithms have gained increased
popularity due to their ability to significantly reduce floating-point data
size and bound the error at each data point. The focus of this collaboration is to explore how to use
compression techniques to improve checkpoint-based recovery routines for
multigrid methods used either as a stand alone linear system solver or as a
preconditioner for other methods such as GMRES or CG. In particular, we explore
hybrid compression techniques that switch between the lossy compressor SZ
developed at ANL and multi-level multigrid compression in order to minimize the
resilience overhead. When using SZ we explore various methods of setting the
compressor’s error bounds such as a static tolerance and one that varies the
tolerance based on the current accuracy of the solver. To improve the quality
of the compressed checkpoint we create and solve a local problem based on the
patch of the solution that we are recovering. Finally, we plan to create performance
models to explore theoretical possibilities for new compressor designs and
system architectures.

The project involves JLESC Fellow Jon Calhoun, JSC affiliated graduate student
Mirco Altenbernd, Robert Speck from JSC, and Franck Cappello from Argonne. This
project was formed though collaborative discussions at the 2018 JLESC workshop
in Barcelona.


## Results for 2019/2020

In-progress results from comparing SZ lossy compression vs multigrid compression for
checkpointing iterative linear solvers was presented at the SPPEXA workshop in Dresden
(October 2019). Currently, a journal article based on the results in being
prepared for submission to the IEEE Transactions on Parallel and Distributed
Systems.

Preliminary results on evaluating current state-of-the-art compressors for use
inside the pySDC application from Robert Speck were accepted and presented as
an ACM student research competition (SRC) poster at SC'19. Results showed that
specially designed lossy compressors are effective at reducing the runtime
memory size, but long compression/decompression times results in slowdown.

## Results for 2020/2021



Integration of in-line lossy compression was explored using ZFP compressed arrays. ZFP compressed arrays use  a block-based compression scheme to enable random access into the compressed data. Moreover, ZFP compressed arrays use a software cache to mitigate the impact of decompression time on the critical path. During this year, we ran several HPC computation kernels (e.g. matrix-matrix multiplication, sparse matrix-vector multiplication) and two Department of Energy mini-apps Branson and Pennant. Results show that use of in-line compression reduces runtime memory requirements, but does degrade runtime performance by an order-of-magnitude. Error in the mini-app solutions compared to a version without lossy compression grows logarithmically with compressions in each iteration.  From this exploration, we plan to build a generic compression runtime system to support any compressor as an in-line compressor. This generic framework will be integrated into the pySDC application of Robert Speck (JSC) for further testing.

To protect compressed data from catastrophic corruption due to silent data corruption caused by a soft error, we develop the automated resiliency for compression (ARC) tool. ARC applies error-correcting codes to lossy compressed data to detect/correct silent data corruption. Results show that ARC is able to protect against potentially100-1000s of bit-flips in the compressed arrays with encoding and decoding bandwidths up to 3.6 GB/s on a modern multi-core CPU.


## Visits and meetings

* Completed: Visit by Mirco Altenbernd to Clemson, Spring 2019 for 2 months.
* Completed: Present talk at JLESC Meeting in Knoxville, April 2019.
* Completed: Brief meetup and presented in progress work at SPPEXA workshop in Dresden, October 2019.
* Planned: Present talk at JLESC Meeting in Bonn, April 2020.


## Impact and publications

* One ACM student research competition poster at Supercomputing 2019.

{% bibliography --cited --file jlesc.bib %}


## Future plans

Create performance models for using lossy compression inside running HPC applications. Integrate lossy compression algorithm into applications and measure the impact on performance / accuracy.

## References


{% bibliography --file external/lossy-compress-linear-algebra.bib %}

