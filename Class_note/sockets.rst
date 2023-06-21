=======
Sockets
=======

.. contents:: Outline

Learning objectives
~~~~~~~~~~~~~~~~~~~

* Understand Linux Sockets

- Understand How to Use Sockets in your programs 


Sockets
~~~~~~~

* One of serveral forms of interprocess Communication (IPC)

 * Can comminicate across different systems over TCP/IP

- Also known as BSD or Berkeley Sockets 

* Supported by all major operating system

- Reference [1]_

.. figure:: Connection_oriented_sockets.png


Port Forwarding
~~~~~~~~~~~~~~~

* Allow us to route port to VM or emultor

.. figure:: Port_forward.png
   :width: 600 pt

TCP
~~~

* Transmission Control Protocol

- Connection oriented protocol

 * Connection is established and maintained while programs are exchanging messages 

* Accepts packets

- Manages flow control

* Handles retransmission of dropped packets

- Handles acknowledgement of packets 
   
* Reference [2]_

UDP
~~~

* User Datagram Protocol

- Connectionless Protocol 

* preservation of sequence

- protection against duplication

* minimum resource used (e.g. bandwidth)


IP
~~

* Addresses Packets

- Supports routing between sender and receiver

* IPv4 was first implementation - X.X.X.X - 4 byte (32 bit) format - ~4.3 billion addresses

- IPv6 supports 128 bits of address space - 340 billion (10^9) billion billion billion addresses)

 * 4000 addresses for each person on earth

* Also uses a \"port\" for local addressing

Types of Sockets
~~~~~~~~~~~~~~~~

* SOCK_STREAM - Stream Sockets

 - Reliable two way connected (TCP) streams

 * Messages are delivered in order

 - Retried as necessary

- SOCK_DGRAM - Datagram Sockets

 * Connectionless sockets

 - Uses UDP (User Datagram Protocol) instead of TCP


Accessing Sockets
~~~~~~~~~~~~~~~~~

* In Linux everything is a file

- How do we interact with sockets?

 * Using a scoket file descriptor

* How do we obtain a socket file descriptor? 

 - Use the socket() POSIX function

- Reference [3]_

Socket connect vs Bind
~~~~~~~~~~~~~~~~~~~~~~

* Rederence [4]_

.. figure:: Socket_connect_vs_bind.png 
   :width: 500pt


Socket
~~~~~~

* domain - PF_INET or PF_INET6

- type SOCK_STREAM or SOCK_DGRAM

* protocol - 0 to choose the proper protocol for the given type  

- Reference [5]_

Bind
~~~~

* Assigns an address to the socket

- sockfd is the fd from socket()

* sockaddr addr/addrlen describes the address to bind (optionally select a specific network adapter) 

- sockaddr - maps to a server socket location

 * sa_family - AF_INET or AF_INET6

 - sa_data - destination address and port

* socketlen_t - unsigned integer type
  sizeof(struct sockaddr)

- Referenc [5]_

Setting up sockaddr
~~~~~~~~~~~~~~~~~~~

* sockaddr structure isn't built directly, setup from other structures

- Two options discussed:

 * Setting up sockaddr_in and casting to sockaddr

 - Setting up with getaddrinfo()

 * getaddrinfo is newer and more flexible

 - Either is acceptable for the assignment

* getaddrinfo provides addrinfo (containing sockaddr) through addrinfo argument

- malloced - must freeaddrinfo after use

* Reference [5]_ [7]_

Setting addrinfo hints and node
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* ai_flags in hints and node parameter sets up the socket address for bind()/accept()

 * hints.ai_flags = AI_PASSIVE 

 - node = NULL

* service parameter sets port for the connection

 - \"1234\" would setup for port 1234 

Getting sockaddr
~~~~~~~~~~~~~~~~

* Setup pointer res to store addrinfo returned from getaddrinfo

 * Pass addresss of pointer as res arg (pointer to pointer)

- Call getaddrinfo with hints, port string as service argument, and pointer to pointer in res  

- Use res->ai_addr as sockaddr for bind()

* freeaddrinfo(res) when no longer needed

 - What if you forget to free

  * Memory leak

listen
~~~~~~

* Passed sockfd from socket()

- backlog specifies number of pending connections allowed before refusing 

* Reference [6]_

accept
~~~~~~

* sockfd - socket file descriptor from socket()

- addr - location to store the connecting address

* addrlen in/out - length of addr and location to store the length of result  

- returns: fd for accepted connect 

* Reference [6]_

recv/send
~~~~~~~~~

* Similar to read/write file descriptor based commands we've discussed in early lectures 

- Use acceptedfd (from accept() return value) for server application

* Use blocking or non-blocking reads based on flags argument to recv/send

- Reference [5]_

---------------------------------------------------------------------------


.. [1] Berkeley sockets

  https://en.wikipedia.org/wiki/Berkeley_sockets

.. [2] TCP 

  https://www.techtarget.com/searchnetworking/definition/TCP

.. [3] Beej's Guides

  https://beej.us/guide/

.. [4] Socket connect vs bind

  https://stackoverflow.com/questions/27014955/socket-connect-vs-bind#:~:text=bind()%20associates%20the%20socket,connect%20to%20server%5D%20is%20used.

.. [5] POSIX API man page

  https://linux.die.net/man/2/socket

  https://linux.die.net/man/2/bind

  https://pubs.opengroup.org/onlinepubs/7908799/xns/syssocket.h.html 

  https://linux.die.net/man/3/getaddrinfo

  https://man7.org/linux/man-pages/man2/read.2.html

  https://man7.org/linux/man-pages/man2/recv.2.html

  https://man7.org/linux/man-pages/man2/send.2.html

  https://man7.org/linux/man-pages/man2/write.2.html

.. [6] Opengroup - POSIX API document 

  https://pubs.opengroup.org/onlinepubs/009696799/functions/listen.html

  https://pubs.opengroup.org/onlinepubs/009696799/functions/accept.html

  https://pubs.opengroup.org/onlinepubs/9699919799/functions/accept.html

.. [7] Pointer reference 

  https://www.tenouk.com/Module8a.html
