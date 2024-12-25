---
hide:
  - toc
---

# RabbitMQ

**RabbitMQ** is an open-source message broker that enables applications to communicate by sending and receiving messages through queues. It's known for its reliability, flexibility, and support for multiple messaging protocols, making it ideal for building scalable and distributed systems.

```yaml
services:
  <name>.queue.rabbitmq:
    image: rabbitmq:management-alpine
    container_name: <name>.queue.rabbitmq
    hostname: <name>-queue
    volumes:
      - ./.containers/queue/data/:/var/lib/rabbitmq
      - ./.containers/queue/log/:/var/log/rabbitmq
    environment:
      RABBITMQ_DEFAULT_USER: admin
      RABBITMQ_DEFAULT_PASS: admin
    ports:
      - "5672:5672"
      - "15672:15672"
```