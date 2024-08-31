---
hide:
  - toc
---

# Seq

**Seq** is a log server designed for collecting and querying structured log data from applications. It is used to analyze and troubleshoot applications by providing a powerful search interface and visualizations for logs.

```yaml
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
