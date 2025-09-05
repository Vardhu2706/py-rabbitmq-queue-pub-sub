# RabbitMQ Tutorial #3 - Publish/Subscribe (Python)

In this tutorial, we’ll build a simple **publish/subscribe** system using RabbitMQ.  
Instead of sending messages to a single queue, the producer publishes messages to an **exchange**, and multiple consumers (subscribers) receive copies of the same message.

---

## Overview

- **Producer (`emit_log.py`):** Publishes messages to a `fanout` exchange named `logs`.
- **Exchange (`logs`):** Broadcasts all received messages to every queue bound to it.
- **Consumers (`receive_logs.py`):** Each consumer creates a fresh, temporary queue and binds it to the exchange.  
  Every consumer gets its own copy of the message.

Diagram:

```
[Producer] ---> [Exchange: logs] ---> [Queue 1] ---> [Consumer 1]
                                 ---> [Queue 2] ---> [Consumer 2]
```

---

## Key Points

- **Exchanges** are message routers. Here we use the `fanout` type to broadcast to all queues.
- Consumers use **temporary, exclusive queues** that are automatically deleted when the consumer disconnects.
- Every consumer gets **a copy** of the published log message.

---

## Running the Example

1. Start RabbitMQ server.
2. Run one or more consumers:
   ```bash
   python receive_logs.py
   ```
3. Publish a log message:
   `    python emit_log.py "info: This is a log message."
   `
   All running consumers will print the log message.

## Reference

- Tutorial #2: https://github.com/Vardhu2706/py-rabbitmq-queue-work-queues/tree/main
- Official tutorial: [RabbitMQ - Tutorial Three (Python)](https://www.rabbitmq.com/tutorials/tutorial-three-python)
