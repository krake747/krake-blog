# Global Exception Handler

## Web API Project

Create the `GlobalExceptionHandler` using the `IExceptionHandler`.

```cs title="GlobalExceptionHandler.cs"
internal sealed class GlobalExceptionHandler(ILogger<GlobalExceptionHandler> logger)
    : IExceptionHandler
{
    public async ValueTask<bool> TryHandleAsync(HttpContext httpContext, Exception exception,
        CancellationToken cancellationToken = default)
    {
        logger.LogErrorUnhandledException(exception);

        var problemDetails = new ProblemDetails
        {
            Status = StatusCodes.Status500InternalServerError,
            Type = "https://datatracker.ietf.org/doc/html/rfc7231#section-6.6.1",
            Title = "Server failure"
        };

        httpContext.Response.StatusCode = problemDetails.Status.Value;

        await httpContext.Response.WriteAsJsonAsync(problemDetails, cancellationToken);

        return true;
    }
}

internal static partial class LoggerExtensions
{
    [LoggerMessage(Level = LogLevel.Error, Message = "Unhandled exception occurred")]
    public static partial void LogErrorUnhandledException(this ILogger logger, Exception exception);
}
```

Add the `GlobalExceptionHandler` to the service collection and for production environment add the `UseExceptionHandler` in the middleware pipeline.

```cs title="Program.cs" hl_lines="3 9 13"
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddExceptionHandler<GlobalExceptionHandler>();

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage(); // (1)
}
else
{
    app.UseExceptionHandler();
}

app.Run();
```

1. `UseDeveloperExceptionPage` middleware captures unhandled exceptions from the pipeline & generate HTML error response.