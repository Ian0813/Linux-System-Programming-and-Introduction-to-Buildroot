================================================================================================
Learning objectives: Introduce Signals, Understand default Signal handling, Introduce core files 
================================================================================================

.. contents:: Outline 

Signals
~~~~~~~

 * Software interrupts for handling asynchronous events: 

  * Events outside the system (Ctrl->C). 

  - Events from the program or kernel (divide by 0)

  * Interprocess Communication Method.

 * Event is asynchronous and handler is asynchronous

Signal lifecycle
~~~~~~~~~~~~~~~~

  * raised (sent or generated)

  - stored (by kernel)

  * handled by kernel, based on process request

Signal Handling Options
~~~~~~~~~~~~~~~~~~~~~~~

 * Ignore (except for SIGKILL and SIGSTOP)
  
 - Catch and handle
 
  * Suspend execution of the process
 
   * Including execution of other signal handlers
 
  - Jump to a previously registered function.
 
  * SIGINT and SIGTERM are two common examples.
 
 * Perform the default action 
 
  * Often terminates the process, possibly with core    dump (capture of running process memory) 


Signal Default Actions
~~~~~~~~~~~~~~~~~~~~~~

Term - SIGTERM

Ign  -  Ignore

Core - SIGTERM and dump core

Stop - SIGSTOP


Common Signal
~~~~~~~~~~~~~

 * SIGABRT - assert() - terminate & generates core files

 - SIGHUP - May be used to reread config files

 * SIGINT - Ctrl->C

 - SIGKILL - cannot be ignored, unconditionally terminate the process

 * SIGSEGV - Segmentation fault (null pointer, etc)

  - terminates and generates core file as default action 

 - SIGTERM - gracefully terminate a process

  - Process can catch and cleanup

 * SIGSTOP - Unconditionally pause (can't be ignored)


Experiment with the use of apport and core dump files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 * apport - A system service for automatic crash report generation 

 - core dump file - Produce it when a signal causes a process to terminate.

 Eample::

  int main ( void ) {
      int *mem = 0x0;
      *mem = *mem + 1;
      return 0;
  }
    



Reference [1]_.

.. figure:: image.png
   :width: 300pt

---------------------------------------------------------------------------

.. [1] apport and gdb debugger

- https://stackoverflow.com/questions/14204961/how-to-change-apport-default-behaviour-for-non-packaged-application-crashes 
