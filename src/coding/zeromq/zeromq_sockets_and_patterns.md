# ZeroMQ Sockets and Patterns

> Note: the `zmq_send()` function is bad at dealing with messages of arbitrary or unknown size. The `zmq_msg_send()` function is better at this, though uses a more difficult API.
> To get the best understanding of how messages are used/passed in ZeroMQ using the *zmq_msg_t* structure, refer to Chp. 2 of the ZeroMQ Guide on *Working with Messages*.


?? zmq_pollitem_t ??

### Pub-Sub Message Envelopes
Envelopes are structures that split the *key/topic* from the *message data*. Envelopes have to be created by the developer: ZMQ doesn't natively support them in their API.

Subscription topics work by prefix matching. Thus, there is potential for the message content to match the prefix. Envelopes fix this issue by seperating the subscription prefix from any additional data that you wish to send over the wire.

In ZMQ, you can implement envelopes by sending multipart messages where the first frame is the *key/topic* the next frame is the *address* (typical use case for pub-sub messaging when you want to send data over another socket) and the final frame is the *data*.

> See [ZeroMQ Guide: Pub-Sub Message Envelopes](https://zguide.zeromq.org/docs/chapter2/#Pub-Sub-Message-Envelopes)

ZMQ manages an internal message queue