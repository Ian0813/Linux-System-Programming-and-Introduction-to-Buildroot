**Learning objectives**

 * Additional tips for using Buildroot and Completing Assignment 4

**dirname $0 trick**

 * $0 is full execution name, like /path/to/script.sh if you start using ./path/to/script.sh

 * dirname gives us /path/to

 * cd 'dirname $0' means change to the directory where the script is located

**Single Package Rebuild/Local Build**

 * Single Package Rebuild

  * USe make aesd-assignments-rebuild or aesd-assignments-reconfigure from buildroot directory 

 * Local builds

  * Use argument AESD_ASSIGMENTS_OVERRIDE_SRCDIR=/path/to/local

 * These save time! Use them!

  * Don't do a clean build each time you make a change 

**GNU screen**

 * What happens if you start the build from a terminal session and your session dies or is closed?

 * Build stops

 * Alternative: Setup a dedicated screen for your build 

  * screen -S buildroot-build
  * start the build
  * Ctrl+a d
  * To reconnect, screen -r build-root

**ssh_agent**

  * Build needs to start by installing toolchain

  * Will be a while before it tries to compile your package

  * Will stall there waiting for you to enter your SSH credentials for your key 

  * Instead use passwordless key or setup ssh-agent in your terminal session

    * eval \`ssh-agent\`
    * ssh-add ~/.ssh/yourprivatrkey

**QEMU ssh passthrough**

  * SSH - Secure Shell
  * Secure remote command line access
  * ssh user@ip-or-hostname
  * Default SSH port is TCP port 22
  * Our QEMU instance can't user this port (as it's in use by VM)
  * Need to modify runqemu script to forward port 10022 to our QEMU instance using hostfwd
  * Then connect ssh -p 10022 root@localhost
     
     - Use capital -P for scp command

**Buildroot Full Rebuilds**

  * it is the responsibility of the user to know when a full rebuild is necessary 

   * Target architecture/toolchain config changed some other fundamental configuration item

   * Package is reomved 

   * When package referencing other packages are added (in some cases) 

   * Package sub-options are changed 

  * Bottom line - ./clean.sh && ./build.sh is usually a troubleshooting step but don't use this for incremental changes to your package 

   * See single package rebuild/local build instrucations 

**Buildroot Output Directory**

  * The output/target directory contains the almost complete content which will make up your root filesystem.

   * Good for sanity checking whether things are placed where you think they are placed. 

   * Can delete files here which you moved/deleted in a package to avoid the need to full rebuild
 
**Reference**

 * dirname $0 trick

   - https://electrictoolbox.com/bash-script-directory/ 

 * make-tips

   - https://buildroot.org/downloads/manual/manual.html#make-tips 

 * screen usage

   - https://linuxize.com/post/how-to-use-linux-screen 

 * gnu make not support a file name with spaces

    - https://stackoverflow.com/questions/9838384/can-gnu-make-handle-filenames-with-spaces 

 * SSH - Secure Shell

    - https://mediatemple.net/community/products/dv/204403684/connecting-via-ssh-to-your-server

 * Buildroot Full Rebuilds

    - https://buildroot.org/downloads/manual/manual.html#full-rebuild 
