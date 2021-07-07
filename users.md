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

*Summary: Contact the HPC committee for a user account, then VPN to Oxy and SSH into `bletchley.oxy.edu`.*

<!-- FIXME should we create an email address for the HPC committee? -->
Bletchley is administered by the HPC committee, which currently includes Profs. [Jeff Cannon](mailto:jcannon@oxy.edu) (Chemistry), [Justin Li](mailto:justinnhli@oxy.edu) (Cognitive Science, Computer Science), [Diana Ngo](mailto:dngo@oxy.edu) (Economics), [Janet Scheel](mailto:jscheel@oxy.edu) (Physics), and [Amanda Zellmer](mailto:zellmer@oxy.edu) (Biology), led by [David Dellinger](mailto:ddellinger@oxy.edu) (ITS). To get access to Bletchley, you should contact one of us with a description of what you plan to use Bletchley for. We would be happy to talk you through Bletchley's capabilities, and how it can best assist with your research or project.

Once we have confirmed that Bletchley is able to support your work, we will create a user account for you on the cluster and email you with your username and password. Since Bletchley hosts research data from many Oxy faculty, including potentially sensitive personal information, it is only accessible from Oxy's network. To log in from off campus, you will need to install a *virtual private network* (*VPN*). A VPN creates a "tunnel" between your computer and Oxy, so that your computer will essentially *be* part of Oxy's network for all intents and purposes. You can use a VPN to access journals that Oxy has subscriptions to, but more importantly for us, you will also be able to log into Bletchley.

__To install a VPN client__, follow [ITS' instructions for installing Fortinet](https://helpdesk.oxycreates.org/kb/?s=VPN) on your [Windows](https://helpdesk.oxycreates.org/kb/2016/07/setting-up-the-windows-fortinet-vpn-client/) or [Mac](https://helpdesk.oxycreates.org/kb/2016/07/setting-up-the-mac-os-x-fortinet-vpn-client/) computer. Once you have installed Fortinet, you should make sure that the connection is activated as well. If you are unable to connect, you may need permission from ITS to use the VPN; please email ITS or the HPC Committee for help.

Be aware that when you are connected to Oxy's VPN, *all* your internet traffic is sent to Oxy first. If you are not comfortable with this, be sure to *only* connect your VPN when needed, and to disconnect when you are done.

Once you have activated the connection to Oxy's network, you can now SSH to log into Bletchley. *SSH* stands for "secure shell", and allows you interact with Bletchley and tell it what to do.

__To SSH into Bletchley from your computer__, you will need a terminal. If you are on a Mac, you can open the Terminal app. On Windows, you can FIXME. Regardless, once you are in the terminal, you should type (replacing `username` with your given username):

```
ssh username@bletchley.oxy.edu
```

Then press Enter. You will then be prompted for password. *Note that when you type your password, no characters will show up - this is normal!* If your log in to Bletchley is successful, your screen should not look markedly different. Here is what my screen shows:

```
[justinnhli@air2019 ~]$ ssh justinnhli@bletchley.oxy.edu
justinnhli@bletchley.oxy.edu's password:
Last login: Sat May  1 15:52:20 2021

[justinnhli@bletchley ~]$
```

To confirm that you've logged in, you can type:

```
hostname
```

This command will print out which computer you are currently on. After you press Enter, the screen print `bletchley.oxy.edu`, which means that you have successfully logged into Bletchley.


<!--
* user accounts (who to contact)
* VPN and SSH
-->

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
