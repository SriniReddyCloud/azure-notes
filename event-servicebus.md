# Azure Service Bus
## Overview
- Service Bus can decouple applications and services.
- Service Bus is intended for traditional enterprise applications. These enterprise applications require transactions, ordering, duplicate detection, and instantaneous consistency. 
- Service Bus enables cloud-native applications to provide reliable state transition management for business processes. 
- When handling high-value messages that cannot be lost or duplicated, use Azure Service Bus. 
- Service Bus also facilitates highly secure communication across hybrid cloud solutions and can connect existing on-premises systems to cloud solutions.
- Service Bus is a brokered messaging system. It stores messages in a "broker" (for example, a queue) until the consuming party is ready to receive the messages.
- Enable 1:n relationships between publishers and subscribers.
- It has the following characteristics:
  - reliable asynchronous message delivery (enterprise messaging as a service) that requires polling
  - advanced messaging features like FIFO, batching/sessions, transactions, dead-lettering, temporal control, routing and filtering, and duplicate detection
  - at least once delivery
  - optional in-order delivery


## Concepts
- Producer / Sender
- Queue
  - Brokered messaging communication model: components of a distributed application do not communicate directly with each other; instead they exchange messages via a queue, which acts as an intermediary (broker)
  - Each message is processed by a SINGLE consumer

- Topic
  - Publish/subscribe messaging communication model: components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary
  - One-to-many form of communication: when a message is sent to a topic, it is then made available to each subscription to handle/process independently
  
## Authentication and Authorization
- Shared Access Key
  - Namespace level
  - Queue level

## Configurations
- Data Encryption At Rest: Support customer-managed key
- Queue
  - Size
  - Message retention (time to live)
    - Message time to live determines how long a message will stay in the queue before it expires and is removed or dead lettered. 
    - When sending messages it is possible to specify a different time to live for only that message. 
    - This default will be used for all messages in the queue which do not specify a time to live for themselves.
  - Lock duration
    - Sets the amount of time that a message is locked for other receivers. 
    - After its lock expires, a message pulled by one receiver becomes available to be pulled by other receivers. 
    - Defaults to 30 seconds, with a maximum of 5 minutes.
		- Duplicate detection
  - Dead Lettering
    - Dead lettering messages involves holding messages that cannot be successfully delivered to any receiver to a separate queue after they have expired. 
    - Messages do not expire in the dead letter queue, and it supports peek-lock delivery and all transactional operations.
  - Sessions
    - allow ordered handling of unbounded sequences of related messages. 
    - guarantee first-in-first-out delivery of messages.
  - Partition
    - Partitions a queue across multiple message brokers and message stores. 
    - Disconnects the overall throughput of a partitioned entity from any single message broker or messaging store. 
    - Not modifiable after a queue has been created.
  - Queue URL
    - To send message to
    - To receive message from
- Topic
    - Only available in standard and premium tier

## SKU and pricing
- The Azure Service Bus Standard tier operates as a multi-tenant setup with a pay-as-you-go pricing model


## Throttling

## Service Bus Queue vs Storage Queue
- Storage queues
  - part of the Azure storage infrastructure, feature a simple REST-based GET/PUT/PEEK interface, providing reliable, persistent messaging within and between services.
  - consider using Storage queues when:
    - store over 80 GB of messages in a queue.
    - track progress for processing a message inside of the queue. This is useful if the worker processing a message crashes. A subsequent worker can then use that information to continue from where the prior worker left off.
    - server side logs of all of the transactions executed against your queues.

			
- Service Bus queues
  - part of a broader Azure messaging infrastructure that supports queuing as well as publish/subscribe, and more advanced integration patterns.
  - consider using Service Bus queues when:
    - receive messages without having to poll the queue. With Service Bus, this can be achieved through the use of the long-polling receive operation using the TCP-based protocols that Service Bus supports.
    - guaranteed first-in-first-out (FIFO) ordered delivery
    - automatic duplicate detection
    - "At-Most-Once" delivery guarantee
    - batches of messages
    - process messages as parallel long-running streams (messages are associated with a stream using the SessionId property on the message). In this model, each node in the consuming application competes for streams, as opposed to messages. When a stream is given to a consuming node, the node can examine the state of the application stream state using transactions.
    - transactional behavior and atomicity when sending or receiving multiple messages from a queue.
    - messages that can exceed 64 KB but will not likely approach the 256 KB limit.
    - RBAC to the queues, and different rights/permissions for senders and receivers. 
    - AMQP 1.0 standards-based messaging protocol
    - migration from queue-based point-to-point communication to a message exchange pattern that enables seamless integration of additional receivers (subscribers), each of which receives independent copies of either some or all messages sent to the queue. The latter refers to the publish/subscribe capability natively provided by Service Bus.


