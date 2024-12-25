---
hide:
  - toc
---

# Jeager

**Jaeger** is an open-source distributed tracing system designed for monitoring and troubleshooting microservices-based architectures. It helps track requests across services, visualize performance bottlenecks, and improve system observability.

```yaml
services:
  <name>.jaeger:
    image: jaegertracing/all-in-one:latest
    container_name: <name>.jaeger
    ports:
      - "4317:4317"
      - "4318:4318"
      - "16686:16686"
```