# Serilog

## Web Api Project

Add these two Nuget packages to the .NET project.

```bash
dotnet add package Serilog.AspNetCore
dotnet add package Serilog.Sinks.Console
```

Afterwards setup Serilog in the `Program.cs` file.

```cs  hl_lines="9 14"
using Serilog;

var builder = WebApplication.CreateBuilder(args);

Log.Logger = new LoggerConfiguration()
    .ReadFrom.Configuration(builder.Configuration)
    .CreateLogger();

builder.Host.UseSerilog(static (ctx, lc) => lc.ReadFrom.Configuration(ctx.Configuration)); // (1)
//builder.Services.AddSerilog(Log.Logger) // (2)

var app = builder.Build();

app.UseSerilogRequestLogging();

try
{
    app.Run();
}
finally
{
    Log.CloseAndFlush();
}

```

1. `UseSerilog` configures serilog as the only logging provider.
2. `AddSerilog` adds Serilog as one of potentially many logging providers.

Add the following section to the `appsettings.[env].json` configuration files and remove the default `Logging` section.

```json
{
    "Serilog": {
        "Using": [
            "Serilog.Sinks.Console"
        ],
        "MinimumLevel": {
            "Default": "Information",
            "Override": {
                "Microsoft": "Warning",
                "Microsoft.AspNetCore": "Warning",
                "System": "Warning"
            }
        },
        "WriteTo": [
            {
                "Name": "Console"
            }
        ],
        "Enrich": [
            "FromLogContext",
            "WithMachineName",
            "WithThreadId"
        ],
        "Properties": {
            "Application": "[Name]"
        }
    }
}
```
