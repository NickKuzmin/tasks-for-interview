- www.erlang.org
- www.rabbitmq.com
- https://github.com/DeveloperStories/RabbitMQ
------------------------------
**RabbitMQ Documentation:**
- Management: https://www.rabbitmq.com/management.html
- Installation: https://www.rabbitmq.com/install-windows.html
- AMQP: https://www.rabbitmq.com/tutorials/amqp-concepts.html
- Tutorials: https://www.rabbitmq.com/getstarted.html
------------------------------
- ```localhost:15672 (guest - guest)```
- Management:
```
cd C:\Program Files\RabbitMQ Server\rabbitmq_server-3.9.12\sbin
rabbitmq-plugins enable rabbitmq_management
```
------------------------------
- RabbitMQ Management -> Exchanges -> Add a new Exchanges -> Name = "dev-exchange" + Type = "Fanout"
- RabbitMQ Management -> Queue -> Add a new Queue -> Name = "dev-queue"
- RabbitMQ Management -> Exchanges -> ```Exchange Instance``` -> Bindings -> To Queue = "dev-queue" (После добавления - появится Binding в Exchanges + Queue)
- RabbitMQ Management -> Exchanges -> ```Exchange Instance``` -> Publish Message -> Payload = "First message-broker message" -> Publish Message
- RabbitMQ Management -> Exchanges -> ```Queue Instance``` -> Get Messages (+ Ack mode, Encoding, ...) -> Get Message(s) button
------------------------------
**Exchange types:**
1) Default Exchange
2) Direct Exchange
3) 
------------------------------
**Issues:**
1. ```The AMQP operation was interrupted: AMQP close-reason, initiated by Peer, code=406, text='PRECONDITION_FAILED - inequivalent arg 'durable' for queue 'dev-queue' in vhost '/': received 'false' but current is 'true'', classId=50, methodId=10```

Попробовать удалить очередь из RabbitMQ Management.
