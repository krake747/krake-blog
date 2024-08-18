---
hide:
  - toc
tags:
  - .NET
  - C#
---

# Dapper

The repository for these snippets can be found here: [Krake.Snippets.Dapper](https://github.com/krake747/krake-blog-snippets/tree/main/Krake.Snippets.Dapper)

## .NET Minimal API Project

Add the `Dapper` NuGet packages to the .NET project. 
Additionally, you need to use one of the supported database providers. This example uses `Sqlite`.

```bash
dotnet add package Dapper
dotnet add package System.Data.SQLite.Core
```

Afterwards add the database connection factory services in the `Program.cs` file.

```cs title="Program.cs" hl_lines="8"
using System.Data;
using Dapper;
using Krake.Snippets.Dapper;
using Microsoft.Data.Sqlite;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddScoped<IDbConnectionFactory, SqliteConnectionFactory>(sp => // (1)
{
    var connectionString = sp.GetRequiredService<IConfiguration>().GetConnectionString("DefaultConnection");
    return new SqliteConnectionFactory(connectionString);
});

var app = builder.Build();

app.MapGet("/example", async (IDbConnectionFactory dbConnectionFactory) =>
{
    using var connection = await dbConnectionFactory.CreateConnectionAsync();
    // Use the connection...
    return Results.Ok();
});

using (var scope = app.Services.CreateScope())
{
    var dbConnectionFactory = scope.ServiceProvider.GetRequiredService<IDbConnectionFactory>();
    await new DatabaseInitializer(dbConnectionFactory).InitializeAsync();
}

app.Run();

namespace Krake.Snippets.Dapper
{
    public interface IDbConnectionFactory
    {
        Task<IDbConnection> CreateConnectionAsync(CancellationToken token = default);
    }

    public sealed class SqliteConnectionFactory(string connectionString) : IDbConnectionFactory
    {
        public async Task<IDbConnection> CreateConnectionAsync(CancellationToken token = default)
        {
            var connection = new SqliteConnection(connectionString);
            await connection.OpenAsync(token);
            return connection;
        }
    }

    public sealed class DatabaseInitializer(IDbConnectionFactory connectionFactory)
    {
        public async Task InitializeAsync()
        {
            using var connection = await connectionFactory.CreateConnectionAsync();
            await connection.ExecuteAsync( // lang=sql
                """
                // Initialize bookstore database... // (2)
                """
            );
        }
    }
}
```

1. `Scoped` lifetime ensures that each request gets its own instance of `IDbConnection`, which is ideal for managing database connections that should be opened and closed per request.
2. The bookstore initialization scripts are found in the [Krake.Snippets.Dapper](https://github.com/krake747/krake-blog-snippets/tree/main/Krake.Snippets.Dapper) repo.

## Dapper in Action

```cs title="Bookstore.cs"
public sealed class Author
{
    public int Id { get; set; }
    public string Name { get; set; } = string.Empty;
}

public sealed class Customer
{
    public int Id { get; set; }
    public string Name { get; set; } = string.Empty;
    public string Email { get; set; } = string.Empty;
}

public sealed class Order
{
    public int Id { get; set; }
    public DateTime OrderDate { get; set; }
    public Customer Customer { get; set; } = null!;
    public List<Book> Books { get; set; } = [];
}

public sealed class TopSellingBook
{
    public string Title { get; set; } = string.Empty;
    public int TotalSold { get; set; }
}
```
### Basic Queries and Commands

```cs
// Basic Dapper Command
app.MapPost("/customers", async (IDbConnectionFactory dbConnectionFactory, Customer customer) =>
{
    using var connection = await dbConnectionFactory.CreateConnectionAsync();

    const string sql = // lang=sql
        """
        INSERT INTO Customers (Name, Email)
        VALUES (@Name, @Email)
        RETURNING Id;
        """;

    customer.Id = await connection.ExecuteScalarAsync<int>(sql, customer);

    return customerId is null ? Results.BadRequest() : Results.Created($"/customers/{customer.Id}", customer);
});

// Basic Dapper Query
app.MapGet("/customers/{id:int}", async (IDbConnectionFactory dbConnectionFactory, int id) =>
{
    using var connection = await dbConnectionFactory.CreateConnectionAsync();

    const string sql = // lang=sql
        """
        SELECT Id, Name, Email
        FROM Customers
        WHERE Id = @Id
        """;

    var customer = await connection.QuerySingleOrDefaultAsync<Customer>(sql, new { Id = id });

    return customer is not null ? Results.Ok(customer) : Results.NotFound();
});
```

### Advanced Queries and Mapping
```cs
// Advanced Dapper Query with mapping function
app.MapGet("/books", async (IDbConnectionFactory dbConnectionFactory) =>
{
    using var connection = await dbConnectionFactory.CreateConnectionAsync();

    const string sql = //lang=sql
        """
            SELECT
                b.Isbn, b.Title, b.Price,
                a.Id, a.Name
            FROM Books b
                LEFT JOIN BookAuthors ba ON b.Isbn = ba.BookIsbn
                LEFT JOIN Authors a ON ba.AuthorId = a.Id
        """;

    var books = new Dictionary<string, Book>();
    _ = await connection.QueryAsync<Book, Author, Book>(
        sql,
        (book, author) =>
        {
            if (books.TryGetValue(book.Isbn, out var existingBook) is false)
            {
                existingBook = book;
                books.Add(existingBook.Isbn, existingBook);
            }

            existingBook.Authors.Add(author);
            return existingBook;
        },
        splitOn: "Id"
    );

    return Results.Ok(new { Books = books.Values });
});

// Advanced Dapper Query with mapping function and custom response mapping
app.MapGet("/orders", async (IDbConnectionFactory dbConnectionFactory) =>
{
    using var connection = await dbConnectionFactory.CreateConnectionAsync();

    const string sql = //lang=sql
        """
        SELECT
            o.Id, o.OrderDate,
            c.Id, c.Name, c.Email,
            b.Isbn, b.Title
        FROM Orders o
            JOIN Customers c ON o.CustomerId = c.Id
            LEFT JOIN OrderBooks ob ON o.Id = ob.OrderId
            LEFT JOIN Books b ON ob.BookIsbn = b.Isbn
        """;

    var orders = new Dictionary<int, Order>();
    _ = await connection.QueryAsync<Order, Customer, Book, Order>(
        sql,
        (order, customer, book) =>
        {
            if (orders.TryGetValue(order.Id, out var existingOrder) is false)
            {
                existingOrder = order;
                existingOrder.Customer = customer;
                orders.Add(existingOrder.Id, existingOrder);
            }

            existingOrder.Books.Add(book);
            return existingOrder;
        },
        splitOn: "Id,Id,Isbn"
    );

    return Results.Ok(new
    {
        Orders = orders.Values.Select(o => new
        {
            o.Id,
            o.OrderDate,
            o.Customer,
            Books = o.Books.Select(b => new
            {
                b.Isbn,
                b.Title
            })
        })
    });
});
```

### Dapper Multiple Result Sets

```cs
// Dapper multiple result sets
app.MapGet("/sales-statistics", async (IDbConnectionFactory dbConnectionFactory) =>
{
    using var connection = await dbConnectionFactory.CreateConnectionAsync();

    const string sql = // lang=sql
        """
        SELECT COUNT(*) AS TotalOrders
        FROM Orders;

        SELECT SUM(b.Price * ob.Quantity) AS TotalSales
        FROM Orders o
        JOIN OrderBooks ob ON o.Id = ob.OrderId
        JOIN Books b ON ob.BookIsbn = b.Isbn;

        SELECT b.Title, SUM(ob.Quantity) AS TotalSold
        FROM Books b
        JOIN OrderBooks ob ON b.Isbn = ob.BookIsbn
        GROUP BY b.Title
        ORDER BY TotalSold DESC
        LIMIT 5;
        """;

    await using var result = await connection.QueryMultipleAsync(sql);
    var totalOrders = await result.ReadSingleAsync<int>();
    var totalSales = await result.ReadSingleAsync<decimal>();
    var topSellingBooks = (await result.ReadAsync<TopSellingBook>()).AsList();

    return Results.Ok(new
    {
        TotalOrders = totalOrders,
        TotalSales = totalSales,
        TopSellingBooks = topSellingBooks
    });
});
```

## Other Database Providers

### MS Sql Server

```cs
using System.Data;
using Microsoft.Data.SqlClient;

public sealed class SqlConnectionFactory(string connectionString) : IDbConnectionFactory
{
    public async Task<IDbConnection> CreateConnectionAsync(CancellationToken token = default)
    {
        var connection = new SqlConnection(connectionString);
        await connection.OpenAsync(token);
        return connection;
    }
}
```

### Postgres

```cs
using System.Data;
using Npgsql;

public sealed class NpgsqlConnectionFactory(string connectionString) : IDbConnectionFactory
{
    public async Task<IDbConnection> CreateConnectionAsync(CancellationToken token = default)
    {
        var connection = new NpgsqlConnection(connectionString);
        await connection.OpenAsync(token);
        return connection;
    }
}
```