- www.erlang.org
- www.rabbitmq.com
------------------------------
**RabbitMQ Documentation:**
- Management: https://www.rabbitmq.com/management.html
- Installation: https://www.rabbitmq.com/install-windows.html
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
- RabbitMQ Management -> Exchanges -> ```Queue Instance``` -> Get Messages -> Get Message(s) button
