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

## 🔍 Notes

- All log methods support optional structured log output and exception escalation.
- Fully supports console-based formatting and pipeline-ready tracing.
- Prefer `Message(...)` for banner content with no prefix.
---

## 🧩 Dependency Injection

To register `ActionLoggerService` for use throughout your application:

```csharp
services.AddSingleton<IActionLoggerService, ActionLoggerService>();
```

To make the global logger available via static access (optional):

```csharp
var logger = services.BuildServiceProvider().GetRequiredService<IActionLoggerService>();
ActionLogger.Initialize(logger);
```

Once registered, `ActionLogger.Global` can be used anywhere without direct constructor injection:

```csharp
ActionLogger.Global.Info("Copilot started...");
```
