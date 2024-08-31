---
hide:
  - toc
---

# Papercut

**Papercut** is a lightweight SMTP server that is often used for testing email applications and configurations. It provides a simple and efficient way to simulate sending and receiving emails within a local development environment.

```yaml
services:
  <name>.papercut:
    image: jijiechen/papercut:latest
    container_name: <name>.papercut
    ports:
      - "25:25"
      - "37408:37408"
```
