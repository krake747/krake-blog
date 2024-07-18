# MS SQL

```docker
services:
  [name].database.mssql:
    image: mcr.microsoft.com/mssql/server:2022-latest
    container_name: [Name].Database.Sql
    environment:
      - ACCEPT_EULA=true
      - MSSQL_SA_PASSWORD=Admin#123
      - MSSQL_PID=Express
    ports:
      - "1433:1433"
```
