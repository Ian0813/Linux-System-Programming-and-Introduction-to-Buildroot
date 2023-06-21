**Learning objectives:**

    - **Threading overview/review**
    
    - **Multithreading Tradeoffs**
    
    - **Threading models**


**Threads**

    * Binaries: dormant programs on storage
    
    * Processes: Binaries in action, running on the system 

      - Contains one or more threads
      - One thread = single threaded
      - More than one thread = multithreaded
      - Has dedicated virtualized memory

    * Threads:

      - Virtuadlize processor
      - Stack
      - Program state
      - Shared virtualized memory

    * Why Use Multithreading?

      - Alternative to state machines  
      - Parallelism - scales your process apllication to multiple processors 
      - improve responsiveness 

        * Long running operations don't belong in UI handling threads 
        * Blocking I/O doesn't belong in UI threads.

    * Additional supplementary:
      
      +-----------------------------------------------------------------------------------------------------+
      | For instance, you wouldn't want to put long-running operations in the UI handling thread.           | 
      | Because if those threads took a long time to complete or if actions with them thread took a long    |
      | time to complete. Then the UI would probably freeze up waiting for the user in. So that's an        |
      | example of where you'd want two different threads running one to be responsive to the user requests | 
      | in the UI. And maybe one to handle some kind of long running computational or other task.           | 
      +-----------------------------------------------------------------------------------------------------+

      +-----------------------------------------------------------------------------------------------------+
      | The blocking I/O wouldn't belong in UI thread so you wouldn't want to be waiting for a hardware     |
      | device or something like that.                                                                      | 
      +-----------------------------------------------------------------------------------------------------+

**Concurrency and Parallelism**

 * Concurrency 

   - Ability of two or more threads to execute in overlapping time periods 
   - Programming pattern

    =======  =====  ===== =====
    thread1  run..  
    thread2         run..
    thread3               run..
    =======  =====  ===== =====


 * Parallelism

   - Ability to execute two or more threads simultaneously
   - Requires multiple processors (hardware) (e.g. In Linux, we can check the processor amount by /proc/cpuinfo.) 

    =======  =====  ===== =====
    thread1  run..  run.. run.. 
    thread2  run..  run.. run.. 
    thread3  run..  run.. run..
    =======  =====  ===== =====

**Why Use Multithreading?**

 * Context switching 

   - Thread context switching is "cheaper than" process contextswitching (No additional overhead of swapping the different processes).

 * Memory savings

   - Share memory accross multiple execution units 

**Why Not Use Multithreading?**

 * Complexity

   - increase the cost for writing, understanding, debugging

 * Alternatives to Multithreading

   - Non-blocking I/O
   - Multiple processes

**Thread Design Model:**

  * Thread Per Connection Model
  
    * Each unit of work (request, connection, etc) gets a thread
    * Thread performs blocking I/O 
  
      - May need more threads than CPU processors for maximum parallelism. 
    * Breaks down as number of requests becomes very large.
    * Apache web server is an example of this model 

  * Event-Driven Threading Model

    - Uses asychronous I/O and callbacks 
    - Uses an event loop 
    - NGINX, Node.js are examples of this model
    - No reason to have more threads than CPU processors 
    - No waiting in threads
    - Author's suggestion: try this pattern first for yuor application.

**Amdahl's Law**

  * Refer to reference   
  * How does this relate to Event DRiven Threading and statement "no reason to have more threads than processors"?

    - Not doing any waiting in threads, can't be parallelization  

**Event Driven Threading and Parallelism**

  * Second sentence is true because we can't add more threads to parallelize if all threads are non-blocking and we've already got a thread assigned to each processor.


**Reference:**

1. thread work theory

 * https://www.javamex.com/tutorials/threads/how_threads_work.shtml 
 
2. Introduction to common web server 

 * https://opensource.com/business/16/8/top-5-open-source-web-servers
 
3. Thread design model

 * https://stackoverflow.com/questions/14189496/thread-in-an-event-driven-vs-non-event-driven-web-server

4. Amdahl's Law

 * http://www.umsl.edu/~siegelj/CS4740_5740/Overview/Amdahl's.html 
 * https://www.geeksforgeeks.org/computer-organization-amdahls-law-and-its-proof/
 * https://study.com/academy/lesson/amdahl-s-law-definition-formula-examples.html
 * https://en.wikipedia.org/wiki/Amdahl%27s_law 
 * https://learn.saylor.org/mod/page/view.php?id=27029&forceview=1

5. IBM - Thread Memory Leak

 * https://developer.ibm.com/tutorials/l-memory-leaks/

6. Non-blocking, Blocking and Asynchronous I/O

 * https://www.cs.rutgers.edu/courses/416/classes/fall_2009_ganapathy/slides/io.pdf 

Appendix:

+------------------------------------------------------------------------------------+
| From the perspective of system resources, the content switching of a thread is     |
| cheaper than a process because when a process swap out for another process swap in,| 
| the memory space needs to exchange. However, the threads don't need to exchange    |
| memory space because threads share the same memory space with each.                | 
+------------------------------------------------------------------------------------+
