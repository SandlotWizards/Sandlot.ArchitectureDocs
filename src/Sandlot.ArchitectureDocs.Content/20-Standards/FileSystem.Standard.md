# 📘 FileSystem Standard

## ⚠ Canonical Enforcement Notice

This document defines a **canonical standard** for file system layout and resolution in the Sandlot ecosystem.  
All folder structures, resolution logic, and conventions herein must be followed without deviation by developers and AI agents.

---

## 📘 Purpose

To define consistent patterns for resolving file system paths across all developer and deployment environments in Sandlot.

This standard governs where solutions are stored, how environments are structured, and what inputs are required to locate or manipulate solution content.

---

## 🗂 Scope

This applies to all Sandlot tooling, automation agents, deployment systems, and developer-side utilities that:
- Reference solution repositories
- Operate on file system structure
- Deploy or scaffold environments

---

## 🧭 Deployment Layouts

### 🔹 Localhost Deployment
```
C:\Solution_Deployments\
  └── localhost\
      └── LocalProfiles\
          └── {profile}\
              ├── Solutions\
              └── Deployment\
```
- Profile is **required**
- Used for local development and isolated testing

### 🔹 GitHub Self-Hosted Runner Deployment
```
C:\Solution_Deployments\
  └── {Organization}\
      └── Environments\
          └── {EnvironmentRepo}\
              ├── Solutions\
              └── {repo_lowercase}\
```
- Profile is **not used**
- Structure mirrors GitHub organization/repo context

---

## 🧭 Developer Repository Structure

```
%USERPROFILE%\source\repos\
  └── {solution}\
      └── src\
          └── {project}
```
- This is the default unless overridden
- Intended only for **developer usage**

---

## 🧩 Resolution Rules

| Input Parameters     | Environment     | Profile Required | Notes                             |
|----------------------|------------------|------------------|------------------------------------|
| `--environment=localhost` | Localhost        | ✅ Yes           | `profile` is mandatory             |
| `--environment=STAGING_POOL_1` | GitHub Runner   | ❌ No            | Inferred from GitHub context       |
| None                 | Developer        | ❌ No            | Defaults to `%USERPROFILE%` layout |

---

## 🧠 Continuous Improvement

This standard shall be reviewed and updated as new deployment modes or architectural patterns emerge.