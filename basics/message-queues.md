# Message Queues

_= durable component, stored in memory, that supports asynchronous communication. Helps reduce request times for expensive operations that would otherwise be performed in-line. Receives, holds, and delivers messages._

<figure><img src="../.gitbook/assets/11.webp" alt=""><figcaption></figcaption></figure>

If an operation is too slow to perform inline, you can use a message queue with the following workflow:

* An application publishes a job to the queue, then notifies the user of job status.
* A worker picks up the job from the queue, processes it, then signals the job is complete.

e.g. RabbitMQ, Amazon SQS

## SQS

* supports <mark style="color:yellow;">**dead-letter queues (DLQ)**</mark> - useful for debugging your application or messaging system because they let you isolate unconsumed messages to determine why their processing doesn't succeed.
* supports <mark style="color:yellow;">**visibility timeout**</mark> - When a consumer receives and processes a message from a queue, the message remains in the queue. SQS doesn't automatically delete the message, the consumer needs to. To prevent other consumers from processing the message again, SQS sets a _visibility timeout_, a period of time during which Amazon SQS prevents all consumers from receiving and processing the message. - a message is hidden _only after it is consumed from the queue_.
* supports <mark style="color:yellow;">**delay queues**</mark> - let you postpone the delivery of new messages to consumers for a number of seconds -  a message is hidden _when it is first added to queue_

