+++
category = "technical"
title = "Configuring and Building the Linux Kernel — Absolute Guide to Compiling Your Kernel"
date = 2024-01-25
+++

Linux Kernel is an Open-Source Software and the user is free to modify and customise it as per the requirements. The modification of the Kernel requires a deep understanding of the working of the Kernel, although patches are available to make the Kernel optimised for specific hardware. Linux Kernel Source Code has various options to configure the drivers, modules, preferences on hardware options, etc. This part can be studied by the user and is pretty much easy to work with. The confusing part, however, is building the Kernel.

Building the Kernel includes creating user-specific configurations, and modifications as well as building in a way that is most efficient and error-free. It’s comforting for the fact that you can get the default configuration and build the Kernel over it in the simplest manner. But this approach lacks the freedom that you have over the clone of the code you own. For the most efficient build of the Kernel, you need to understand all the nuts and bolds of how to build the finest version of your Kernel. (if you are particularly a computer nerd, then you will be proud of the fact that you have your version of the Kernel).

The idea of building the Kernel is to create the `.config` file and compile it to the reference of this file. This file instructs the compilation process to build the Kernel as per the configuration in this file. There are various methods to create this file, ranging from the most configurable to the fastest way to get it done.

## Configuring from Scratch

The most basic method for configuring the Kernel is to use the make config method. This way, the Kernel will prompt you to set up every single configuration as per your wish and you need to fill in all the prompts to create the configuration file which you would need to build the kernel.

1. y: Build directly into the Kernel
2. m: Leave entirely out of the Kernel
3. m: Build as a module, to be loaded if needed
4. ?: Print a brief descriptive message and repeat the prompt

The fact that the Kernel has over 2000 options makes this process tedious. For users who need the most basic configuration and also have it quite a bit stable can use the default configuration file.

## Default Configuration Options
Linux Kernel also ships with a default configuration which is loosely based on the defaults that the Kernel Maintainer has. For the i386 architecture, this configuration matches close to what Linus Torvalds uses on his main development machine. This is a quick way to create a config file and get the Linux Kernel Build in the least time possible (and the fact that maintainers use them makes the config relatively stable for most of the users).

```bash 
cd linux-<kernel_version>
make defconfig
```

Now **this is a recommended build option** even if you want to create your custom Kernel. This method creates a base configuration file that you can modify to add or remove features as per the requirements. This way, you don’t need to worry about each option and have the freedom to skip any section that you want to be the default. So consider it to be the first step of Kernel customisation.

## Modifying the Kernel Configuration
The Kernel Configuration can be done in various ways, all resulting in the creation of the config file for building the Kernel itself. There are three ways of configuring the Kernel:

1. A **Terminal-based** one called **menuconfig**: `make menuconfig`
2. A **GTK+ based** graphical one called **gconfig**: `make gconfig`
3. A **QT-based** graphical one called **xconfig**: `make xconfig`

All of them do the same job and it’s the user’s preference to choose one method that is the most comfortable and create the config file. All the options would create a visual way of modifying the options which is comfortable and sorted logically. This way, every option can be found easily and modified as per the requirements.

Building the Kernel
Now building the Kernel in the most basic way is to just enter a one-word command: **make**

This will build the whole Linux Kernel with the provided configurations This will create the Kernel Image once the build is completed. Note that this image needs to be configured with the Linux Distro you are using before trying to boot from it.

## Advanced Building Options for the Kernel

The Kernel Source Code is a big file and needs resources to be compiled. Using the full potential of your system to build the Kernel will boost up the compiling process. To use all the cores of your system, you can provide the -j tag with the make command.

`make -j<number_of_cpu_cores>`

For example, if you have 6 cores CPU, then use the command `make -j6` to use all the 6 cores to compile the Kernel.

To find out the number of CPU cores in Linux, use the command: `nproc`.

So overall, to make use of all CPU cores, you can use the command:

`make -j$(nproc)`

## Building only a Portion of the Kernel
If you only want to build a portion of the Kernel, for example for drivers/usb/serial, you can use the command:

`make drivers/usb/serial` (but this will not build the final module images)

To build the final module images, use the command:

`make M=drivers/usb/serial`

To link the module image to the built Kernel, you have to use the `make` command again to add it to the final Kernel Image.

## Output to Another Folder
To output the contents of compiled files to another location, use the command: `make O=<location_of_output>`. This can be useful when installation is done via CD/ROM and is read-only for any purposes where the compiled image needs to be placed in some other location.

## Building for Different Architectures
Linux Kernel allows you to compile the image of other architectures. This is useful for embedded devices as well as to use powerful computers to compile Kernels for small devices. To do this, use the command:

`make ARCH=x86_64 defconfig` This will create configurations for an x86–64 architecture.

You can use CROSS_COMPILE options to use other architectures toolchain. For example, the ARM toolchain located in /usr/local/bin:

`make ARCH=arm CROSS_COMPILE=/usr/local/bin/arm-linux-`

To use programs like distcc or ccache (to change the build system used by the compiler), which helps to reduce the compile time significantly, use the CC option.

`make CC="ccache gcc"`

To use distcc and ccache together:

`make CC="ccache distcc"`

## Conclusion
Building your own Linux Kernel gives you the freedom to configure the system to the roots. Optimisation of Kernel can result in improved performance as well as help you understand the depths of computers. For learning more in-depth, I can recommend a few books:

Linux Kernel in a Nutshell — Greg Kroah-Hartman
Linux Kernel Development — Robert Love
