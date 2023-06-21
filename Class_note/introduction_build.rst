**Learning objectives**

 * **Build System Overview**
 * **Buildroot Overview**


**Linux Components**

 * Toolchain
 * bootloader 
 * kernel
 * root filesystem

**What makes a Build System?**

 * How are you going to generate these?

 * Options

  * Buildroot, Yocto, OpenWRT  
  * Roll Your Own(RYO)
  * Existing distribution (debian, Ubuntu, etc)


**Why use a Build System over RYO?**

 * Why reinvent the wheel?
 * Is there really something so specific about your project that means you can't leverage significant protions from other projects?
 * What is your strategy for keeping up with security patches?

**Build System vs Distribution**

 * Reducing the image size may challenging

 * Likely needs customization work to generate a producation image

 * Binary compatibility on different upgrade paths (v1->v3 vs v1->v2->v3) may be challenging


**Steps Perfromed by a Build System**

 * Download source for common package from upstream
 * Apply patches for cross compilation, arch dependent bugs, etc
 * Build components
 * Assemble rootfs in staging area
 * Create image files

**Other Build System Features**

 * Add your own packages (applications or drivers)

  * Often using proprietary license for some/all of these

 * Select system profiles

  * with/without graphics

 * Track open source license used

  * Help with open source license compliance 

**What is Buildroot?**

 * Builder of root filesystems for embedded devices
 * Collection of Linux packages with build instructions

  * Host and target packages

 * Started in 2001
 * Focuses on simplicity
 * Build system is licensed GPLv2 

  * You are expected to share changes to Buildroot source 

 * Leverages popular and ubiquitous make files and kconfig/menuconfig  

  * Same configuration mechanism used with the Linux kernel, busybox, ct-ng

**Installing Buildroot**

 * Based on GNU make and utilities
 * Need a collection of packages, most of which you already probably have installed.  

  * https://buildroot.org/downloads/manual/manual.html#requirement-mandatory

 * Also suggect ncurses (libncurses5-dev)

**Buildroot Packages**

 * Buildroot uses "packages" with build and install instructions utilizing GNU Make syntax

 * By default these packages are located directly in the buildroot tree for package builds, what Buildroot calls "br2-external" trees 

 * Why might it make sense to use an external tree?

  * For packages you can't share upstream (proprietary license])
 
 * Packages can reference git repositories for source code 

  * Build your own custom applications from your own dedicated repositories   

 * Packages need at least two files: 

  * Config.in - KConfig code adding the package to the config menu 

  * <package_name>.mk 

 * Buildroot Package definitions do not contain code 

  * Instead, they contain instructions to get code, compile, and add to rootfs

  



**Reference**

* 4 tools for building embedded Linux systems

  - https://opensource.com/article/18/6/embedded-linux-build-toolsu

* Buildroot Custom

  - https://buildroot.org/downloads/manual/manual.html#outside-br-custom 

* Adding packages

  - https://buildroot.org/downloads/manual/manual.html#adding-packages 
