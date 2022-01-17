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
3) Topic Exchange

------------------------------
**Routing pattern matching examples:**
1) ```health.*``` – health as the first word followed by one word (```health.education```, ```health.sports```, ```health.anything```)
2) ```#.sports.*``` – Zero or more words, then sports, after that exactly one word (```sports.education```, ```sports.sports.sports```, ```sports.sports```)
3) ```#.education``` – Zero or more words followed by the word education (```health.education```, ```education.education```, ```education```)
------------------------------
**Default Exchange:**

*Producer:*
```
var factory = new ConnectionFactory() { HostName = "localhost" };
using (var connection = factory.CreateConnection())
using (var channel = connection.CreateModel())
{
    channel.QueueDeclare(queue: "dev-queue",
                         durable: false,
                         exclusive: false,
                         autoDelete: false,
                         arguments: null);

    string message = $"Message from publisher N {counter}";

    var body = Encoding.UTF8.GetBytes(message);

    channel.BasicPublish(exchange: "",
                        routingKey: "dev-queue",
                        basicProperties: null,
                        body: body);

    Console.WriteLine($"Message is sent into Default Exchange [N:{counter++}]");
}
```

*Consumer:*
```
var factory = new ConnectionFactory() { HostName = "localhost" };
using (var connection = factory.CreateConnection())
using (var channel = connection.CreateModel())
{
    channel.QueueDeclare(queue: "dev-queue",
                         durable: false,
                         exclusive: false,
                         autoDelete: false,
                         arguments: null);

    var consumer = new EventingBasicConsumer(channel);

    consumer.Received += (sender, e) =>
    {
        var body = e.Body;
        var message = Encoding.UTF8.GetString(body.ToArray());
        Console.WriteLine(" Received message: {0}", message);
    };

    channel.BasicConsume(queue: "dev-queue",
                         autoAck: true,
                         consumer: consumer);

    Console.WriteLine("Subscribed to the queue 'dev-queue'");

    Console.ReadLine();
}
```
------------------------------
**Direct Exchange:**

*Producer:*
```
static void Main(string[] args)
{
    Task.Run(CreateTask(12000, "error"));
    Task.Run(CreateTask(10000, "info"));
    Task.Run(CreateTask(8000, "warning"));

    Console.ReadKey();
}

    static Func<Task> CreateTask(int timeToSleepTo, string routingKey)
    {
        return () =>
        {
            var counter = 0;
            do
            {
                int timeToSleep = new Random().Next(1000, timeToSleepTo);
                Thread.Sleep(timeToSleep);

                var factory = new ConnectionFactory() { HostName = "localhost" };
                using (var connection = factory.CreateConnection())
                using (var channel = connection.CreateModel())
                {
                    channel.ExchangeDeclare(exchange: "direct_logs", type: ExchangeType.Direct);

                    string message = $"Message type [{routingKey}] from publisher N {counter}";

                    var body = Encoding.UTF8.GetBytes(message);

                    channel.BasicPublish(exchange: "direct_logs",
                                        routingKey: routingKey,
                                        basicProperties: null,
                                        body: body);

                    Console.WriteLine($"Message type [{routingKey}] is sent into Direct Exchange [N:{counter++}]");
                }
            } while (true);
        };
    }
}
```

*Consumer ALL:*
```
var factory = new ConnectionFactory() { HostName = "localhost" };
using (var connection = factory.CreateConnection())
using (var channel = connection.CreateModel())
{
    channel.ExchangeDeclare(exchange: "direct_logs", type: ExchangeType.Direct);

    var queueName = channel.QueueDeclare().QueueName;

    channel.QueueBind(queue: queueName,
                             exchange: "direct_logs",
                             routingKey: "error");
    channel.QueueBind(queue: queueName,
                             exchange: "direct_logs",
                             routingKey: "info");
    channel.QueueBind(queue: queueName,
                             exchange: "direct_logs",
                             routingKey: "warning");

    var consumer = new EventingBasicConsumer(channel);

    consumer.Received += (sender, e) =>
    {
        var body = e.Body;
        var message = Encoding.UTF8.GetString(body.ToArray());
        Console.WriteLine(" Received message: {0}", message);
    };

    channel.BasicConsume(queue: queueName,
                         autoAck: true,
                         consumer: consumer);

    Console.WriteLine($"Subscribed to the queue '{queueName}'");

    Console.ReadLine();
}
```

*Consumer ERROR:*
```
var factory = new ConnectionFactory() { HostName = "localhost" };
using (var connection = factory.CreateConnection())
using (var channel = connection.CreateModel())
{
    channel.ExchangeDeclare(exchange: "direct_logs", type: ExchangeType.Direct);

    var queueName = channel.QueueDeclare().QueueName;

    channel.QueueBind(queue: queueName,
                             exchange: "direct_logs",
                             routingKey: "error");

    var consumer = new EventingBasicConsumer(channel);

    consumer.Received += (sender, e) =>
    {
        var body = e.Body;
        var message = Encoding.UTF8.GetString(body.ToArray());
        Console.WriteLine(" Received message: {0}", message);
    };

    channel.BasicConsume(queue: queueName,
                         autoAck: true,
                         consumer: consumer);

    Console.WriteLine($"Subscribed to the queue '{queueName}'");

    Console.ReadLine();
}
```
------------------------------
**Issues:**
1. ```The AMQP operation was interrupted: AMQP close-reason, initiated by Peer, code=406, text='PRECONDITION_FAILED - inequivalent arg 'durable' for queue 'dev-queue' in vhost '/': received 'false' but current is 'true'', classId=50, methodId=10```

Попробовать удалить очередь из RabbitMQ Management.
