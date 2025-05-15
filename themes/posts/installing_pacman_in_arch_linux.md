+++
category = "technical"
title = "Installing Pacman in Arch Linux — When You Blow it Up"
date = 2024-01-17
+++

Let me suckless and divide the article into two parts:

My story how I blew up Pacman Package Manager
How to reinstall the Pacman Package Manager
If you only care about the second part, skip the first one.

## The Scenario — Blow it Up

I was trying to install the pacman game from the Internet to get it running on my Arch Linux Terminal (I use Suckless Terminal BTW). When I got it installed and played it, it was super awesome. It was fun to the point that I decided to add it to my /usr/bin directory to make it my usual command and play it whenever I want. This is where I messed up and replaced the Pacman Package Manager binary with the Pacman Game binary. And now I ended up losing it and unable to update or install anything to my system and enabled me to play a Pacman Game.

Now when you are in a relaxed state and don’t have a broad angle of thinking what you are doing, you ending messing things up. And it may be a case happened to you too and you might too have blown you Pacman Package Manager by any reason (trust me, you messed up).

It is a 2 minutes solution which took me 2 hours to find out. I am including the steps here so that you can save your good time.

## Looking on the Brighter Side

The 2 hours went by where some of the good hours that Arch Linux gives you frequently. Last time, it was a Wi-Fi driver error due to outdated kernel which I documented in my other article. This is what I use Arch for: not just getting my system fast and make it the most custom tailored operating system ever, but also learning a lot of things through challenges like this. I actually love these challenges that come in my way to make me think valid approaches and tackle that problem.

I first thought of using pacstrap (which of course was not a command in my Arch Distro). To overcome this, I got my Arch Installation media (super useful to have: for installing Arch in new systems and debugging existing machines as well) ready, which is a 16GB USB. I plugged it in, used `iwctl` to connect to the Wi-Fi, mount the SSD with my Arch Linux with the commands `mkdir /mnt/boot`, `mount /dev/sda1` `/mnt/boot`, `mount /dev/sda2 /mnt` (mine was sda labelled). Then I pacstrapped it: `pacstrap /mnt base base-devel`. And it failed.

Then spent time with the the Arch Wiki (this takes the most amout of time) and got the whole git repo of Pacman Package Manager cloned in my system. Followed all the steps to get the meson build ready as well as ninja build and install. At last, didn’t work (it will work in the solutions part).

After this part, I did make it happen. It was just a small configuration of adding repositories to the configuration, from which the Arch Linux will install all of it’s tools.

## Solution to the Problem: Getting Pacman Package Manager Installed on the System

1. Get the Pacman Package Manager git repository cloned in your system `git clone https://gitlab.archlinux.org/pacman/pacman.git`
2. Get the Build and Install Procedures done :

- `$ meson build`
- `$ ninja -C build`
- `$ ninja -C build install`

3. Edit the pacman.conf file: File location: `/etc/pacman.conf`. Add these lines in the pacman.conf.

[core]
Include = /etc/pacman.d/mirrorlist

[extra]
Include = /etc/pacman.d/mirrorlist

[community]
Include = /etc/pacman.d/mirrorlist

4. Update the mirrorlist with the Official Arch Linux Mirrorlist Generator. Just selected the desired location and other settings. Then just copy and paste them in the file `/etc/pacman.d/mirrorlist`.

Arch Official Mirrorlist Generator: `https://archlinux.org/mirrorlist/`

And the Pacman Package Manager would run as expected with the command `pacman`. Try doing `pacman -Syu` which updates your system for testing it.

Official Webpage for Pacman: https://archlinux.org/pacman/

If still you Pacman Package Manager doesn’t work out, I am really sorry for your loss. You need to try harder to get it done. I would like to know if there are even more ways to solve this problem (or even things can go even more wrong). Although theoretically it must work by now, but in case if it doesn’t, happy solving the issue.
