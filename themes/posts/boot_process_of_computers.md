+++
category = "technical"
title = "Boot Process of Computers — A Learner’s Perspective Of Exploring the Depth of Computers"
date = 2024-01-15
+++

*Prior Clarifications: Here, I will be providing a philosophical explanation about the bootloaders and understanding them in a simple and as minimal way as possible. This is not supposed to be a manual for bootloader or provide any advice for experimenting over your live system. It’s my journey to understand computers (one of the most complex creations of mankind) and I will be stating my thoughts. Take it with a pinch of salt.*

I have been reading the book *“Linux in a Nutshell” by Ellen Siever, Stephen Figgins, Robert Love and Arnold Robbins* which I consider to be my Linux Handbook and an absolute recommendation to have around your desk. Being a handbook, it does not suppress the comprehensive explanation of the topics. I have been using Linux for a long time but I would not deny the fact that I have learnt a lot from this book itself. The recent learnings I had from this book is about the Bootloaders. While I was skimming over and exploring the source code of coreboot (https://coreboot.org/), I fell in love with the low levels of computers.

Artificial Intelligence, Blockchain Technologies, Machine Learning, etc. have been a lot famous these days. Back in the days when computers were new and there was a lot of access to the lower levels, people were a lot enthusiastic about the low levels of computers. Humans have a natural curiosity to explore the stuff they use and want to understand the principles behind why and how it works. In the current age of generative AI, modern developers I enthusiastic about understanding the mechanisms between Artificial Intelligence, Decentralised Technologies, etc. and topics like Bootloaders, Partition Tables, Microprocessor Designs, etc. have now become the heading of the textbook chapters. If you have been taking Computer Science, Electronics and Electrical Engineering Courses at your University, chances are you might be studying these topics, in a very theoretical way. At least I am right now while writing the blog.

The fact that the computers that we buy nowadays, like, for example, MacBooks, we find ourselves not accessing the GRUB menu or Bios of the computer very often. These things are now hidden from us, to make it user-friendly because a single boot process is a very complex thing in itself for an average person just opening the laptop to skim over the internet. We can’t see these things and hence we ignore it. Our natural curiosity to explore then never gets triggered. AI, on the other hand, is highly accessible to any person on the internet or cryptocurrency for transactions or investments is easily accessible. This triggers the natural tendency to explore them (which is good). Hence, the lower levels of computers go unnoticed and we often under-estimate the beauty of the process that goes under the hood.

*A programming language is low-level when its programs require attention to the irrelevant. — Alan Perlis (American computer scientist)*

A computer you own is in itself a world where everything is just as synchronised as our real world is. It’s a whole ecosystem of processes happening the a very controlled way each triggering a different process, just as the real world does. Mankind’s creation is condensed into these small boxes. The boot process, which I like to believe is the beginning of the chaotic behaviours of the world. Just like eyes in the morning after a long deep sleep. The screen gets the smooth blasts of colours and inputs ready to get an interaction from the real world. This is the exact thing that makes this thing so awesome that I spend most of my time in this world. The real world is very hard to understand, a whole branch called science is trying to resolve it. It’s a chaotic system where everything has no obligation to explain itself. Computers on the other hand are human developer machines where the system can be considered as a sequentially proceeding system.

The two major bootloaders are the LILO (Linux Loader) and the GRUB (Grand Unified Boot Loader). Modern Linux distributions use GRUB as their bootloader of choice due to its more user-friendly nature (it has a GUI). LILO on the other hand was used previously but there are no restrictions on using it today. I use GRUB on my Arch Linux Distro due to its simplicity.

The main function of the bootloader is to get the kernel image of the Operating System triggered (or even other bootloader triggered). Kernel is a program that works as a layer between the hardware and the software of the computer system. From my perspective, I believe that the kernel is something that provides an analogous explanation of the underlying hardware to the developer to make it easy for them to make complex logic run on it. Bootloaders like LILO and GRUB are capable of booting into other OS like Windows too, in case you are dual booting. Although Microsoft Windows use its bootloader, the GRUB or LILO would transfer the control to the Windows Bootloader. These bootloaders can be configured according to your preferences.

The very first sectors of a drive are considered to be the boot partitions, where the MBR (Master Boot Record) is present. This is a 512-byte code that is responsible for transferring the control to other complex software that will boot the system. When a computer is turned on and when the BIOS is initialised, the BIOS looks for MBR partitions on the Drives. A Drive with an MBR Partition is said to be bootable and hence would provide the way out to boot up the operating system. Once the MBR is triggered, it will point out the way to the LILO or GRUB where there would be a lot more options present due to no restrictions on the size of software (since the MBR is just 512 Bytes). This whole thing can be considered to be a chain of processes that carry out their specific task and pass on the control to other parts of the system. It’s the awakening of a computer, the world inside it is coming to light.

This was a philosophical perspective of learning the internals of computers in as depth as possible. Resources out there are capable of explaining them in-depth, but there are very few providing the reason to do so. It’s the beauty of complexity, compiled by simple and slow progressions made over a long time.

Some Useful Links:

Coreboot Website: https://coreboot.org/

Bootloader Wikipedia Page: https://en.wikipedia.org/wiki/Bootloader

GNU GRUB Official Website: https://www.gnu.org/software/grub/

LILO Bootloader: https://en.wikipedia.org/wiki/LILO_(bootloader)


