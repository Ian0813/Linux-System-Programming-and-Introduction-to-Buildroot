**How do we create a rootfs?**

    * Start by creating a folder tree (MELP uses ~/rootfs, we'll use a script argument)

        $ mkdir ~/rootfs 

        $ cd ~/rootfs

        $ mkdir bin dev etc home lib proc sbin sys tmp usr var 

        $ mkdir -p usr/bin /usr/lib usr/sbin var/log

    **Why use root as owner?**

        * Your user account doesn't exist on the system we are creating

            * Note: you need to be sudo root to run this command

**What about the files?**

    * Now we've got tthe filesystem structure, where do we get tje files we need to fill it?

    * User BusyBox 

    * Single binary that implements essential Linux programs

    * Symbolic links are used to tell which prgrams is being requested

    Example:
        /bin/cat -> /bin/busybox/

        It is a symbolic link point to where the program is located.
