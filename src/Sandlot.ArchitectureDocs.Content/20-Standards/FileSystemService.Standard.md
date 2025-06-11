# 📘 FileSystemService Standard

## ⚠ Canonical Enforcement Notice

This document defines a **canonical standard** for the Sandlot `FileSystemService`.
All instructions and structures herein must be followed without deviation by developers and AI agents.

---

## 📘 Purpose

To standardize the behavior and interface of the `FileSystemService` used within the Sandlot ecosystem, supporting both **developer workstations** and **deployment environments** (including self-hosted GitHub runners).

This service is intended to simplify filesystem interactions, provide clear access to solution and project directories, and expose safe wrappers around common file/directory operations.

---

## 🗂 Scope

This standard applies to all .NET applications, tools, and services that need to resolve:

* Local developer repository paths (e.g., `%USERPROFILE%\source\repos`)
* Deployment paths (e.g., `C:\Solution_Deployments`)
* GitHub self-hosted runner environments
* Filesystem utility operations (read, write, delete, exists, etc.)

---

## 🔧 Interfaces and Responsibilities

### 👩‍💻 IDeveloperFileSystemService

Used by local tools and CLI commands in a **developer context**.

```csharp
public interface IDeveloperFileSystemService
{
    string GetDeveloperRootPath(string? rootOverride = null);
    string LocateDeveloperSolutionPath(string solution, string? rootOverride = null);
    string LocateDeveloperDotNetRoot(string solution, string? rootOverride = null);
    string LocateDeveloperProjectPath(string solution, string project, string? rootOverride = null);
    string GetArchitectureDocsPath(string? rootOverride = null);

    bool DirectoryExists(string path);
    void CreateDirectory(string path);
    void DeleteDirectory(string path, bool recursive = true);
    void EmptyDirectory(string path);

    bool FileExists(string path);
    void WriteFile(string path, string content, bool append = false);
    string ReadFile(string path);
    void DeleteFile(string path);
    void CopyFile(string source, string destination, bool overwrite = true);
    void MoveFile(string source, string destination, bool overwrite = true);
}
```

#### 🧠 Notes:

* Default developer repo path: `%USERPROFILE%\source\repos`
* All methods accept optional override
* Project paths assume `src/` subfolder convention

---

### 🚀 IDeploymentFileSystemService

Used by CLI commands, GitHub runners, and deployment orchestration.

```csharp
public interface IDeploymentFileSystemService
{
    string LocateDeploymentRepoPath(string environment, string? profile = null);
    string LocateDeploymentRepoPath(string environment, string solution, string? profile = null);
    string LocateDeploymentRepoPath(string environment, string solution, string project, string? profile = null);

    bool DirectoryExists(string path);
    void CreateDirectory(string path);
    void DeleteDirectory(string path, bool recursive = true);
    void EmptyDirectory(string path);

    bool FileExists(string path);
    void WriteFile(string path, string content, bool append = false);
    string ReadFile(string path);
    void DeleteFile(string path);
    void CopyFile(string source, string destination, bool overwrite = true);
    void MoveFile(string source, string destination, bool overwrite = true);
}
```

#### 🧠 Notes:

* Canonical root: `C:\Solution_Deployments`
* `--environment` is required
* `--profile` is required only for `localhost`
* GitHub runners use self-hosted Windows machines and derive structure from GitHub repo context

---

## 📁 Resolution Summary

| Context          | Method Base                     | Root Path (Default)                              | Profile Needed? |
| ---------------- | ------------------------------- | ------------------------------------------------ | --------------- |
| Developer        | `GetDeveloperRootPath`          | `%USERPROFILE%\source\repos`                     | ❌ No            |
| Developer        | `LocateDeveloperSolutionPath`   | `%USERPROFILE%\source\repos\{solution}`          | ❌ No            |
| Developer        | `LocateDeveloperDotNetRoot`     | `%USERPROFILE%\source\repos\{solution}\src`      | ❌ No            |
| Localhost Deploy | `LocateDeploymentRepoPath(...)` | `C:\Solution_Deployments\localhost\...`          | ✅ Yes           |
| GitHub Runner    | `LocateDeploymentRepoPath(...)` | `C:\Solution_Deployments\{org}\Environments\...` | ❌ No            |

---

## 🧠 Continuous Improvement

This standard shall be reviewed periodically to account for new environments, evolving repo structures, or platform transitions. Proposed changes should be submitted via pull request to the documentation repository.
