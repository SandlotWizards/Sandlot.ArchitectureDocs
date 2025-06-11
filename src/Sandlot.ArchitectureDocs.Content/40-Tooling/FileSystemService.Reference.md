# 📘 FileSystemService Reference

## 📘 Purpose

This document serves as a practical **developer reference** for using the `FileSystemService` in both development and deployment contexts.
It supplements the formal standards by providing examples, guidance, and rationale for typical usage scenarios.

---

## 🧭 Developer Usage (IDeveloperFileSystemService)

### 🔹 Locate Developer Paths

```csharp
// Get base developer repo folder
var root = fileSystem.GetDeveloperRootPath();

// Get full path to a solution
var solutionPath = fileSystem.LocateDeveloperSolutionPath("SolutionCentral");

// Get path to the /src folder inside a solution
var dotnetRoot = fileSystem.LocateDeveloperDotNetRoot("SolutionCentral");

// Get path to a specific project
var projectPath = fileSystem.LocateDeveloperProjectPath("SolutionCentral", "SolutionCentral.Core");

// Get canonical path to ArchitectureDocs.Content
var archDocs = fileSystem.GetArchitectureDocsPath();
```

* Default root: `%USERPROFILE%\source\repos`
* Override with optional `rootOverride` param
* Project path assumes `src/` layout

---

## 🚀 Deployment Usage (IDeploymentFileSystemService)

### 🔹 Locate Deployment Repo Paths

```csharp
// Locate deployment root for localhost
var root = fileSystem.LocateDeploymentRepoPath("localhost", "Testing");

// Locate solution within environment
var solutionPath = fileSystem.LocateDeploymentRepoPath("localhost", "SolutionCentral", "Testing");

// Locate project within solution
var projectPath = fileSystem.LocateDeploymentRepoPath("localhost", "SolutionCentral", "SolutionCentral.Core", "Testing");
```

* `profile` is **required** for `localhost`
* `profile` is **not used** for GitHub runner deployments

---

## 🧰 Filesystem Helper Methods

All interfaces expose the following helper methods:

```csharp
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
```

These provide safe, predictable, and testable wrappers around the standard `System.IO` APIs.

---

## 🧠 Hints for Developer Success

* Use `IDeveloperFileSystemService` for local tools, scaffolds, and CLI development
* Use `IDeploymentFileSystemService` in build pipelines, runners, and deployment agents
* Inject a single implementation (`FileSystemService`) but code to the correct interface

---

## 📚 Supporting Documents

* [FileSystem.Standard.md](./FileSystem.Standard.md)
* [FileSystemService.Standard.md](./FileSystemService.Standard.md)
