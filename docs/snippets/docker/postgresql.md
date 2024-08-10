---
hide:
  - toc
---

# PostgreSQL

```docker
services:
  <name>.database.postgresql:
    image: postgres:latest
    container_name: <name>.Database.PostgreSQL
    environment:
      - POSTGRES_DB=<name>
      - POSTGRES_USER=sa
      - POSTGRES_PASSWORD=Admin#123
    ports:
      - "5432:5432"
```
