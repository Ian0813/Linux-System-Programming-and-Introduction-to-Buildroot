==========================================================
Writing Signal Handlers and Signale Handler and Reentrancy
==========================================================

.. contents:: Outline 

Signal Management
~~~~~~~~~~~~~~~~~

* POSIX in Linux 

 * signal (deprecated) 

 - sigaction (in use) [1]_

- sigaction signal handling

 * POSIX alternative (not part of the original std C library)  

 - Better signal management capabilities

  * Block new signals during handler

  - Retrieve state information 

  * Only need to setup sa_handler in sigaction in simple cases


Waiting for signals
~~~~~~~~~~~~~~~~~~~

* pause() waits for a signal   

Sending signals
~~~~~~~~~~~~~~~

* kill() sends a signal to a process 

 * Sends any signal, not just SIGKILL 

- Available as system call or user command

sigaction signal handling
~~~~~~~~~~~~~~~~~~~~~~~~~

* signal handling 

 * Ctrl->C sends SIGINT

 - Restart

 * Find process PID

 - Send TERM 

 * Process exits 

- Source code [2]_

Additional Signal Concepts
~~~~~~~~~~~~~~~~~~~~~~~~~~

* Child inherits signal actions of the parent on fork

- Starting a processes with exec() resets all signals to default actions (other than those ignored by the parent)  

Signal Handlers and Safety
~~~~~~~~~~~~~~~~~~~~~~~~~~

* Signal handlers:

 * Suspend execution of a process

 - Jump to our signal handler function 

 * Not a thread switch or new thread - reuses the existing thread 

 - **What does this mean about the functions you can call in the signal handler?**

  * Must be \"async-signal-safe\" in Single Unix Specification parlance

  - Must be reentrant \*and\* block signals during any points which could cause inconsistencies [4]_

 * **How do I know if a POSIX function I'm calling in signal safe?**
   
  * Table of allowed functions - one in your book, more complete in reference [4]_

  - malloc, free, (or any function which may call these) stdio library functions (printf for instance) are generally not safe to call.

 - Reference [3]_


Signal Handlers and Reentrancy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Must not manipulate static data also used outside the signal handler (strsignal() or similar functions)  
* Should manipulate only stack-allocated data or data provided by the caller 

* Must not invoke any non-async-signal-safe function  

Signal Handler Best practices
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Minimize global data access

 * Confirm any access is async signal safe   

- Save/restore errno 

* Call an absolute minimum set of functions,  

 * Call only functions on an approved list of signal handler functions.

Why Use/Not USe Signals?
~~~~~~~~~~~~~~~~~~~~~~~~

* \"old, antiquated mechanism for kernel to user communication\" 

- However, we are forced to use them for many important notifications (especially termination).

* Signal safety problems are easy to introduce and diffcult to track down 

 * Handlers must be implemented carefully.


---------------------------------------------------------------------------

.. [1] signal and sigaction manpage

 * https://man7.org/linux/man-pages/man7/signal.7.html

 - https://man7.org/linux/man-pages/man2/sigaction.2.html

.. [2] signal_handler.c

 * https://github.com/cu-ecen-aeld/aesd-lectures/blob/master/lecture9/signal_handler.c

.. [3] Signal Handlers and Safety

 * https://pubs.opengroup.org/onlinepubs/9699919799/

 - book: Advanced Programming in the Unix Environment - 10.6 section

.. [4] signal-safe table

 * https://pubs.opengroup.org/onlinepubs/9699919799/functions/V2_chap02.html#tag_15_04_03_03
