===========================
Linux System Initialization
===========================


.. contents:: Outline

Learning objectives
~~~~~~~~~~~~~~~~~~~

 * Overview of GDB command line 

 - Using Remote GDB 


Debugging
~~~~~~~~~

 * Use -g argument to GCC for debug symbols 

 - Use -O0 to disable optimizations if needed

  - Improves single stepping experience  


GDB Commands
~~~~~~~~~~~~

 * r<args>-run 

 - b - set breakpoint 

 * p - print variable name 

 - n - step over next statement  

 * finish - step out of function 

 - info b - list breakpoints

 * delete <x> - delete breakpoints

 - bt = Backtrace

 * Reference [2]_
  

Remote GDB
~~~~~~~~~~

 * Whar about when we have a problem which exists on the target only? 

   - BR2_PACKAGE_HOST_GDB 

   * BR2_PACKAGE_GDB

   - BR2_PACKAGE_GDB_SERVER

   * Build image with required GDB packages and host tools

   .. figure:: remote_gdb_1.png 
      :width: 350 pt 

   * On the target, pick an unused port, start gdbserver and the application 

   .. figure:: remote_gdb_2.png 
      :width: 350 pt

   - On bulidroot, start cross gdb 

   * Setup for remote debug on same port specified to gdbserver


Remote GDB with Buildroot
~~~~~~~~~~~~~~~~~~~~~~~~~

 * The cross debugger is in buildroot/output/host/bin

 - Reference [3]_


.. figure:: remote_gdb_buildroot.png
   :width: 500pt



start-stop-daemon
~~~~~~~~~~~~~~~~~

 * init scripts should use start-stop-daemon 

  - Starts with -S (if the daemon doesn't exist) 

  * Sends SIGTERM with -K

 - See Week4 content for notes about how to write the daemon [1]_


Manually start and stop your script
-----------------------------------

 * /etc/init.d/Smydaemon start

 - /etc/init.d/Smydaemon stop

---------------------------------------------------------------------------

.. [1] start-stop-daemon man page 

 - https://man7.org/linux/man-pages/man8/start-stop-daemon.8.html

.. [2] GDB  

 - https://www.gnu.org/savannah-checkouts/gnu/gdb/index.html

.. [3] Buildroot advanced usage

 - https://buildroot.org/downloads/manual/manual.html#_advanced_usage 
