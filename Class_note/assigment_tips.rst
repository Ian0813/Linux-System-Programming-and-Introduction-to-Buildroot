=================
Assignment 5 Tips
=================

.. contents:: Outline 

-Wall and -Werror
~~~~~~~~~~~~~~~~~

 - Coding Guidlines

  * Every source file should compile with zero warnings (User -Werror/-Wall for solving bugs) or justification be provided for each warning  

   - Examples::

     $ gcc -c main.o main.c -Wall -Werror

Assignment 5 hints/suggestions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 * Remember to close file descriptor (from both socker() and accept()) to avoid memory leaks.

 - Consider using shutdown() in your signal handler strategy 

 * To avoid bind() failing with \"Address Already In Use\" user SO_REUSEADDR 

Assignment 5 Memory Leak Check
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 - Use Valgrind to check your program for memory leaks

  * Pronounced \"val grinned\"

  - Example execution for our aesdsocket::

    $ valgrind --leak-check=full --show-leak-kinds=all --track-origins=yes --verbose --log-file=valgrind-out.txt "./target_program"

  * Reference [2]_

---------------------------------------------------------------------------

.. [1] Assignment 5 hints / suggestions 

 - https://stackoverflow.com/questions/18173111/is-it-necessary-to-close-an-accept-return-file-descriptor

 * https://man7.org/linux/man-pages/man2/shutdown.2.html 

 - https://stackoverflow.com/questions/9365282/c-linux-accept-blocking-after-socket-closed/19239058#19239058 

 * https://beej.us/guide/bgnet/html 

.. [2] Valgrind usage

 * https://stackoverflow.com/questions/5134891/how-do-i-use-valgrind-to-find-memory-leakse
