# 📘 ActionLoggerService Standard

## ⚠ Canonical Enforcement Notice

This document defines the canonical behavior of the `ActionLoggerService` within the Sandlot platform.
Any implementation or use must adhere strictly to the methods, patterns, and telemetry behaviors described.

---

## 📘 Purpose

To establish a structured, traceable, and telemetry-aware logging system for developer workflows, AI pipelines, build orchestration, and CLI tooling within Sandlot.

---

## 🗂 Scope

This applies to:
- All CLI commands and services using `ActionLoggerService`
- Logging of developer or automation activities
- Any structured operation benefiting from observability

---

## 🔧 Interfaces and Responsibilities

### ✳️ `IActionLoggerService`

```csharp
public interface IActionLoggerService
{
    IDisposable BeginStep(string title, TimeSpan? threshold = null, bool logToLogger = false);
    string Trace(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    string Debug(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    string Info(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    string Warning(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    string Error(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    string Critical(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    string Success(string message = "✔ Done", bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = false);
    string Message(string message, ConsoleColor color = ConsoleColor.Gray, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = false);
    void PrintHeader(ConsoleColor color = ConsoleColor.Gray);
    void PrintTrailer(ConsoleColor color = ConsoleColor.Gray);

    // ValidationResult variants
    ValidationResult TraceResult(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    ValidationResult DebugResult(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    ValidationResult InfoResult(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    ValidationResult WarningResult(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    ValidationResult ErrorResult(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    ValidationResult CriticalResult(string message, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = true);
    ValidationResult SuccessResult(string message = "✔ Done", bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = false);
    ValidationResult MessageResult(string message, ConsoleColor color = ConsoleColor.Gray, bool throwException = false, Func<string, Exception>? exceptionFactory = null, bool logToLogger = false);
}
```

---

## 💡 Logging Conventions

| Method     | Purpose                         | Prefix        | Console Color |
|------------|----------------------------------|----------------|----------------|
| Trace      | Detailed diagnostics             | `[trace]`      | Cyan           |
| Debug      | Debugging output                 | `[dbg]`        | DarkGray       |
| Info       | General operations               | `⟳`            | Gray           |
| Warning    | Non-critical problems            | `⚠️`            | Yellow         |
| Error      | Errors, validation failures      | `❌`            | Red            |
| Critical   | Severe issues                    | `🔥`            | Red            |
| Success    | Completion notice                | `✔` (default)  | Green          |
| Message    | Symbol-free messages             | (none)         | Configurable   |

---

## ✅ ValidationResult Integration

Each logging method has a corresponding `ValidationResult`-returning variant. These methods allow error reporting while preserving control flow for downstream logic, such as:

```csharp
var result = _logger.WarningResult("Insufficient metadata");
if (!result.IsValid) return result;
```

They return either `ValidationResult.Fail(...)` or `ValidationResult.Success()`, based on severity.

---

## 🎯 Telemetry Integration

- Each `BeginStep()` triggers an `ActivitySource` span.
- Steps log duration and status (warning if threshold exceeded).
- Exception throwing is available on every log type.
- Optional logger injection supports structured storage (e.g., Serilog).

---

## 🧠 Continuous Improvement

This logger standard enables composable observability with zero external dependencies.
Refinements should be backward-compatible and align with telemetry ecosystems like OpenTelemetry.