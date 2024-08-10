# Seq

```docker
services:
  <name>.seq:
    image: datalust/seq:latest
    container_name: <name>.Seq
    environment:
      - ACCEPT_EULA=Y
    ports:
      - "5341:5341"
      - "8081:80"
```
