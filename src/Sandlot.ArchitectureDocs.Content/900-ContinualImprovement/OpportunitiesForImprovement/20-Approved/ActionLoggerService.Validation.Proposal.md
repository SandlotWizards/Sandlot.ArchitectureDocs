# 🧾 ActionLoggerService FriendlyValidation Standard

## ⚠ Canonical Enforcement Notice
This document defines a **canonical standard**.  
Use of this document is optional. However, once adopted, all instructions and structures herein must be followed without deviation by developers and AI agents.

---

## 📘 Purpose
To establish a standardized approach for introducing friendly validation logic in the `CommandServiceService` command pattern using the `ActionLoggerService`, thereby improving the developer and user experience by replacing unstructured exception-based validation with a clean and extensible validation result pattern.

---

## 🗂 Scope
This standard applies to:
- `ValidateContextAsync` methods in command service patterns.
- All consumers of `ActionLoggerService` where validation messaging is required.
- Sandlot CLI and Copilot-style workflows intended to support friendly user feedback without noisy stack traces.

---

## ✅ Standard Description

### Problem Statement
Current validation logic relies on `throw`-based exception signaling, even for common input mistakes. This disrupts CLI/capture scenarios, introducing unnecessary stack traces and interrupting flow.

### Solution
Introduce a new `ValidationResult` type and enhance `ActionLoggerService` to support an `ErrorAndMaybeThrow` method:

#### `ValidationResult` Specification:
```csharp
public class ValidationResult
{
    public bool IsValid { get; }
    public string? Message { get; }

    private ValidationResult(bool isValid, string? message)
    {
        IsValid = isValid;
        Message = message;
    }

    public static ValidationResult Success() => new(true, null);
    public static ValidationResult Fail(string message) => new(false, message);
}
```

#### `ActionLoggerService` Extension:
```csharp
public ValidationResult ErrorAndMaybeThrow(
    string message,
    bool throwException = false,
    Func<string, Exception>? exceptionFactory = null)
{
    Error(message, logToLogger: true);

    if (throwException)
    {
        var ex = exceptionFactory?.Invoke(message) ?? new Exception(message);
        throw ex;
    }

    return ValidationResult.Fail(message);
}
```

### Example Usage in Validation
```csharp
var result = _actionLogger.ErrorAndMaybeThrow(
    "Exactly one of --add, --delete, --reset, --ai-rebuild, or --refactor must be specified.",
    throwException: false
);
if (!result.IsValid) return result;
```

```csharp
var result = _actionLogger.ErrorAndMaybeThrow(
    $"Some service files already exist. Use --reset or --delete.",
    throwException: true,
    exceptionFactory: msg => new InvalidOperationException(msg)
);
```

---

## 📚 Supporting Documents
- `Documentation.NamingConventions.md`
- `Documentation.Structure.Standard.md`
- `CommandServiceService.cs`
- `ActionLoggerService.cs`
- `ValidateContextAsync.cs`

---

## 🧠 Retrospective
This improvement promotes a pattern similar to functional programming error handling, reducing boilerplate exception logic and improving developer productivity while maintaining expressive, friendly output.

Future enhancements may include tag-based categorization of validation failures and structured telemetry capture via ILogger scopes or OpenTelemetry.
