# 🧱 Scaffolding Copilot Rules

## ⚠ Canonical Enforcement Notice
This document defines a **canonical standard**.  
Use of this document is optional. However, once adopted, all instructions and structures herein must be followed without deviation by developers and AI agents.

## 📘 Purpose
This standard outlines the architectural rules and behavioral principles used by the Sandlot Copilot scaffolding engine to generate projects, solutions, and their supporting artifacts in a consistent, schema-driven manner.

## 🗂 Scope
These rules apply to all project types supported by Sandlot Copilot, including but not limited to: web, infrastructure, mobileframe, cli, api, and dbcontext class libraries.

---

## 🔟 Copilot Scaffolding Rules (P01–P10)

### 🔹 P01 – Project Types are Defined by Schemas
Each project type must be defined by a standalone schema YAML file named `project.{type}.schema.yml`.

### 🔹 P02 – Solution Schema Drives Composition
The solution-level `solution.schema.yml` controls which projects are allowed, their ordering, naming format, and project-specific token overrides.

### 🔹 P03 – Tokens are Resolved per Project
Each `AllowedProject` may define its own `tokens:` block. These tokens can be injected into output filenames and template contents.

### 🔹 P04 – Includes Control Behavior
A project's schema must explicitly declare which template files to include via the `includes[]` array. The inclusion of a file implies the feature is required.

### 🔹 P05 – Templates Are External and Generic
All file templates are stored outside the Copilot engine, typically in a versioned Git repository. They are parameterized and reusable across multiple project types.

### 🔹 P06 – Packages and Project References Are Declared
Each project schema may declare:
- NuGet `packages[]` to be added
- `projectReferences[]` for internal solution dependencies

### 🔹 P07 – No Solution-Specific Assumptions
Schematics must not hardcode solution names (e.g., `SafetyManagement`). All dynamic values such as `{{SolutionName}}` must be injected via tokens.

### 🔹 P08 – Folder Layout is Schema-Driven
The `includes.output` path declares the full relative path where each file should be created. No implicit path rules are allowed.

### 🔹 P09 – All Project Artifacts Must Be Discoverable via Schema
If any file, feature, or behavior cannot be derived through naming convention or reflection, it must be declared in the schema.

### 🔹 P10 – Project-to-Project Dependencies Are Declared and Scoped
Projects may include a `dependsOn:` list that defines their internal references to other projects. This drives `ProjectReference` creation during scaffolding.

---

## 📚 Supporting Documents

- `Documentation.NamingConventions.md`
- `Documentation.Structure.Standard.md`
