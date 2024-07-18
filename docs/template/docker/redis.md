# Redis

```docker
services:
  [name].redis:
    image: redis:latest
    container_name: [Name].Redis
    restart: no
    ports:
      - "6379:6379"
```
