# 📘 Documentation Naming Convention

## ⚠ Canonical Enforcement Notice

This document defines a **canonical standard** for naming documentation files within the organization.  
Use of this naming convention is **mandatory** for all `.md` files representing formal documentation such as processes, procedures, standards, or references.  
All file names must conform to this structure without deviation by developers or AI agents.

---

## 📘 Purpose

To ensure consistent, descriptive, and logically structured naming for all markdown-based documentation used across systems, projects, and teams.

---

## 🗂 Scope

This standard applies to all documentation types stored in markdown format (`.md`) that are used to define canonical processes, procedures, standards, references, or retrospectives.

---

## ✅ Format

```
{Subject}.{Context}.{Type}.md
```

---

## ✅ Components

| Part       | Description                                                                 |
|------------|-----------------------------------------------------------------------------|
| `Subject`  | The main topic or domain (e.g., `Testing`, `SolutionCentral`, `Scheduler`) |
| `Context`  | The scope or interface layer involved (e.g., `ChatGPTInterface`, `CLI`)     |
| `Type`     | The kind of document (e.g., `Procedure`, `Reference`, `Retrospective`)     |

---

## ✅ Style Rules

- Use **PascalCase** for all parts.
- Use **dots (.)** for logical segmentation — not slashes or dashes.
- Use **`.md`** as the file extension.
- Avoid redundant or overly generic labels like `Doc`, `Notes`, or `Info`.

---

## ✅ Examples

| Valid File Name                         | Description                                             |
|----------------------------------------|---------------------------------------------------------|
| `Testing.ChatGPTInterface.Procedure.md` | Canonical test generation process for ChatGPT agents    |
| `SolutionCentral.CLI.Procedure.md`      | Canonical orchestration behavior for CLI interaction    |
| `Scheduler.Domain.Rules.md`             | Domain-specific business rule definitions               |
| `Testing.Retrospective.Notes.md`        | Retrospective notes from completed testing sessions     |

---

## 🧠 Continuous Improvement

This naming convention is subject to periodic review and refinement to support evolving architecture and documentation standards.