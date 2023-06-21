===========================
Linux System Initialization
===========================


.. contents:: Outline

Learning objectives
~~~~~~~~~~~~~~~~~~~

 * Linux Initialization/Startup Manager Options

 - Basic of Linux Init Scripts

Initialization
~~~~~~~~~~~~~~

 * Busybox Init 

  - Default for buildroot

 - System V (System 5) init

  * Default for Yocto projects 

 * systemd

  - More sophisticated startup manager 


System V Init
~~~~~~~~~~~~~

 * 1980s era Unix system

 - Includes concept of runlevels

 * S runlevel = startup tasks

 - K runlevel = shoutdown

 * Levels 1-5 are defined as single/multi user
   modes with or without graphical login support

Init Scripts 
~~~~~~~~~~~~

 * In System V and Busybox cases, initialization is mostly driven with shell scripts

 - Busybox

   * /etc/init.d/rcS
   
   - S = startup runlevel

Busybox /etc/init.d scripts
~~~~~~~~~~~~~~~~~~~~~~~~~~~

 * Should support start and stop parameters

 - Typically handle these in a case statement 


.. figure:: Busybox_init_script.png 
   :width: 300pt


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

.. [2] Random facts: 

  - Emacs provides an rst mode 
  - when converting rst to html, a style sheet can be provided (there is a similar feature for latex)
  - rst can also be converted into XML
  - the recommended file extension for rst is ``.txt``

