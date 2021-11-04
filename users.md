# Bletchley Users Guide

## Table of Contents

* [The Bletchley Cluster](#the-bletchley-cluster)
* [Accessing Bletchley](#accessing-bletchley)
* [Command Line Basics](#command-line-basics)
* [Uploading and Downloading Files](#uploading-and-downloading-files)
* [Running Your Code](#running-your-code)
    * [Running Jobs in the Foreground](#running-jobs-in-the-foreground)
    * [Running Jobs in the Background](#running-jobs-in-the-background)
    * [Monitoring and Managing Jobs](#monitoring-and-managing-jobs)
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

Bletchley is a *high-performance computing (HPC) cluster* - a network of computers that work together to perform computations. Bletchley is Oxy's own cluster, the result of an [NSF MRI grant](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1919771). In a lot of social and physical sciences, research increasingly involves processing large amounts of data or finding the optimal configuration out of many possible parameters. Doing this requires not only requires lots of computing power, but also multi-day run-times that Oxy's other infrastructure cannot support. The Bletchley cluster exists to support these kinds of research, and also acts as an instrument where students can learn how to apply computational methods.

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

*Summary: Know what "command", "options", and "arguments" are, and know how to use `cd`, `ls`, and `man`. Use a tutorial for everything else.*

The *command line interface* (CLI) or sometimes the *terminal* is a text-based interface for doing things on a computer. CLIs were originally the only way to get a computer to do things, until the development of the graphical user interface (GUI) in the mid 1970s, which eventually led to Windows and OS X that you're familiar with. Here is an example command line session:

```
[justinnhli@bletchley ~]$ ls
 bin   courses   Desktop   Downloads   Dropbox   git   Library   media  'My Games'   oxy   papers   pim   scholarship   work
[justinnhli@bletchley ~]$ ls -l
total 84
lrwxrwxrwx  1 justinnhli justinnhli    20 2016-05-21 16:15  bin -> git/dotfiles/bin/bin
lrwxrwxrwx  1 justinnhli justinnhli    18 2021-07-07 17:53  courses -> oxy/courses/202201
drwxr-xr-x  4 justinnhli justinnhli  4096 2021-07-07 11:10  Desktop
drwx------  4 justinnhli justinnhli 32768 2021-07-17 11:50  Downloads
drwx------ 14 justinnhli justinnhli 12288 2021-07-19 17:21  Dropbox
drwxr-xr-x 20 justinnhli justinnhli  4096 2021-07-18 21:51  git
lrwxrwxrwx  1 justinnhli justinnhli    24 2020-01-26 22:06  Library -> git/dotfiles/pip/Library
drwxr-xr-x  9 justinnhli justinnhli  4096 2021-07-03 17:31  media
drwxr-xr-x  3 justinnhli justinnhli  4096 2018-05-29 08:33 'My Games'
lrwxrwxrwx  1 justinnhli justinnhli    12 2017-08-15 13:08  oxy -> Dropbox/oxy/
drwxr-xr-x 28 justinnhli justinnhli  4096 2021-01-07 13:32  papers
lrwxrwxrwx  1 justinnhli justinnhli    11 2020-05-19 11:34  pim -> Dropbox/pim
lrwxrwxrwx  1 justinnhli justinnhli    20 2017-01-17 12:04  scholarship -> Dropbox/scholarship/
drwxr-xr-x 11 justinnhli justinnhli  4096 2016-05-25 11:50  work
[justinnhli@bletchley ~]$ ls -l Dropbox
total 33516
-rw-r--r--  1 justinnhli justinnhli       51 2017-03-31 18:55  api_keys
drwxr-xr-x  2 justinnhli justinnhli     4096 2021-06-17 15:39  bin
drwxr-xr-x  2 justinnhli justinnhli     4096 2021-07-13 14:02 'Camera Uploads'
drwxr-xr-x  2 justinnhli justinnhli     4096 2021-07-03 12:05  croncheck
drwxr-xr-x  5 justinnhli justinnhli     4096 2020-12-04 23:42  music
drwxr-xr-x  3 justinnhli justinnhli    16384 2021-06-23 11:07  obsidian
drwxr-xr-x 16 justinnhli justinnhli     4096 2020-04-09 21:46  oxy
drwxr-xr-x  8 justinnhli justinnhli     4096 2021-01-10 17:41  personal
drwxr-xr-x  8 justinnhli justinnhli     4096 2021-07-16 19:47  pim
drwxr-xr-x 20 justinnhli justinnhli     4096 2021-07-14 16:08  projects
drwxr-xr-x  5 justinnhli justinnhli     4096 2021-07-06 21:18  reference
-rw-r--r--  1 justinnhli justinnhli   305937 2020-01-22 13:31  scanned-pages.pdf
drwxr-xr-x 10 justinnhli justinnhli     4096 2018-09-07 22:39  scholarship
-rw-r--r--  1 justinnhli justinnhli  2460602 2021-04-17 23:27  wallpaper.png
[justinnhli@bletchley ~]$
```

There is a lot of information here that is irrelevant for using Bletchley, so we will focus on four things: the *prompt*, *commands*, *options*, and *arguments*. For example, the first line above (`[justinnhli@bletchley ~]$ ls`) has two parts:

* Everything before the dollar sign (`[justinnhli@bletchley ~]$`) is the *prompt*. Your specific prompt may be different, but this is the computer waiting for you (or *prompting* you) to tell it to do something.

* The remainder of that line (`ls`) is the *command*. Every command tells the computer to do something - in this case, `ls` asks the computer to *l*i*s*t the files in the current folder. The result of that command is the second line of the transcript above, so you can see that the folder has a `bin` file/folder, a `courses` file/folder, and so on.

In the next line of the transcript, we issued another command (`ls -l`). Like before, this is asking the computer to list files, except we also gave it the `-l` *option*. As the name suggests, this tells the computer to do something slightly different - in this case, don't just list the file names, but also show additional information those files, such as when it was last modified.

Finally, the last command we gave in the transcript is (`ls -l Dropbox`). The final part here (`Dropbox`) is the *argument*, which tells the computer *which folder* to list the contents of. In general, *options* will being with a hyphen (`-`), while *arguments* will not.

To sum up, to use the command line, the computer will give you a *prompt* for you to tell it what to do. Everything you type in is a *command*, and you can specify *how* that command works with *options*, and *what* it runs on with *arguments*.

That's really it! The rest of using the command line is about knowing what commands exist. We will look at a few below.

### Navigating via the Command Line

When you first log into Bletchley, you will be in your "home directory". ("Directory" is another word for "folder".) All your files and folders will be inside this directory, and it's your private workspace on the cluster. To confirm this, the first command is `pwd`:

```
[justinnhli@bletchley ~]$ pwd
/home/justinnhli
[justinnhli@bletchley ~]$
```

`pwd` stands for "present working directory", and it tells you which folder you are in; in this case, we are currently in `/home/justinnhli`. This means that you are currently in the `justinnhli` folder inside the `home` folder, which is where all home directories exist.

To make things more interesting, let's create a new folder. You can do this with the `mkdir` command:

```
[justinnhli@bletchley ~]$ mkdir test
[justinnhli@bletchley ~]$
```

`mkdir` stands for "make directory", and the command should have created a folder called `test`. Notice that nothing else was printed out after the `mkdir` command. This is perfectly normal - CLIs tend to be rather terse, so no printout usually means that the command succeeded. To confirm that we did in fact create the `test` folder, we can use `ls`:

```
[justinnhli@bletchley ~]$ ls
 test
[justinnhli@bletchley ~]$
```

The last command we will talk about here is `cd`, which stands for "change directory". As you might imagine, this will take you inside a folder:

```
[justinnhli@bletchley ~]$ cd test
[justinnhli@bletchley test]$ pwd
/home/justinnhli/test
[justinnhli@bletchley test]$ ls
[justinnhli@bletchley test]$
```

The three commands we used here first took us into the `test` folder (`cd test`), then printed out where we were (`pwd`), and finally listed the (currently empty) `test` folder (`ls`). You will notice that the prompt has also changed to show me which folder we are in; we configured the prompt do to this, so don't be worried if yours doesn't.

Finally, we can go back to our home directory using `cd` without any arguments:

```
[justinnhli@bletchley test]$ cd
[justinnhli@bletchley ~]$ pwd
/home/justinnhli
[justinnhli@bletchley ~]$
```

You will use these three commands - `cd`, `ls`, and `pwd` - over and over again as you work on Bletchley, so you should get pretty familiar with what they do and how they work.

### Additional Resources

Mastering the command line takes years, so we recommend learning commands as you need them. If you want to learn more, however, here are some resources you might use:

* [Command Line for Beginners tutorial](https://ubuntu.com/tutorials/command-line-for-beginners) - a complete tutorial on learning the command line.
* [Command Line Cheat Sheet](https://justinnhli.oxycreates.org/bash/) - a handy reference for common commands that you will use.
* [A-Z Index of Commands](https://ss64.com/bash/) - a comprehensive reference for commands you might see.

The last thing we will say is this: Google is your friend. Thousands of people have learned to use the command line and have asked questions on forums like Stack Overflow. If in doubt, just google a command (eg. "ls command line"), and there will be pages and pages of resources to help you figure things out.

<!--
* the command line
* basic navigation
* additional resources
-->

## Uploading and Downloading Files

*Summary: Use an FTP client to move files to and from Bletchley.*

Although you can create and edit files on Bletchley, the easiest way to write your code is to do it on your own computer then upload it to Bletchley. To do this, you will need an FTP client; we recommend [FileZilla](https://filezilla-project.org/download.php?show_all=1). Once you have installed FileZilla, you can follow [their tutorial](https://wiki.filezilla-project.org/FileZilla_Client_Tutorial_(en)) (substituting your Bletchley login information) to upload files to the cluster. FileZilla will also allow you to download files from Bletchley, so that you can do additional analysis on your computer.

More advanced ways of moving files to Bletchley and keeping the files in sync with each other, such as using git, are beyond the scope of this tutorial.

__Important__: Note that Bletchley does __not__ have a backup/archive system. This means that if you delete something from Bletchley, there is no way to recover that file if you don't have a copy yourself. For this reason, we recommend uploading files to Bletchley only once they are ready, and downloading any changed code or result files from Bletchley as soon as possible.

## Running Your Code

*Summary: Run your code by submitting it to Slurm, Bletchey's job manager.*

Almost all high-performance clusters like Bletchley have a *workload manager* or *job scheduling system* that manages what programs are running and where they run. On Bletchley, this program is called Slurm. Slurm's role is to make sure that whenever someone wants to use Bletchley, they can be assigned a CPU (or multiple CPUs) with enough memory to run their program, without monopolizing the cluster from other people. Although you can run programs directly on Bletchley, this is *highly* discouraged, as you may prevent other users from doing their work; anyone found doing this may have their access to Bletchley removed. Running programs directly from the command line should be reserved for testing your code, and once you are confident your code works, you should then ask Slurm to assign your program to a CPU.

In general, your workflow for using Bletchley will look like this:

1. Develop the code on your own computer, and make sure that it works there (on a small example).
2. Upload your code to Bletchley.
3. Run your code from the command line in Bletchley on a small example, to make sure it still works.
4. Modify your code to do the actual work instead of the small example.
5. Submit your code to Slurm and wait for it to finish
6. Download any result files to be analyzed.

In workload manager parlance, the code your submit to Slurm is called a *job*. When you submit a job to Slurm, you must specify which *partition* the job goes into. For Bletchley, the partitions are separated by the amount of memory your code needs, and how long you think your code will run for. Based on those requirements, Slurm will then assign an appropriate CPU(s) to run the job. The partitions available on Bletchley are:

* `demo`, which has a runtime limit of 1 minute
* `teaching`, which has a runtime limit of 5 minutes
* `short`, which has a runtime limit of 5 hours
* `medium`, which has a runtime limit of 48 hours
* `long`, which has a runtime limit of 7 days
* `unlimited`, which has an unlimited runtime

Note: there are additional partitions reserved for particular research groups; your professor or the HPCC will tell you if you should use any of those instead.

When picking a partition to submit your job to, you should pick the one that gives enough time for your program to finish, but not too much beyond that. This is because Slurm uses these time estimates to assign CPUs, and also because if you are in a partition with long jobs, it may take longer before your job is run.

### Running Jobs in the Foreground

*Summary: Use the `srun` command to submit jobs to Slrum.*

Submitting jobs to Slurm is done through the `srun` command. The complete syntax for the command is:

```sh
srun --partition=<PARTITIONS> --nodelist=<NODELIST> --output=<FILENAME> COMMAND ...
```

To break this down:

* `srun` is the name of the command
* `--partition=<PARTITIONS>` is an option that tells Slurm which partition you would like your code to run on. If you don't provide this option, Slurm will run the job on the `demo` partition by default.
* `--nodelist=<NODELIST>` is an option that tells Slurm which specific *node* you would like your code to run on. See below for details. If you don't provide this option, Slurm will run the job on `n001` by default.
* `--output=<FILENAME>` is an option that tells Slurm what file to store the output of your command. If you don't provide this option, Slurm will directly print the output by default. __BE CAREFUL!__ If the file you specified already exists, Slurm will overwrite it without asking.
* `COMMAND ...` are the arguments to `srun`; this would be how you normally run your code without Slurm.

Remember how Bletchley is is actually a network of computers? Each of these computers is called a *node*, or more specifically a *compute node*, which does the actual work. When you log into Bletchley, you are actually logging into the *head node*, a special node which tells the other nodes what to do. Bletchley is currently (as of Fall 2021) made of 24 compute nodes, named `n001` to `n024`, with different amounts of memory available:

* `n001`-`n008` each has 24 CPUs, with 2.6GB of RAM per CPU
* `n009`-`n016` each has 24 CPUs, with 10.6GB of RAM per CPU
* `n017`-`n024` each has 24 CPUs, with 21.3GB of RAM per CPU

There is an additional node, `gpu01`, which has two GPUs for specialized computation. Your professor or the HPCC will tell you if you should use this node instead. As with selecting a partition, you should also pick a node with just enough memory for your program, so that more powerful nodes remain available for other users.

Putting all of this together, we will use this Python program as the demonstration:

```python
# hostname.py
import socket

print(socket.gethostname())
```

We can run the script like this:

```
[justinnhli@bletchley ~]$ python3 hostname.py
bletchley.oxy.edu
```

As you can see, the only thing the script does is print the name of the current node, which in this case is `bletchley.oxy.edu`. If we wanted to run this with Slurm instead, we will first have to decide the partition and the node to use. Since this script is so simple, we can just use the `demo` partition (for a runtime of up to one minute) and node `n001` (since we don't need much memory at all). Together, the command to run the script would be:

```sh
srun --partition=demo --nodelist=n001 --output=output.txt python3 hostname.py
```

This means that we are asking Slurm to run `python3 hostname.py` on the `demo` partition on node `n001`, and saving the output to `output.txt`. Let's see what happens when we do this:

```
[justinnhli@bletchley ~]$ ls
hostname.py
[justinnhli@bletchley ~]$ srun --partition=demo --nodelist=n001 --output=output.txt python3 hostname.py
[justinnhli@bletchley ~]$ ls
hostname.py  output.txt
[justinnhli@bletchley ~]$ cat output.txt
n001.cluster.com
```

Walking through step by step:

1. We first do `ls` to see that the only thing in the current folder is `hostname.py`
2. We submit the job to Slurm with `srun`. Notice that nothing is printed; this means that Slurm has accepted the job.
3. When we do `ls` again, we now see there's a new file, `output.txt` - the file we told Slurm to save the output to.
4. The `cat` command simply prints out its arguments, so `cat output.txt` will print out the contents of `output.txt`. As you can see, the result is `n001.cluster.com` - which means that our script actually ran on node `n001`.

That's the basics of submitting a job to Slurm. The `srun` command has a lot of other options, which you can look up at <https://slurm.schedmd.com/srun.html>.

### Running Jobs in the Background

*Summary: Append `&` to the `srun` command to run jobs in the background.*

It wasn't noticeable with the previous example, which takes less than a second to run, but the Python program was actually running in the *foreground*. That is, your computer must remain connected to Bletchley, and it will stop the job if you log off. Often, what we want is for the job to run in the *background*, so that even if your disconnect, the job will continue running until it is done.

We will need a longer running job to demonstrate this, so here's a Python countdown program:

```python
# countdown.py
from time import sleep

n = 300
for time in reversed(range(1, n + 1)):
    print(time)
    sleep(1)
```

This program will count down from 300 every second until it reaches 0, meaning it will take 300 seconds = 5 minutes to complete. If we run it as before:

```
[justinnhli@bletchley ~]$ srun --partition=demo --nodelist=n001 --output=output.txt python3 countdown.py
```

Your command line will just hang waiting for the program to finish - nothing will happen even if you type more commands or press Enter. (Note that the job will actually be terminated after 1 minute instead of the full 5 minutes, because we are running it on the `demo` partition.) To make the job run in the background instead, we append a `&` at the end of the `srun` command:

```
[justinnhli@bletchley ~]$ srun --partition=short --nodelist=n001 --output=output.txt python3 countdown.py &
[1] 196488
[justinnhli@bletchley ~]$
[justinnhli@bletchley ~]$ ls
countdown.py
```

Notice that this time, the command line will respond if we run the `ls` command. If we wait the 5 minutes and come back, we will see that `output.txt` indeed as our countdown:

```
[justinnhli@bletchley ~]$ cat output.txt
300
299
298
[...]
```

### Monitoring and Managing Jobs

*Summary: Use the `squeue` command to see what jobs are running, and the `scancel` command to cancel running/scheduled jobs.*

In addition to submitting jobs, you can also check on jobs that Slurm is currently running, and cancel them if it's necessary. If we submit a job for `countdown.py` as before, we can check on its status with the `squeue` command:

```
[justinnhli@bletchley ~]$ srun --partition=short --nodelist=n001 --output=output.txt python3 countdown.py &
[1] 200570
[justinnhli@bletchley ~]$ squeue
             JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
             17240     short  python3 justinnh  R       0:02      1 n001
[justinnhli@bletchley ~]$
```

The `squeue` command prints out all the jobs that are running or are waiting to run. The output is a table with the following columns:

* `JOBID` - the ID of the job, which is used to refer to the job in other commands such as `scancel` (see below)
* `PARTITION` - the partition that the job is running on
* `NAME` - the name of the command that the job is currently running
* `USER` - the user who submitted the job
* `ST` - the status/state of the job. There are a large number of possible states, but the main ones you will see are:
    * `PD` means the job is pending (waiting for a free CPU)
    * `R` means the job is running
    * `CD` means the job has completed
    * `CA` means the job was canceled
    * `F` means the job has failed
* `TIME` - the amount of time the job has been running for
* `NODES` - the number of nodes the job is running on
* `NODELIST(REASON)` - the specific node(s) that the job is running on

As with the `srun` command, you can look up the other options for `squeue` and `scancel` at <https://slurm.schedmd.com/squeue.html> and <https://slurm.schedmd.com/scancel.html> respectively.

### Running Multiple Jobs at Once

## Language-Specific Examples

This section contains additional information for specific languages/applications.

### Docker

### Gaussian

### Matlab

### Python

It is common for Python projects to require additional packages, which you should install using `pip` in a virtual environment. See <https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/> for a detailed set of instructions for how to do this.

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
