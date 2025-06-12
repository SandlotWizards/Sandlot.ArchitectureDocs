# 📘 ActionLoggerService Reference

## 📘 Purpose

This document supplements the canonical standard for `ActionLoggerService` by providing usage examples and rationale for application developers, CLI tools, and orchestrators.

---

## 🧭 Common Use Patterns

### ➕ Begin a Step

```csharp
using (_logger.BeginStep("Scaffold service layer"))
{
    // Do something meaningful
}
```

### 🧾 Log Informational Message

```csharp
_logger.Info("Creating folder structure...");
```

### ⚠️ Emit Warning

```csharp
_logger.Warning("No files found in input folder.");
```

### ❌ Report Error + Throw

```csharp
_logger.Error("Validation failed", throwException: true);
```

### ✔ Log Success

```csharp
_logger.Success("Scaffolding complete.");
```

### 🪪 Use Global Logger Singleton

```csharp
ActionLogger.Global.PrintHeader();
ActionLogger.Global.Info("Starting Copilot process...");
```

---

## 🧰 Header/Trailer

```csharp
_logger.PrintHeader();
_logger.PrintTrailer();
```

These help delineate execution boundaries in terminal output.

---

## ⏱ Step Thresholds

```csharp
using (_logger.BeginStep("Long task", threshold: TimeSpan.FromSeconds(2)))
{
    // Will log warning if > 2 seconds
}
```

---

## ✅ ValidationResult Variants

For CLI commands and orchestrators, `ActionLoggerService` provides variants that return `ValidationResult` for all severity levels:

```csharp
return _logger.ErrorResult("Missing required input");
return _logger.SuccessResult("✓ Ready to proceed");
```

This enables pattern matching on validation output without interrupting control flow:

```csharp
var result = _logger.WarningResult("Low confidence match");
if (!result.IsValid) return result;
```

---

## 🔍 Notes

- All log methods support optional structured log output and exception escalation.
- Fully supports console-based formatting and pipeline-ready tracing.
- Prefer `Message(...)` for banner content with no prefix.
- Use `Result`-suffixed variants when control flow requires `ValidationResult`.

---

## 🧩 Dependency Injection

To use the static logger (`ActionLog.Global`), add this to your service registration:

```csharp
services.AddSingleton<IActionLoggerService, ActionLoggerService>();

var logger = services.BuildServiceProvider().GetRequiredService<IActionLoggerService>();
ActionLog.Initialize(logger);
```

You can now use it globally:

```csharp
ActionLog.Global.Info("Copilot started...");
```

> ✔️ Be sure to include `using Sandlot.ActionLogger;` at the top of any file that uses `ActionLog.Global`.
### ✅ Option 1: Use the static `ActionLog.Global` globally

Place this at the **top of your service registration**:

```csharp
services.AddSingleton<IActionLoggerService, ActionLoggerService>();
```

After building the container, initialize the global static accessor:

```csharp
using Sandlot.ActionLogger;

var provider = services.BuildServiceProvider();
var logger = provider.GetRequiredService<IActionLoggerService>();
ActionLog.Initialize(logger);
```

You can now use it globally without DI:

```csharp
ActionLog.Global.Info("Copilot started...");
```

> 💡 Don’t forget to include: `using Sandlot.ActionLogger;`

---

### ✅ Option 2: Inject the concrete `ActionLoggerService` or interface

Place this at the **top of your service registration**:

```csharp
services.AddSingleton<IActionLoggerService, ActionLoggerService>();
services.AddSingleton<ActionLoggerService>(); // Only if consuming directly
```

Then inject it wherever needed:

```csharp
public class MyService
{
    private readonly IActionLoggerService _logger;

    public MyService(IActionLoggerService logger)
    {
        _logger = logger;
    }

    public void Run()
    {
        _logger.Info("Running task...");
    }
}
```