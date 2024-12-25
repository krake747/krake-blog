---
hide:
  - toc
---

# MongoDB

**MongoDB** is an open-source NoSQL database system that stores data in flexible, JSON-like documents. It's known for its scalability and ease of use, making it ideal for applications requiring fast, schema-less data storage and retrieval.

```yaml
services:
  <name>.database.mongo:
    image: mongo:latest
    container_name: <name>.mongo
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: mongo
      MONGO_INITDB_ROOT_PASSWORD: mongo
    volumes:
      - ./.containers/mongo:/data/db
```