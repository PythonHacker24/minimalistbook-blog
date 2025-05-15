+++
category = "technical"
title = "Tmux is the Ultimate Choice for Power Users - An Awesome Terminal Multiplexer for Managing Persistent Sessions"
date = 2024-05-27
+++

## What is Tmux?

Tmux is a Terminal Multiplexer Application for Linux and MacOS for managing terminal sessions and Windows. It is to be mentioned that Tmux is not a terminal emulator, instead, it’s a terminal application, a binary that allows you to stay productive over your terminal. It doesn’t matter which terminal emulator you are using (although I recommend the Suckless Terminal). The functionality of managing Windows and the session doesn’t happen on the desktop GUI side but on the terminal session, you are working with. 

Tmux is Free and Open Source Software and its source code is available at its Official GitHub Repository: https://github.com/tmux/tmux 

Readers of my articles know how much I love Open Source and Free Software and this one is one of my favourite terminal applications.

## Why do You Need Tmux?

One thing about Tmux that I would like to mention is that Tmux is highly productive and you just need some amount of patience to learn it. 

Terminal Emulators are great, they can manage a lot of things like splitting panes and tabs, which Tmux also does by default. For instance, I use the Suckless Terminal with DWM (Dynamic Window Manager) which is a tiling window manager that allows me to have screen layout split into patterns that I prefer depending upon my work and have multiple workspaces mimicking as tabs on my system for the terminal emulators. In the past, I used to work with Terminator which is a graphical-based terminal emulator and had a decent amount of functionalities where windows were split and tabs were created inside one whole application. The GNOME terminal also supports the same and gets these basic jobs done. 

Tmux on the other hand works in a different way. Tmux runs on the terminal emulator and performs these operations on the TUI itself. So it doesn’t matter which terminal application you use, Tmux is going to work in the same way. When you split the screen, it’s not the GUI of the Terminal (like in GNOME terminals) where it’s going to split graphically. It would be splitting the terminal space in that terminal session. 

It might sound a bit confusing in the beginning but is easy when you use it. Let me put it like a story: 

When you open a terminal emulator on a desktop environment, it runs as a GUI and starts a terminal session with the underlying operating system. All the stuff you work in here is gone into the terminal session and is confined inside it. 

When you split the terminal, a new session is created which is different from the session it was in that prompt. It’s a “different terminal session”. The same goes with the tabs, when you open a new tab, a new terminal session is spawned. 

In the case of Tmux, when you open a GUI terminal, you get that one terminal session to work on. When you start a Tmux session inside it, all the tabs and windows are packed into that tmux session which is running on the same terminal session. Hence, you would be controlling a lot of prompts inside the same terminal session. All the creation of tabs and windows would be happening inside the tmux session which was inside that terminal session. 

Now if somehow your terminal crashes or gets closed by mistake, the terminal session is lost and all the history or temporary environment variables disappear. But if you were working in the Tmux session, that Tmux session can be restored in any other terminal session as well. 

You can have multiple terminal sessions running and you can access the Tmux session from all of them at once. So even if one of the terminal sessions is closed, the underlying Tmux session doesn’t stop and can be restored.

## Tmux for Linux Administration

Linux Administrators connect to servers remotely, commonly via SSH (Secure Shell). Working with a shell that is connected to a server with a network can be fragile. And you get disconnected with the shell, all the work that wasn’t saved or history can get destroyed. Tmux provides a persistent session here with a lot of other functionalities. 

When you log into a server, if you start a Tmux Session and start working on it, then that session is stored in the server while it’s running, even if the SSH is logged out. And you are allowed to create multiple Tmux sessions if you want! All those sessions would be restored even if get accidentally disconnected from the server, saving your precious work done on that session. 

Furthermore, when you spilt screens in terminal emulators, it happens on the client side. So when you are connected to a server and you need to do multiple things on different panes, you need to log in again on that split terminal (remember, the split terminal is a new terminal session, in this case on the client side only). But with Tmux when you split the screen, it’s split on the server side and you would see a split terminal on the client side in the same session of the terminal, without any interaction with the client’s terminal. The same goes with tabs, they are created on the server side with Tmux. And even when you disconnect from the server, all the Tmux sessions, tabs and windows are saved!

This makes Tmux one of the best tools for Linux Administration purposes and when you are working remotely with servers. 

## Tmux for Personal Computers 

As good as remote servers, Tmux works like a charm with productive setups on your personal computers. All the good things listed above are as important in Personal Computers too. Creating tabs, and sessions and splitting windows with persistent and redundant sessions come in handy while immersing in the work. 

