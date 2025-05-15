+++
category = "technical"
title = "Why More is Not Always Good in Terms of Software - Words on Cross Platform Utilities, Bash-ism, and POSIX Compliance. "
date = 2024-06-01
+++

***Preface:*** *This article is about my views on software compliance and cross-platform support, and reflects my opinions and experience with the subject. Your experience and opinions may vary, which I respect.*

## What I am Specifically Talking About? 

I am going to talk about the issues caused by non-compliant software and why more features are not always good, especially in the case of the upgrade of tools on a single platform. 

I have been a Linux User for a few years now, and there have been some wild experiences when I am working especially with cross-platform applications. This is usually when I work with deployments where I am using different Operating Systems or environments, and what I think must be done or must be followed to avoid this kind of issue. 

Software Compliance is a necessary component while developing tools and applications for different platforms. Here, I am not talking about widely different OS, like comparing Windows and Linux for software compliance, in which case we know that the Kernels are completely different, but about the ones that seem somewhat similar, but have some hidden strings attached that would disrupt your usage. 

I am going to provide a few examples related to Bash, which is a GNU utility and how it’s creating a sense of extra features for new users, who get comfortable with it and end up failing to use other platforms when needed and can’t figure out why. So if you are new to Linux user or have been suffering from this issue, or even if you don’t care about cross-platform applications since your work is not related to it, it’s an article based on a lot of information related to what GNU is going and where the POSIX side of compliance is going. There are going to be facts about a Bash and the SED utility, so even if you think that this is stupid, you still have some takeaways from reading this article. 

## Example of Bash-ism

Bash is an interactive shell, which is built by GNU and is the default in a lot of Linux distributions, including a lot of which new to Linux users try as their first Linux Distro. Even for me, Bash was the first shell used, while I was using Kali Linux which is built upon Debian, with its default shell Bash. So for me, Bash became a standard for using shells and writing shell scripts. 

Before proceeding, let me first state what POSIX compliance is, since it’s necessary to understand it before proceeding:

*POSIX compliance refers to adherence to the standards specified by POSIX (Portable Operating System Interface), which is a family of standards defined by the IEEE for maintaining compatibility between operating systems. These standards cover various aspects of operating system interfaces, including shell command languages, system calls, and utilities. The main goal of POSIX is to ensure that software written for one POSIX-compliant system can be easily ported to another without significant changes.*

Now Bash by default is not POSIX compliant, like its subset is POSIX Compliant, and all the things that were written for POSIX compliant scripts will run on Bash, but not vice-versa. If you try to run a shell script, which was particularly written on the Bash environment and runs perfectly on Bash Shells with features that only Bash had in itself, it would break on others, including POSIX complaint shells. Now this is an issue that would come when you are a new Linux user. 

When you are new to Linux and use distributions like Ubuntu, Mint, etc. you start with using Bash as your default shell. And you learn a lot of commands and manipulate them, tie them up to get something useful out of it and decide to write a shell script. That shell script with all those Bash-ism included in it would break on other shells, like the dash shell which is POSIX Compliant and doesn’t have those bash functionality. 

Don’t get me wrong while I give examples of Bash and Bash-ism, a lot of tools and utilities have this problem within them and cause the learning curve for newbies to get steeper once they realise this. This issue introduces inefficiency in work, even though they promise to get more efficient work by extended functionalities going out of compliance. 

Now proper acknowledgement of these additional features can help, assuming that the steep learning curve and lesser cross-compactible issues can be fixed by ever-changing the shell scripts written for bash can be modified or rewritten again for POSIX Compliant Shells (which is not, it would be too much tedious), still there the basic issue here. That is a lack of acknowledgement of these features. Let me give an example to clear this out.&&

The diff command is used to find the differences between two files and what’s less and more in two given files. It finds line by line what is the difference between both of them and is super useful in bash scripts to find the difference between two files or if a file has been updated. 

General Syntax (very basic usage): 
```bash
diff file1 file2 
```
Now let's say you want to find if interfaces and IP Addresses are updated with the ifconfig command. Now in normal usage terms, you can do something like: 

```bash 
ifconfig > intial_file 
```

When checking time comes, 


```bash
ifconfig > updated_file 

diff initial_file updated_file
```
And this will get the job done. And it’s okay with POSIX Complaint software Shells. 

But with Bash Shell, there is a feature called process substitutions. 

In this case, you will directly add outputs of commands into the diff command without creating a file. 

```bash 
ifconfig > initial_file
```
 
When checking time comes to check updates, 

```bash
diff <(ifconfig) initial_file
```

And this is an example of Bash-ism. This would break on POSIX Compliant shells, like dash which is at times symbolically linked with /bin/sh in a lot of Linux distributions. So this would work when you run it with bash. 

Now if you consider a situation with bash as your interactive shell but your /bin/bash is symbolically linked with the dash shell. Then if process substitutions work on your prompt of Bash, it would break when you write #!/bin/sh on the shell script and run it with ./script.sh. And if you don’t know what’s happening underlying these terms of dash and bash, it would take a lot of time to figure out what you are doing. 

