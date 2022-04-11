# ZeroMQ Basics

> Links:
> - [ZeroMQ Basics](https://zguide.zeromq.org/docs/chapter1/#Programming-with-ZeroMQ)

## Programming with ZeroMQ

1. Learn ZeroMQ step-by-step. Take is slow and learn to master each of the simple building blocks.

2. Write nice code. Use variable names that *have real words* and use *consistent indentation*.

3. Test what you make as you make it. Break your code into small chuncks.
   
The *context* is one of the most important aspects of ZeroMQ. The *context* is what you use to create sockets. There should only be one *context* per process, sometimes more is okay, but be **really sure that's what you want** before making that your design.

> Call `zmq_ctx_new()` once at the start of a process, and `zmq_ctx_destroy()`once at the end.

4. Always clean up when you finish a job. The ZeroMQ objects you need to worry about are *messages*, *sockets*, and *contexts*.
  - Use `zmq_send()` and `zmq_recv()` whenever possible as is avoids the need to use `zmq_msg_t` objects.
  - If you do use `zmq_msg_recv()`, always release the received message as soon as you’re done with it, by calling `zmq_msg_close()`.
  - Don't open and close lots of sockets. If you are you probably have a design problem.
  - When you exit the program, close your sockets and then call `zmq_ctx_destroy()` to destroy the context.

### Clean Exit with Multithreaded ZeroMQ

1. Do not try to use the same socket from multiple threads, ever.
2. Shutdown each socket that has ongoing requests by setting a low LINGER value (1 second), and then close the socket. Your language binding should do this for you automatically if you destroy a context.
3. Destroy the context.

## The Life of a ZeroMQ socket

1. Creating and desttorying sockets (with `zmq_socket()`, `zmq_close()`)
2. Configuring sockets by setting options on them and checking them if necessary (with `zmq_setsockopt()`, `zmq_getsockopt()`)
3. Plugging sockets into the network topology by creating connections (with `zmq_bind()`, `zmq_connect()`)
4. Using the sockets to carry data by writing and receiving messages on them (with `zmq_send()`, `zmq_recv()`)

Sockets are always void pointers, while messages are structures the programmer defines.

You should think of your *servers* (the ones that call `zmq_bind()`) as relatively static parts of your application, while the *clients* (the ones that call `zmq_connect()`) are more dynamic and can come and go.

