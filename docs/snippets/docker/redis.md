---
hide:
  - toc
---

# Redis

**Redis** is an in-memory data store that allows you to quickly save and access data, making it useful for caching and real-time applications. It supports various data structures, like strings, lists, and hashes, and is known for its high performance and simplicity.

```yaml
services:
  <name>.redis:
    image: redis:latest
    container_name: <name>.Redis
    restart: no
    ports:
      - "6379:6379"
```
