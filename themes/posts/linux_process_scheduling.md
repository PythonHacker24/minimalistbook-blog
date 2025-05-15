+++
category = "technical"
title = "Linux Process Scheduling — The Reason your Linux System Processes so Efficiently (Kernel Perspective)"
date = 2024-02-02
+++

*Preface: I was going through the book “Linux Kernel Development” by Robert Love, one of the best books I have referred to for low-level stuff and understanding the workings of Linux. I study this book with intensity, simplify the concepts and write it down here so that the readers can get a straightforward description and all they need to know about the topic. Covering the whole Linux Process Scheduling is not possible and is not the goal of this article. It’s to let you know the topic in more depth than a summary can provide and create a pathway you need to go to learn the topic.*

## A Quick Introduction to the Topic
The handling of processes in an Operating System like Linux is a vital topic for understanding the working of the Kernel. The logic behind scheduling processes in the system and prioritising them in a manner that is the most optimised and efficient, while considering some trade-off gives an insight on real-life engineering behind low-level computer stuff.

To understand what a process is, I highly recommend you go through my previous article, “Linux Processes — A Kernel’s Perspective Explained with Clarity and Simplicity” where I explain the processes and threads simply and concisely.

To understand the topic, appreciating the concept and then moving towards understanding the code structure is important. Here, the code part would not be covered as explaining the chain of concepts is taken to the priority.

## The Significance of Process Scheduling
A Kernel by definition is the abstraction layer between the Operating System and the Hardware. An Operating System has a lot of tasks running simultaneously to make things happen in the way they are intended to be. Even an idle system has a lot going under the hood and the Kernel needs to interact with the hardware in a way that each task is carried out in the most appropriate way possible.

Since an Operating Systems have multiple processes running (definitely more than the processors on the system), the Kernel has to decide which process to consider at the given time. Modern hardware has multiple processors (multiple cores) and the Kernel needs to make use of them in the most reliable way possible. This whole work of decision-making is made by the process scheduler in the Linux Kernel.

![diagram](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*xuhuHRLCeeVghN8BDEEdcQ.png)

If there are any processes that too in a runnable state, the processor should be always running. In the case of multiple, time-consuming processes, some processes must be paused or kept waiting in a way that the system functions in the way it is intended to work. This happens with the mechanism of prioritisation of tasks, which the process scheduler in Linux Kernel handles.

## The Concept of Multitasking
A *Multitasking Operating System* by definition has the ability to execute multiple processes on the system simultaneously. On a single processor machine, it can give an illusion that all the processes are running simultaneously at the same time (actually the processor can focus on one process at any time, but the execution is not only the definition of the process, it is the whole thing from memory allocation and multiple processes spawning. Hence, the system seems to be having multiple processes running at the same time. A task which is marked as sleeping is also a process, it’s just the processor is busy with something else). On a multiprocessor machine, these processes are running simultaneously in parallel while some more processes are blocked or sleeping, waiting to get executed when a processor is free. A lot of processes might be residing in the memory, they might just be waiting for some input from an external device, and at that time, it might also be the case that only one process is in a runnable state. The Linux Scheduler manages all this with precise mechanisms to make the system smooth and interactive.

There are two types of multitasking in operating systems: *cooperative multitasking* and *preemptive multitasking*. A very concise definition of them is that *cooperative multitasking* operating systems have no right to stop the process during the execution and the process has to exit on its own. On the other hand, a *preemptive multitasking operating system* has the right to stop the execution of the process at any time. Unix, at its core, has been implementing *preemptive multitasking* and Linux Kernel has been implementing *preemptive multitasking* (it’s obvious that if *cooperative multitasking* is used and a process hangs and does not exit due to any reason, it can potentially bring down the whole system).

The Implementation of Policy
Policy is the behaviour of the scheduler that determines what runs when. To optimally use the processor time, Linux Process Scheduler implements some policy that determines which process to run at a given time and what process to keep waiting to make the most out of system resources.

There are a few terms that are considered while following a policy. They are:

1. **I/O-Bound Versus Processor-Bound Processes**
2. **Process Priority**
3. **Timeslice**

## I/O-Bound Versus Processor-Bound Processes
Processes can be divided into two types, the processes which are controlled by external devices (like keyboard, mouse, drives, etc.) are *I/O-Bound Processes*. These processes are most of the time idle and consume less processor time. But these are the ones that are responsible for making the system responsive to the user. For example, keyboard input must be processed at each stroke or else the system will not feel responsive. No matter how fast the user types (it’s not going to be that fast for the computer), this process is idle most of the time and resides in the memory. Hence, this process takes less processor time but needs to run as soon as it needs to be. On the other hand, *Processor-Bound Processes* consume significantly more processor time but do not need to be processed at a particular stroke of time. They can be kept in the memory and processed as per the processor’s state. For example, video rendering takes significant processor time but does not care the amount of time is taken to render the whole video (of course fast rendering would be great but a small latency in video rendering can be accepted than latency in typing in a text editor).

The *Process Scheduler* is responsible for deciding when to process an *I/O-Bound Process* and when to pause/resume the execution of a *Processor-Bound Process*.

Note that a process can be both, an *I/O-Bound Process* and a *Processor-Bound Process*. For example, Word-Processor, which requires quick processing of keyboard input and also does a spell-check simultaneously or some macro calculations).

## Process Priority
Setting up a priority value for a process helps the Linux Scheduler to measure the weight of the process and its requirements to the system. A term called *nice value* is used which ranges from -20 to 19. A lower nice value corresponds to higher priority and vice versa (a less nice value means the process is less nice to other processes and requires more processor attention).

A very important point to be mentioned here: Unix allocates timeslices *proportionally* and not *absolutely* unlike some other operating systems and the same goes with Linux. This means that having a lower *nice value* (higher priority) will give a process relatively more time than a process with a higher nice value (lower priority). This depends upon the number of processes in the system and certain parameters in the Operating System. More discussion on this topic is out of the scope as this is a huge topic about why this is implemented and the approach towards *perfect multitasking*.

A second range is *real-time* priority which is on a different track with *nice value*. Opposite from nice value, higher *real-time priority* refers to more priority and vice versa. Linux implements real-time priority as per Unix standards specifically POSIX.1b standards. All real-time processes have higher priority than the normal processes.

## Timeslice
A *timeslice* is a numerical value that represents how long a task can run until it is preempted. The policy of the scheduler dictates the default timeslice. Too long *timeslice* reduce the responsiveness of the system as more processor time will be allocated to individual processes, reducing the speed of the queue of processes. If too little *timeslice* is provided, then the switching will happen so fast that the process of switching itself will take most of the time (this is called the switching overhead and occurs when a process is preempted and switched to the next one consuming some time) which further decreases the throughput of the processor (the processor wastes time in switching more than it processes). Hence, an optimal value is set to overcome this.

## Concluding with More to Explore
The *timeslice* allocation is done by the process scheduler in a relative way proportional to the number of processes running in the system. This has a bit deeper explanation of why this has been implemented and why this optimises the resource allocation. Explaining that would take another article and is out of the scope of this one.

Understanding *Process Scheduling* in the Linux Kernel is an important path to understanding the working and philosophies of it.
