# Bletchley Users Guide

## Table of Contents

* [The Bletchley Cluster](#the-bletchley-cluster)
* [Accessing Bletchley](#accessing-bletchley)
* [Command Line Basics](#command-line-basics)
* [The Slurm Workload Manager](#the-slurm-workload-manager)
* [Language-Specific Examples](#language-specific-examples)
    * [Docker](#docker)
    * [Gaussian](#gaussian)
    * [Matlab](#matlab)
    * [Python](#python)
    * [R](#r)
* [Additional Support](#additional-support)
* [Appendix: Bletchley Technical Details](#appendix-bletchley-technical-details)

## The Bletchley Cluster

*Summary: Bletchley is a powerful computer open for use by anyone in the Oxy community.*

Bletchley is a *high-performance computing (HPC) cluster* - a (network of) computers that work together to perform computations. Bletchley is Oxy's own cluster, the result of an [NSF MRI grant](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1919771). In a lot of social and physical sciences, research increasingly involves processing large amounts of data or finding the optimal configuration out of many possible parameters. Doing this requires not only requires lots of computing power, but also multi-day run-times that Oxy's other infrastructure cannot support. The Bletchley cluster exists to support these kinds of research, and also acts as an instrument where students can learn how to apply computational methods.

Bletchley is open to be used by Oxy professors and students for teaching and research. This document serves as a technical user guide to Bletchley, and will walk through how to get access, some technical background on the command line and the workload manager, as well as starter code for running your program on the cluster.

<!--
* what is it? why?
* who can use it?
* who to contact to start using it?
-->

## Accessing Bletchley

* VPN and SSH
* FTP?
* user accounts (who to contact)

## Command Line Basics

* the command line
* getting help
* basic navigation
* text editing (advanced)

## Uploading Files

* FTP?

## The Slurm Workload Manager

* overall architecture/components
    * queues
* job submission commands
* job monitoring commands

## Language-Specific Examples

### Docker

### Gaussian

### Matlab

### Python

### R

## Additional Support

* who to email

## Appendix: Bletchley Technical Details

As of summer 2021, the cluster is made of 27 individual computers (*nodes*), including:

* 1 *head node* that manages the jobs to be run by the other nodes
* 24 *compute nodes* that does the actual work. Each compute node has:
    * 36 * 2.6GHz CPUs
    * 8 nodes with 2.6, 10.6, and 21.3 GBs RAM/CPU each
    * 960 GB hard disk space
* 1 *GPU node* with several GPUs to speed up certain kinds of operations
* 1 *storage node* that can store results and datasets
    * 2 * 960GB hard disk space
    * 34 * 8TB long-term storage space

<!--
* what is available?
    * in terms of computing power and storage
    * in terms of hardware
-->