And when you are new to Linux user and you start writing shell scripts, it’s unlikely that you would discover /bin/bash is linked with dash as a POSIX compliant shell to interpret your shell scripts but you are using bash as your shell where things like *process substitutions* work. 

And if you are using bash to interpret your scripts or /bin/sh is symbolically linked with /bin/bash, then that script would be working on your machine but would break in POSIX-compliant shells. So this Bash-ism would make you run your pre-written scripts on Bash only or if you are not familiar with this, on the same distro of Linux that you use while writing your scripts. 

Now Bash also has a POSIX-compliant version, that is accessible with the command 

```bash 
bash --posix 
```

But that’s not the default, and it’s unlikely that you would start using it if you are a new Linux user.

## GNU SED vs BSD SED 

This is an example of different versions of utilities of two different Operating Systems. As you might know, the GNU/Linux term comes with the fact that Linux is the underlying kernel and GNU makes the utilities for that Operating System. BSD stands for the Berkley Software Distribution which has its own Unix-like operating System. Both have the SED command, which stands for stream editor used for editing text files in the shell. 

Now Linux has its own SED developed by GNU and BSD has its own BSD SED. Now it doesn’t matter if you are using bash, dash or any other shells, if functionality of SED for GNU-based OS is used, it would break on the BSD version. Now that the shell script works on shell-like ZSH or Bash, it would break on the same shell on the BSD variant. 

For example, let’s consider the very basic usage of SED, replacing words. 

```bash 
sed ‘s/example/EXAMPLE’ file.txt
```

This will replace the word “example” with “EXAMPLE” in the file.txt file. 

Now if you want to create a backup file before you make any edits, you need to do the following in GNU SED 


```bash 
sed -i.bak ‘s/example/EXAMPLE’ file.txt
```

But on BSD SED

```bash 
sed -i .bak ‘s/example/EXAMPLE’ file.txt
```

Notice that the whitespace between -i and .bak is in BSD SED while there is no whitespace in the case of GNU SED. 

So no matter what shell you use, or if it’s POSIX compliant, or the same tool for both software, it’s going to break down. 

And if you are unaware of this, you would eventually spend a lot of time fixing this and realising this, while they are the same tools in the same shell. 


## Problems Created by Non-Compliant Software 

So if you have read the above sections, it’s pretty evident that you have understood the issues with non-compliant software. Practically, they end up breaking a lot of stuff and cause a waste of time if you don’t know about this. 

Now let me state a practical fact here, there are very few people who would read the whole thing before using a tool. If you are using SED for just substitution, it’s unlikely that you would consider reading the whole man page for SED just to understand. You would think that it just works and gets the job done. Time saved. So acknowledgement of tiny changes like this would go unnoticed even if it is there. And it’s not the case for all of them. Some tools would be similar for a lot of distros but some would be different. It’s pretty time-consuming to read every tiny bit of all the tools for all the platforms. That’s something practically evident, even if ideally it’s recommended to read the manual of a tool before using it. 

So if you understand practically what is happening here, you would understand how these non-compliant software, even if they extend their functionality and make it somewhat more friendly, is adding hurdles when it comes to new Linux users (or experienced professionals too. That’s because it’s a fact that most of us learned Linux with intuition rather than scrolling on man pages and documentations). 

## My Opinion on Software Compliance

Now since a lot of us have been using Linux based on our learning through intuitions and reading man pages as well as documentation on the go when we need to understand all the features of a tool, which is not always the case, non-compliant software makes us bound to the existing environment. It’s somewhere causing the Linux Learning curve to become steeper than it should be and making it kind of obligatory to meticulously go through the docs of the same tools for different platforms, making the acknowledgement issue to become important. 

I think compliant tools are a viable solution here and even if additional functionalities need to be introduced, they must be done by switching extra buttons rather than making them default. This would help beginner Linux users to learn things that are valid cross-platform and further move on to use those extra features by turning on those utilities and going non-compliant. Having the base and default features to be compliant with various platforms will also solve the acknowledgement issues since users going out of the compliant way would mention it beforehand. 

So for shell scripting, I can recommend this. These are the list of fully POSIX complaint shells. 

1. dash (Debian Almquist shell)
2. ksh (Korn shell)
3. mksh (MirBSD Korn shell)
4. pdksh (Public Domain Korn shell)

So while you write scripts, use these shells to execute the scripts. This will make your scripts POSIX compliant. Meanwhile, you can use any shell, like Zsh or Bash which support POSIX compliant scripts, providing extra features which you can leverage as an interactive shell. This will force you to write scripts with POSIX compliant methods which would be cross-platform, which would run perfectly on POSIX compliant shells and also ones that support POSIX compliant and go beyond it to extend there funtionalilities. 


Again, this is my opinion on the topic and is the best of my knowledge in this regard. Your opinions and solution to the problem might be different and I respect that. 

