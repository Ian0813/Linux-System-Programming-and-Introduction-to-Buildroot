===================
Sleeping and Timers
===================

.. contents:: Outline

Learning objectives
~~~~~~~~~~~~~~~~~~~

* Sleeping in your program 

- Alternatives to Sleeping

* Using Timers in your program
 
SLeeping
~~~~~~~~

* sleep(int seconds) [1]_

 * Returns number of seconds \*not\* slept
 
 - **Why would this function exit early?** 
 
  -  signals 

* usleep(int microseconds) [2]_

 * Sleep with microsecond precision \*at least\* usec

- nanosleep [3]_ 

 * Sleep with nanosecond precision

 - Returns remaining time in \*rem if interrupted

 * Supports absolute sleeping with TIMER_ABSTIME flag and absolute time in request

  * Can be used for more MEprecise sleep sequences.

  - Avoids inaccuracies in timing between clocl_gettime() and clock_nanosleep()  

 - What should I use for clock_type to measure duration?

  * **CLOCK_MONOTONIC** [4]_

 - Is clock_nanosleep less accurate? 

  * No all sleep functions are generally not accurate below 1ms on this system   

  - Add a 100 ms delay between clocl_gettime and actual sleep to show benefit of clock_nanosleep and TIME_ABSTIME

- Reference [5]_ 


Alternatives to Sleeping
~~~~~~~~~~~~~~~~~~~~~~~~

* Sleep is approriate for short (<1 sec) infrequent events

- Code that is laced with sleeps in order to \"busy-wait\" for events is usually of poor design. 

* Code that blocks on a file descriptor, allowing the kernel to handle the sleep and wake up the process, is better.

- Avoid the urge to use as band-aids for some poorly understood problem.

 * \"I got an error once, then I added a sleep and it disappeared.\"

* Consider using Timers instead.

Timers - alarm
~~~~~~~~~~~~~~

* Simplest interface

- Delivers SIGALRM to the process after seconds of time have expired

* SIGALRM can be sent outside the process 

- Reference [6]_

alarm concerns
~~~~~~~~~~~~~~

* Signal reentrancy limitations

- SIGALRM can be sent by sleep(), usleep(), setitimer()

* SIGALRM can be sent outside the process 

Timers - Internal Timers
~~~~~~~~~~~~~~~~~~~~~~~~

* Delivers SIGALRM to the process, optionally re-arming itself with it_interval after it_value

- Similar issues with signal handlers

Timers - POSIX timer
~~~~~~~~~~~~~~~~~~~~

* Use threads instead of signals with SIGEV_THREAD

- Adds support for TIMER_ABSTIME

* Reference [7]_

---------------------------------------------------------------------------

.. [1] POSIX sleep man page 

 https://linux.die.net/man/3/sleep

.. [2] POSIX usleep man page 

 https://linux.die.net/man/3/usleep

.. [3] POSIX nanosleep man page

 https://linux.die.net/man/3/nanosleep

.. [4] sleep sample code

 https://github.com/cu-ecen-aeld/aesd-lectures/blob/master/lecture9/sleep_functions.c 

.. [5] system cloce and hardware clock

 https://developer.toradex.com/software/linux-resources/linux-features/real-time-clock-rtc-linux/ 

 https://linuxconfig.org/system-clock-vs-hardware-clock-on-linux 

 https://linuxconfig.org/system-clock-vs-hardware-clock-on-linux

 https://stackoverflow.com/questions/427808/what-is-the-effect-of-changing-system-time-on-sleeping-threads

.. [6] alarm() man page and simple example

 https://linux.die.net/man/3/alarm

 https://github.com/cu-ecen-aeld/aesd-lectures/blob/master/lecture9/timer_simple.c

.. [7] Timers - POSIX timer_create()

 https://linux.die.net/man/3/timer_create 
 https://github.com/cu-ecen-aeld/aesd-lectures/blob/master/lecture9/timer_thread.c

