===============
Coursera - Time
===============

.. contents:: Outline 

Learning onjectives 
~~~~~~~~~~~~~~~~~~~

* Time measurement types and formats

- Clock Types

* Getting and Setting time


Linux Time Measurement Types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Wall time

- Process Time

* Monotonic time

Time Measurement - Wall time
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Actual time and date in the real world (clock)

- Useful for user interaction

  * What time is it now?

  - What time did something happen?

* Localized (timezone, daylight savings) 

- May be saved/restored using battery power and hardware support

* Updated with Network Time Protocol (NTP)

Linux Time Measurement Types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Process Time

 * Time spent executing on a processor

 - Can be less than wall time due to multitasking 

 * Can exceed wall time if running on multiple processors

- Monotonic time

 * Always increasing (system uptime) 

Linux Time Measurement
~~~~~~~~~~~~~~~~~~~~~~

* Relative Time

- Absolute Time


Relative Time Measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~

* Relative to some specific time (like now)

- 5 seconds from now, 10 minutes ago

* Typically use monotonic time

 * Changing time reference could be a problem 

Absolute Time Measurements
~~~~~~~~~~~~~~~~~~~~~~~~~~

* Not relative to a benchmark

- September 24th 2019 3:00 PM MDT 

* Time of an event in a calendar

* Tracked in Linux relative to the epoch 

 * Midnight, Jan 1st 1970


Software Clock in Linux
~~~~~~~~~~~~~~~~~~~~~~~

* System Timer instantiated by the kernel

- Uses a specific interval frequency.

 * Increments the elapsed time by one unit each time the interval ends - \"tick\" or \"jiffy\"

 - \"jiffies counter\" - 64 bit value

 * HZ - frequency of the system timer

 - platform dependent, historical x86 values range from 100 Hz to 1000 Hz 

* **What about jiffies timer rollover?**

 * for x86 each jiffy is 0.004 seconds, rollover in 2^64 * 0x004s = ~5.8 billion years  

 - Frequency of the system timer is call HZ - architecture specific.

 * POSIX time APIs will convert time for us, we don't need to use HZ. 


Time Representations 
~~~~~~~~~~~~~~~~~~~~

* time_t in <time.h> is defined as:

 - typedef long time_t;

- Represents seconds since the epoch (midnight Jan 1st 1970 UTC)

 * 32 bit machine long value will rollover - Monday 18th January 2038!

 * Y2Kv2 - 32 bit systems will stop working [1]_ 

 - What about sub second precision?


POSIX Clock Types
~~~~~~~~~~~~~~~~~

* CLOCK_REALTIME

 * system wide wall clock time

 - settable

- CLOCK_MONOTONIC

 * elapsed time since starting point (ie boot)

 - not settable

* When should you use CLOCK_MONOTONIC over CLOCK_REALTIME?

 * Don't use CLOCK_REALTIME when you are measuring intervals which are dependent on system time \*not\* changing.

 - The system time might be set/change backwards 

Time Representations
~~~~~~~~~~~~~~~~~~~~

* timeval (microsecond) 

 * get/settimeofday, adjtime

- timespec (nanosecond)

 * clock_gettime, clock_settime, nanosleep, clock_nanosleep [2]_


Time Representations - tm
~~~~~~~~~~~~~~~~~~~~~~~~~

* human readable time

- asctime, asctime_r, mktime, gmtime, gmtime_r, localtime, localtime_r [3]_ 

 * _r functions are thread safe

 - consider strftime instead of asctime

POSIX clock_gettime
~~~~~~~~~~~~~~~~~~~

* clock_time sample code [4]_

Setting Time
~~~~~~~~~~~~

* CLOCL_REALTIME is the cld_id to use with these

 * CLOCK_MONOTONIC isn't settable

- May require elevated permissions

* Begin adjusting the system time by delta to a more accurate time 

 * Slowly adjusts the system clock to match required delta 

 - Doesn't move clock backwards

 * Useful for Network Time Protocol (NTP)
   daemons

---------------------------------------------------------------------------

.. [1] Year 2038 problem 

 https://en.wikipedia.org/wiki/Year_2038_problem#:~:text=Thus%2C%20a%20signed%2032%2Dbit,on%20Tuesday%2C%2019%20January%202038.

.. [2] POSIX clock_gettime man page 

 https://linux.die.net/man/3/clock_gettime

.. [3] POSIX asctime man page

 https://man7.org/linux/man-pages/man3/asctime.3p.html

.. [4] POSIX clock_gettime sample code

 https://github.com/cu-ecen-aeld/aesd-lectures/blob/master/lecture9/time_functions.c
