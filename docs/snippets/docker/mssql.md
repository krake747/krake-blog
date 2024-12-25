---
hide:
  - toc
---

# MS SQL

**Microsoft SQL Server** (MSSQL) is a relational database management system that stores and manages data using structured query language (SQL). It provides tools for handling data operations, queries, and transactions, making it a robust choice for building and maintaining databases in various applications.

=== "Default"

    ```yaml
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

=== "Docker Volume"

    ```yaml
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
          - volume.<name>.database.mssql:/var/opt/mssql
    
    volumes:
      volume.<name>.database.mssql
    ```

=== "Local Volume"

    ```yaml
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
          - ./.containers/mssql:/var/opt/mssql/data
    ```
