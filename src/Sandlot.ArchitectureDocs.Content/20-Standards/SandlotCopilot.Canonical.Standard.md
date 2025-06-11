# SandlotCopilot.Conanical.Standard.md

This document defines the core development standards and AI behavioral expectations for the Sandlot Copilot platform. It is used by both human developers and AI agents during all scaffolded or injected logic operations.

## 📌 Purpose

Ensure consistency, maintainability, and architectural clarity across all generated logic in the following contexts:
- Command Services
- Razor Components
- Worker Consumers
- Utility Services
- Repository and Deployment Operations

Unless explicitly overridden by a `design.md` file or domain-specific standard, these rules must be followed by all AI logic processors.

---

## 1. Code Structure & Method Design

- All business logic should reside in **partial class methods**
- Each partial method must fulfill **a single responsibility**
- The orchestrator file (e.g. `MyService.cs`) is responsible only for:
  - Constructor
  - DI wiring
  - Coordinating partial method calls

- The partial method filename must **exactly match the method name** (e.g. `ExecuteAsync.cs` → `ExecuteAsync`)

---

## 2. Injection Markers

- AI-generated logic must replace code inside:
  ```csharp
  // <copilot:inject name="ExecuteCoreLogic" mode="replace">
  // </copilot:inject>
  ```
- All injections must respect the boundaries of the named block
- AI must not touch code outside these blocks

---

## 3. Logging & Developer Feedback

- Use `_logger.BeginStep(...)` for outer scope logging
- Use `_logger.Success(...)`, `.Warning(...)`, or `.Error(...)` to report results
- Never use `Console.WriteLine`

---

## 4. Validation & Early Exits

- Perform null/empty/path existence checks early
- Avoid `try/catch` where validation suffices
- All validation methods should be placed in `ValidateContextAsync`

---

## 5. Naming Conventions

- Method names: `PascalCase`
- Variables: `camelCase`
- Parameters:
  - Use `request` for input model
  - Use `ct` for `CancellationToken`

---

## 6. AI Writing Style

- Clear and readable C#
- Prefer verbosity over cleverness
- All async methods return `Task` or `Task<T>`
- Use `await Task.CompletedTask` if logic is empty but required

---

## 7. Dependency Usage

- Use injected services only:
  - `_fileSystem` → file and directory access
  - `_shell` → git or OS command execution
  - `_logger` → structured logging
- Do not create new `HttpClient`, `StreamReader`, etc.

---

## 8. AI Obedience and Override Rules

- `standard.md` is the default authority
- `design.md` may override any standard explicitly
- AI must favor clarity and consistency over innovation

---

## 9. Sensitive Data

- Never log or echo tokens, credentials, or secrets
- Never hardcode sensitive values in generated code
- Prefer `IConfiguration` or DI-bound secrets

---

## ✅ Summary

This standard serves as the foundational agreement between the developer and the assistant. All generated logic must adhere to these patterns unless told explicitly otherwise. It is a living document and will evolve as Sandlot Copilot grows.