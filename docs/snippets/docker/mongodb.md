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

```yaml
services:
  mongodb:
    build:
      context: .
      dockerfile: database/Dockerfile
    container_name: mongodb
    environment:
        MONGO_INITDB_ROOT_USERNAME: root
        MONGO_INITDB_ROOT_PASSWORD: root
    ports:
      - "27017:27017"
    command: --replSet rs0 --keyFile /etc/mongo-keyfile --bind_ip_all --port 27017
    healthcheck:
      test: echo "try { rs.status() } catch (err) { rs.initiate({_id:'rs0',members:[{_id:0,host:'127.0.0.1:27017'}]}) }" | mongosh --port 27017 -u root -p root --authenticationDatabase admin
      interval: 5s
      timeout: 15s
      start_period: 15s
      retries: 10
    volumes:
      - data:/data/db

volumes:
  data: {}
```

```dockerfile
FROM mongo:latest
RUN openssl rand -base64 756 > /etc/mongo-keyfile 
RUN chmod 400 /etc/mongo-keyfile 
RUN chown mongodb:mongodb /etc/mongo-keyfile
```

```json
"ConnectionStrings": {
    "Mongo": "mongodb://root:root@localhost:27017/?replicaSet=rs0"
},
```