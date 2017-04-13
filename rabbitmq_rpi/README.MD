
## How to build the image
docker build -t skrymer/rabbitmq-rpi:latest .

## How to run
docker run -P --hostname rabbit1 --name rabbitmq -p 15672:15672 -p 5672:5672 skrymer/rabbitmq-rpi

if evertyhing works ok the rabbitmq manager is avaliable on localhost:15672 using guest/guest as logon

## Simple python script to send and recieve messages

* pip install pika

### send

```python
#!/usr/bin/env python
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters('localhost'))

channel = connection.channel()
channel.queue_declare(queue='hello')
channel.basic_publish(exchange='', 
                      routing_key='hello', 
                      body='Hello World!')

print(" [x] Sent 'Hello World!'")
connection.close()
```
### recieve

```python
#!/usr/bin/env python
import pika

connection = pika.BlockingConnection(pika.ConnectionParameters(host='localhost'))
channel = connection.channel()

channel.queue_declare(queue='hello')

def callback(ch, method, properties, body):print(" [x] Received %r" % body)

channel.basic_consume(callback,
                      queue='hello',
                      no_ack=True)

print(' [*] Waiting for messages. To exit press CTRL+C')
channel.start_consuming()
```
