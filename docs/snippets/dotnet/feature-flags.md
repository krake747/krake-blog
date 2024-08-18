---
hide:
  - toc
tags:
  - .NET
  - C#
---

# Feature Flags

The repository for these snippets can be found here: [Krake.Snippets.FeatureFlags](https://github.com/krake747/krake-blog-snippets/tree/main/Krake.Snippets.FeatureFlags)

## .NET Minimal API Project

Add this Nuget packages to the .NET project.

```bash
dotnet add package Microsoft.FeatureManagement.AspNetCore
```

Afterwards setup the feature management services in the `Program.cs` file.

```cs title="Program.cs" hl_lines="7 11 15 24 36"
using Microsoft.AspNetCore.Mvc;
using Microsoft.FeatureManagement;
using Snippets.FeatureFlags;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddFeatureManagement(builder.Configuration.GetSection("FeatureFlags")); // (1)

var app = builder.Build();

app.MapGet("feature-a", static () => Results.Ok("Hello from Feature A")); // (2)

app.MapGet("feature-b", static async ([FromServices] IFeatureManager manager) =>
{
    if (await manager.IsEnabledAsync("FeatureB") is false) // (3)
    {
        return Results.NotFound();
    }

    return Results.Ok("Hello from Feature B");
});

app.MapGet("feature-c", () => Results.Ok("Hello from Feature C"))
    .AddEndpointFilter(static async (context, next) => // (4)
    {
        var featureManager = context.HttpContext.RequestServices.GetRequiredService<IFeatureManager>();
        if (await featureManager.IsEnabledAsync("FeatureC") is false)
        {
            return Results.NotFound();
        }

        return await next(context);
    });

app.MapGet("feature-d", () => Results.Ok("Hello from Feature D"))
    .AddEndpointFilter<FeatureFilter>(); // (5)

app.Run();

namespace Snippets.FeatureFlags
{
    internal sealed class FeatureFilter(IFeatureManager featureManager) : IEndpointFilter
    {
        public async ValueTask<object?> InvokeAsync(EndpointFilterInvocationContext context,
            EndpointFilterDelegate next)
        {
            if (await featureManager.IsEnabledAsync("FeatureD") is false)
            {
                return Results.NotFound();
            }

            return await next(context);
        }
    }
}
```

1. Registers feature management and links it to the "FeatureFlags" section in the configuration.
2. Does not use feature flags.
3. Controls access to an endpoint based on the "FeatureB" flag via `IFeatureManager`.
4. Uses an inline filter to manage access based on the "FeatureC" flag.
5. Uses a custom filter class to manage access based on the "FeatureD" flag.

Add the following section to the `appsettings.[env].json` configuration files which will allow you to enable and/or 
disable feature during runtime.

```json title="appsettings.json"
{
    "FeatureFlags": {
        "FeatureB": false,
        "FeatureC": true,
        "FeatureD": true
    },
}
```
