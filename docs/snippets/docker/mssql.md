---
hide:
  - toc
---

# MS SQL

## Default

```docker
services:
  <name>.database.mssql:
    image: mcr.microsoft.com/mssql/server:2022-latest
    container_name: <name>.Database.Sql
    environment:
      - ACCEPT_EULA=true
      - MSSQL_SA_PASSWORD=Admin#123
      - MSSQL_PID=Express
    ports:
      - "1433:1433"
```

## Docker Volume

```docker
volumes:
  volume.<name>.database.mssql

  services:
  <name>.database.mssql:
    image: mcr.microsoft.com/mssql/server:2022-latest
    container_name: <name>.Database.Sql
    environment:
      - ACCEPT_EULA=true
      - MSSQL_SA_PASSWORD=Admin#123
      - MSSQL_PID=Express
    ports:
      - "1433:1433"
    volumes:
      - volume.<name>.database.mssql:/var/opt/mssql # Docker  
```

## Local Volume

```docker
  services:
  <name>.database.mssql:
    image: mcr.microsoft.com/mssql/server:2022-latest
    container_name: <name>.Database.Sql
    environment:
      - ACCEPT_EULA=true
      - MSSQL_SA_PASSWORD=Admin#123
      - MSSQL_PID=Express
    ports:
      - "1433:1433"
    volumes:
      - ./.containers/mssql:/var/opt/mssql/data # Local  
```
