**Learning objectives:**

    - **Understand Race Conditions**
    
    - **Synchronizaion with PThread**


**Race Conditions**

  * Different program behavior depending on which thread gets there first

  * Unsynchronized access of a shared resource leads to erroneous program behavior

    - hardware, kernel resource, memory 
    - memory - data race - most common form 

  * critical region - region of code which needs synchronization

  * Eliminate races by synchronizing thread access to critical regions 


**Example Race Conditions**

  * When is this code not thread safe?

    - When account is a shared structure in a multi-threaded program 

  * Is this code thread safe when the hardware does not support parallelism?
    
    - No, concurrency is still an issue. 
  
+------------------------------------------------------------------------------+
| /*                                                                           |
|                                                                              |
| Non thread-safe implementation of withdraw, using no locking                 |
|                                                                              |  
| \*/                                                                          |
|                                                                              |
| static bool withdraw_unsafe(struct account \*account, unsigned int amount) { |
|                                                                              |
|     bool success = false;                                                    |
|     const int balance = account->current_balance;                            |
|                                                                              |
|     if (balance >= amount) {                                                 |
|         success = true;                                                      |
|         printf("Withdrawl approved\n");                                      |
|                                                                              |
|         account->current_balance = balance - amount;                         |
|                                                                              | 
|         account->withdrawl_total += amount;                                  |
|         disburse_money(amount);                                              |
|                                                                              |
|     }                                                                        |
|     return success;                                                          |
|                                                                              |
| }                                                                            |
+------------------------------------------------------------------------------+

  * Refer to Linux System Programming Second Edition Chapter 7

   - An atomic operation is indivisible, unable to be interleaved with other operation, appears instantaneous 

   - ++ is not atomic
   
   - **To make shared memory operations safe we need to make the sequence atomic**

**Deadlocks**

  - Two threads both waiting for each other to finish
  
  - One thread blocked on a mutex it already holds.

  - How to avoid?

    - Lock data not code - are multiple locks really required?
    - Have a specific order for obtaining locks when multiple data locks are required
    - Release in opposite order obtained
