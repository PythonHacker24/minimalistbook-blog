+++
category = "technical"
title = "Operating Systems and Low-Level Access to the Hardware — Why should you learn it?"
date = 2024-01-09 
+++

Today, I completed the whole read of the book **“Linux Kernel in a Nutshell” by Greg Kroah-Hartman** and I highly recommend that you go through it if you want to understand how to build your custom configuration of Linux Kernel and all you need to know about all the nuts and bolts. It’s always great to have such handbooks around the desk.

This blog is about why it’s so awesome to look into the operating system you are using with your hardware and why have a grasp on the Low-Level aspects of a computer. I am going to go philosophical in this blog about the reasoning behind why to leave what you are doing and explore under the hood of things around you. When I say computers, it’s not bound to something like a Laptop or Desktop but comprises a whole lot of things that you have lying around. Like your Wireless Access Point (commonly called a wireless router), most probably it’s the case that it is running a whole Linux-based Operating System in it. Owning something might be easy but having an insight into how it functions is something amazing. When you spend a lot of time figuring out all of this, it becomes extremely obvious about how they work rather than the complexity that we predict while accessing these things.

*“The world is full of obvious things which nobody by any chance ever observes” — Sherlock Holmes"*


My last few blogs have been about why I use Arch Operating System. Today, I am not gonna state much about that fact (I use Arch btw). Recently, I was learning the **Rust Programming Language** which I consider to be one of my favourite languages. Yes, I love **Golang** too and I am learning it now. The control that these languages give you on the low-level side is so awesome that I got to learn about Stack Memory and Heap Memory from the Rust Docs itself. This makes you a better programmer than the traditional one trying to look into the syntax and goes on to use it blindly. The Rust Programming Language is now being used in the Linux Kernel which is awesome in a way. The C Language is from my perspective is what I respect a lot and trying to learn it in as depth as possible. **C Language** is something that gives so much control to the developer that the security falls into the hands of the developer. So I consider Rust as an ideal language for most purposes. More on Rust Language in some other blog, there is a lot to cover about that.

Now languages like Rust, Golang, C, etc. hand over the control of the hardware to a great extent to the developer. This means that the first layer that they are going to interact with is the Operating System. Modern devices comprise operating systems which makes them easier to develop rather than hardcoding the firmware from scratch (there are a lot of reasons why companies don’t prefer this much. One of them is building the Kernel from scratch which is a huge work to get done). Interacting with the Operating System and building native applications is I believe a huge advantage. Optimising a program for a specific OS works out well and helps avoid a lot of bugs. All of this comes when the developer has a keen knowledge of Operating Systems and Internal Hardware.

Having a grasp on Operating Systems makes it easy to decode the world of electronics. Like, consider my case. I remember I was trying to hack into my TP-LINK — WR720N by physical access. While I was plugging in the UART ports and trying to learn **Firmware Extraction Techniques**, I learned that it has Linux-based firmware. I use Linux on my Desktop Hardware which uses the same Kernel that the small Wireless Router was using. Isn’t it cool that while I know my operating system in depth, I understand my router as well? Almost the same principles apply to it, like the network management. Operating Systems have networking tools built into them for internet connectivity and networking is the core for Wireless Access Points. This makes the router more understandable while using it, and now you have more control over your devices.

It’s just the optimisations that are made while developing these devices. A Wireless Access Point has almost I believe no need for Keyboard and Mouse Interaction. So these drivers can be removed, which optimises the storage and results in greater speed. A functional Operating System on a Desktop would need this! it’s hard to work without a Keyboard (and sometimes a mouse but if you use NeoVim like me and CLI with Tmux most of the time, then it should be fine). Now consider that you are building a media server on your **Raspberry Pi** and you have SSH to interact with it. Why would you need a Printer and Scanner Drivers if you don’t use them? If you want an Ethernet connection, why go with Wi-Fi drivers? Make your system lightweight and fast enough.

These are some things that you would be able to optimise at low levels of your computers. Doesn’t matter if you are a High-Level Language user working on Web Application Development, having a good command of Low-Level can help you optimise your products. Personally, I like to explore the ecosystems of devices and make my Arch Distro faster for development.

Rust Docs: https://doc.rust-lang.org/book/title-page.html

Golang Docs: https://go.dev/doc/

Linux Wikipedia: https://en.wikipedia.org/wiki/Linux

Linux Kernel in a Nutshell Book (Author’s Website): http://www.kroah.com/lkn/