When you are working with the terminal all the time (like Vim users), persistent sessions are important in case of disruptions like the terminal crashing or accidentally closing the terminal application. Everything in Tmux is stored as it was before it was detached. 

And learning Tmux has an advantage too. Tmux doesn’t care which terminal emulator has been used. So even if you are working on different terminal emulators, say you are a Kitty user shifted to Alacritty, the binding of Tmux would be as per your configurations and would not change. And when you are good with Tmux, your server administration skills will boost up too. When you are conceptually clear with Tmux and have the habits of key bindings, the terminal session on the servers will be as productive as it is on your personal computers. 

I recommend creating an automated script for these cases. For instance, if you need to constantly monitor CPU usage and Memory utilisation on the server while you work, Tmux widgets can be useful to do so. So you can develop a script, which when run on the remote server, installs and configures Tmux in that way in one command. 

## Installing Tmux 

Installing Tmux for different depending upon the Operating System, few of them are listed below (you can install it with your package manager):

### Debain Based Distros 
```bash 
sudo apt update
sudo apt install tmux
```
### Red Hat-based Distros 

```bash 
sudo yum install tmux
```
### Fedora Based Distros
```bash 
sudo dnf install tmux
```
### Arch Linux Based Distros
```bash 
sudo pacman -S tmux
```
### OpenSUSE 
```bash 
sudo zypper install tmux
```
### Gentoo Linux 
```bash 
emerge tmux
```
### MacOS 
```bash 
brew install tmux
``` 
### Installing from Source (Unix Like Distros)

### Installing Dependencies
(Listing for Debain, same can be done with different package managers on different distros)

```bash 
sudo apt update
sudo apt install -y build-essential libevent-dev libncurses-dev
```
#### Downloading the Source Code 
```bash 
wget https://github.com/tmux/tmux/releases/download/3.3a/tmux-3.3a.tar.gz
tar -xvzf tmux-3.3a.tar.gz
cd tmux-3.3a
```
#### Compile and Install 
```bash 
./configure
make
sudo make install
```
Refer the Official Tmux Wiki for more information or Troubleshooting: https://github.com/tmux/tmux/wiki

## Tmux Plugins - The Tmux Plugin Manager

Tmux supports a variety of plugins, which is made easy by the TPM (Tmux Plugin Manager) which allows you to manage your tmux plugins in a better way. Installing TPM is simple, use the following command to download TPM and just add the following line to your tmux.conf file (if it doesn’t exist, create one).

```bash 
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

```config 
set -g @plugin 'tmux-plugins/tpm'

# Plugins here 

# At the end
run '~/.tmux/plugins/tpm/tpm'
```

Finally, run: 
```bash 
tmux source ~/.tmux.conf
```
After this, you are ready to install any plugin of your choice. A few plugins that I use will be listed in the next section where you can understand how to install plugins via TPM.

## Example of Tmux Usage - How I Use it and My Config Files 

I use Tmux on my main Debian Machine and my Macbook all the time. My usual workspace is Tmux + NeoVim for both of my machines (and Tmux looks like a tiling window manager, just like DWM). Although, I use some plugins to make my Tmux beautiful and add some more features. Also, I use my custom bindings as per my requirements. 

![tmux](https://github.com/PythonHacker24/theminimalistbook/blob/main/static/tmux_screenshot.png?raw=true)

This is my Tmux configuration file:

```config 
unbind r 
bind r source-file ~/.tmux.conf

set -g prefix C-s 
set -g status-position top

set -g status-position top

# Vim Bindings 
setw -g mode-keys vi 
bind-key h select-pane -L 
bind-key j select-pane -D 
bind-key k select-pane -U 
bind-key l select-pane -R

# List of plugins 
set -g @plugin 'tmux-plugins/tpm'
set -g @plugin 'dracula/tmux'

set -g @dracula-plugins "cpu-usage ram-usage battery time"
set -g @dracula-show-powerline true
set -g @dracula-show-left-icon window
set -g @dracula-battery-label "Battery"
set -g @dracula-git-show-current-symbol ✓
set -g @dracula-time-format "%T"

# Initialize TMUX plugin manager (keep this line at the very bottom of tmux.conf)
run '~/.tmux/plugins/tpm/tpm'
```
I am using the dracula tmux colorscheme which is dark with optimal contrast to make tmux took awesome. Dracula supports a lot of other features like monitoring various things, like for me, the CPU, Memory and Battery (for Laptop) and a few other configurations.

Dracula Theme Official Page: https://draculatheme.com/tmux  

Configuring Dracula is super easy and is well documented on the Official Page. 

Here, I am using NeoVim on MacOS and I will be posting articles on NeoVim in the future about how to configure it and use it for maximum developer productivity. 
