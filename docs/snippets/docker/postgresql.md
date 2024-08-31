---
hide:
  - toc
---

# PostgreSQL

**PostgreSQL** is an open-source database system that uses SQL to manage and query data. It's known for its flexibility and support for advanced features like complex queries and custom data types, making it a great choice for developers building a wide range of applications.

```yaml
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
