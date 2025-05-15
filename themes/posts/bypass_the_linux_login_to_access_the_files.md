+++
category = "technical"
title = "Bypassing the Linux Login to access the files (with Physical Access), even the root!"
date = 2024-01-08
+++

Imagine being away from the computer for a couple of minutes and getting to know that the system has been compromised and a backdoor has been installed into the system. “The system was locked?” doesn’t matter, without the bios security implementation (which most probably would not be implemented), all the files can be recovered without any login made to the Login Screen.

This goes with the story of me trying to get my Wi-Fi troubleshooting in Arch Linux where I was trying to upgrade the Kernel of my System to get the Wi-Fi working properly (as mentioned in the previous blog. By the way, I got the Wi-Fi working). I used an Arch Installation medium to get into the system and extract all my backup data into a USB.

Doing this is simple given that some physical access to the device is granted. By automating this process with a key-strokes injector, the process can be streamlined to most extent. Even backdoors can be planted in the system and run as background processes.

Now first, let me get the expectations of the line. This is not something very new thing that I have found. It’s just I found it with my way of exploring the computers and troubleshooting a Custom Arch Linux Build. So if the technique exists, great! the world remains as it is.

## Getting the Tools for the Action
What you need for a basic purpose is just a USB drive with some standard space on it (I expect that it is more than 8GB or something, would be good to have one). Just install Arch Installation medium into it.

- Get the image from the Arch Official Website
- Use Balena Etcher or anything you like to flash the image

Now you have an Arch Installation Medium, get to the system want to get access to.

For super fast action, get a USB Ducky or some microcontroller that you can manage to program for keystroke injections. You just have to record the exact command you want and you can pair them for maximum speed and avoid typing on the keyboard while the attack happens (be legit, only on devices you have permission).

## Hack the World! — Action Phase
Let’s call the Arch Installation Medium as Attacker USB for the sake of making this blog look cooler.

Plug that Attacker USB into the system and get the command line ready after login (the Attacker USB login, default ones)
At this point, you might need you connect the system to the internet in case you need to access the internet for uploading or downloading. [Command: iwctl station <interface> connect <SSID> ] and then Enter the Password for the internet.
Now mount the drives of the system to the Attacker USB. There are several steps for this so I am listing this after these bullet points (I am new to Medium while writing this so spare with me) [TAG: MOUNT_SECTION]
Now you can go to the /mnt and get access to all the files in it. I recommend chrooting into it and then exploring the files if there is enough time. This way, you can use the installed binaries and get things from the internet into the system. [Chrooting Command: arch-chroot /mnt /bin/bash]
[MOUNT_SECTION]: Here, I will show how to mount the drive to the USB Medium

Do lsblk and you will get the drives listed
They would be like /sda, /sdb and would have sub-drives like /sda1 and /sda2. Something like that (trust me, I am an Engineer)
With some common sense, I can safely say that the disk might be big enough like hundreds of GB, bigger than the USB I think so for most of the time.
Let’s say it’s sda for the drive you want to access.
First, make a boot file in the /mnt folder in the Attacker USB
- `mkdir /mnt/boot`
- `mount /dev/sda1 /mnt/boot`
- `mount /dev/sda2 /mnt`
Quick Disclaimer, it depends on the partition of the filesystem into the drive. The cases I have provided here are the most common ones found (by my experience)

## Post Exploitation
If you manage to get into the drives or chroot into it (would be awesome if this works), then that’s it. This is what it was all about. You got the files without any Login Screen asking for passwords. The files are compromised.

What I did in the case was, I looked for /etc/passwd and /etc/shadow files which I would have used with Hashcat to crack the login passwords. Now a remote backdoor can be set up by planting it to files that autostart and even trying to hide it to prevent the user from suspecting it.

Having an Access Point handy with a Keystroke Injector and Attacker USB can prove to have a very fast execution of the task given that the system is studied for automated attacks. Manual procedures work the best but take time.

This was it, my story of debugging the Wi-Fi and finding this technique to get access to my files. This methodology can be used for physical penetration tests or even to get out the files from a crashed system (like if the user deletes the /boot file and reboots)

**Disclaimer:** I am a very simple person studying computers and have some knowledge about them. Everything here is just for learning purposes and not for some shady purposes. Do it on your systems and systems you have permission to do this. Be careful, you may end up wiping the disk, so I as a simple author take no responsibility for any loss. I have a lot of things and problems to solve so would likely not engage in something like resolving issues. Have a good time learning!


