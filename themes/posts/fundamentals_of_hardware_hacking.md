+++
category = "technical"
title = "The Fundamentals of Hardware Hacking — Breaking and Reverse Engineering Smart IoT Devices"
date = 2024-03-15
+++

*<strong>Disclaimer —</strong> This is an introductory article about Hardware Hacking and Security of IoT Devices. None of the mentioned information or techniques are intended for any illegal purposes and the author is not responsible for any damage. It’s advisable to experiment on devices that you own or have explicit permission to do so. Rest of all, hardware hacking is fun!*

## The Beauty of Electronic Devices

In the ever-growing world of smart devices and the connectivity of things to the internet, life has become more convenient than ever. Advancements in electronics and microprocessors unlocked infinite potential for developing devices that have become basic needs to survive the economy. Homes and cars became smart enough to make decisions as well as make suggestions to the user. Things that were supposed to be in fantasy books are now absolute essentials of every day. Anything less than that is considered to be outdated or underdeveloped.

Behind these devices possessing these functionalities are circuit boards that house all of the components that work together to make each functionality happen. With the entry point of the power supply where electrons are introduced, millions of active and passive components manipulate the flow of electrons to make the pipeline of wires behave in a certain way.

This flow of electrons which affect the physical behaviors in a certain way to make a functionality happen is nothing less than a miracle of the human brain.

But to make mistakes is called being a human being. Since these devices are just implementations of human minds, they end up containing some sort of mistakes, that hackers like us hunt for.

*<strong>It’s human to make mistakes and some of us are more human than others. — Ashleigh Brilliant</strong>*

## Hardware Hacking — Deviating that one Electron
Electronic devices are circuits that create rules about how electrons must flow to cause a certain logic to execute and interact with the physical world in the way it is intended to do. Since these electrons do follow these rules to flow, in the case when the rules are manipulated, they can do much more than they were designed to do by the manufacturer.

*<strong>To hack a system requires getting to know its rules better than the people who created it or are running it. — Permanent Record (Book by Edward Snowden)</strong>*

## Manipulating the flow of current, or logic in an electronic circuit, at any level of abstraction, rather be the kernel or physical component is called hardware hacking.

Understanding the rules of electronics is absolutely essential before trying to exploit them.

The Layers inside Electronic Devices
An electronic circuit comprises various abstraction layers, developed by humans to better understand the logical structures of the design. Developing the whole functionality of hardware devices just by connecting components is not feasible and certainly not the best way to do the job. The tasks of developing a device are distributed in various sections. The software layer and Hardware layer are the highest levels of classifications.

The lowest element in the stack is the hardware layer. This comprises physical components that are responsible for manipulating the flow of electrons in the circuit. This includes active and passive components like resistors, capacitors, inductors, microprocessors, transistors, MOSFETs, storage devices like EEPROMs, etc. These are all the physical elements in an electronic circuit.

To make sense of millions of components in the circuit, various protocols and standards are defined. An EEPROM can read and write data into it on specific instructions. These instructions are just fluctuations in the current to a certain pin that is defined by some protocol which would be considered as a valid input to the device. Being a valid input, the rest of the process happens inside the packaging of the EEPROM. Which is again a set of logic that would be triggered on a valid input.

These logics are combined into certain rules and standards that further become the software layer of that device. This layer is all about the implications of abstract logic to make certain things happen. These certain things, designed carefully constitute functionalities that the users of that device expect.

The sole purpose of developing circuits in this way is to make them more understandable and universal. Standards and Protocols are being developed that are used to develop them that make them more understandable and become cross-platform.

## Approach to Hardware Hacking and Electronic Devices Security
Approaching and Hardware Device for hunting security issues works in two ways (or often simultaneously).

One is to hunt on the hardware level. Another is to go with the software level. Combine them in necessary situations and you get to understand the relation between the hardware component or certain flow of current in a wire with the software logic defined.

At the hardware level, analyzing for logic in the current flow and values of various parameters is a good start. Certainly, it’s not always about understanding the whole circuit diagram (although it helps in complicated cases. It settles down to knowledge and past experiences of which component is most likely to cause an issue.

At this point in the hardware level, it’s mostly about measurements of parameters in various conditions and states of functionalities.

At the software level, it usually goes with firmware analysis. It goes somewhere close to software security, where the flow of programs is manipulated to cause certain behaviors.

The major difference between application security and hardware security is the dependence on the underlying hardware layer and the code execution. In application security, the hardware underlying the software is not a major influencer. Certainly not the electronic components underlying it. Processor architecture indeed matters in software development, but architecture design is just a set of logic and values of current and voltage that do not have much effect on code execution, at least for software developers.

Hardware Attacks like fault injection require hardware-level glitching (voltage dropping across certain components) to jump instructions at the software level. In this attack, the voltage level is dropped by a certain value at the precise time when an instruction is to be executed, causing the execution to not happen, and giving the attacker a way to bypass certain instructions constituting logic like authentication.

Side Channel Power Analysis is a good example of the relationship between software and hardware devices. Certain CPU instructions take more power than others and vice versa. The input power is measured at points to analyze which instruction is fetched and executed. This is particularly helpful for cryptographic operations analysis and extracting keys from the hardware.

## What does it take to be a Hardware Hacker?
Understanding electronic devices as well as software development is essential for hardware hacking.

Certainly, search engines are one of the best ways to make things happen! The internet is full of resources regarding hardware security.

As a starter, basic electronics and software development skills (embedded ones are more helpful) provide a good kickstart.

Remember, hardware hacking requires a lot of patience. Hacking physical devices incorporates imperfections from physical nature. Unlike application security where rules are perfect, the hardware side has errors and tolerance to them. Hence, it’s more about judgment and experience.

Additional Tip: Wireless Routers are one of the best ways to learn hardware hacking. Modern routers are a combination of wireless technology, web servers, authentication, networking, embedded development, storage mediums, etc. This provides a whole playground for experimenting with various attacks and learning along the way.

## Summing Up Everything
To hack into a system requires an understanding of the rules better than the designer. Hardware has a lot of it to adhere to. It’s awesome to think how many of these devices surround us and developing exploits on them can make a person with an understanding of them the one in control.

More of it: Since Blockchain Technology is on its way to making things smarter and financially capable, the space of hardware hacking is just getting pushed way more than ever before. When these smart devices get integrated with smart contracts, there is a lot more to do than just bypassing password authentication. It would go towards cryptography and finances. So more fun in the future!
