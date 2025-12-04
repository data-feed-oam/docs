# Demo usage

## Python Client - Snapshot

```python
import requests

url = "https://external-api.oam.ltd/v1/event/bookmaker/1"
resp = requests.get(url)
print(resp.json())
```

## Python Consumer - RabbitMQ

```python
import pika, json

connection = pika.BlockingConnection(pika.ConnectionParameters(
    host="external-rmq.oam.ltd", virtual_host="/feed",
    credentials=pika.PlainCredentials("user", "password")
))
channel = connection.channel()

channel.exchange_declare(exchange="feed.exchange", exchange_type="topic")

queue = channel.queue_declare("", exclusive=True).method.queue
channel.queue_bind(exchange="feed.exchange", queue=queue, routing_key="soccer.event.update")


def callback(ch, method, properties, body):
    data = json.loads(body)
    print("Ricevuto:", data)


channel.basic_consume(queue=queue, on_message_callback=callback, auto_ack=True)
print("In attesa di messaggi...")
channel.start_consuming()
```
