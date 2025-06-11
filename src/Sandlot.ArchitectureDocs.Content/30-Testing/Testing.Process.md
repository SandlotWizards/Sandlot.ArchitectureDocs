# 🧪 Testing Process

## ⚠ Canonical Enforcement Notice

This document defines a **canonical testing process**.  
Use of this document is **mandatory** for all test suites generated within the organization.  
All instructions and structures herein must be followed without deviation by developers and AI agents.

---

## 📘 Purpose

To define the end-to-end testing strategy across all supported test types and interfaces, including unit tests, domain tests, integration tests, and CLI tests.  
It also defines how AI agents and developers collaborate to generate and validate test suites.

---

## 🗂 Scope

This process applies to all classes, objects, and services subject to formal testing in the organization’s .NET-based systems. It supports both manual and AI-assisted test generation.

---

## ✅ Steps

### ✅ Step 1: Select Entry Point  
Choose the appropriate test generation procedure:

- [`Testing.ChatGPTInterface.Procedure.md`](./Testing.ChatGPTInterface.Procedure.md) *(optional)*
- [`Testing.Copilot.Procedure.md`](./Testing.Copilot.Procedure.md) *(optional)*

Each procedure defines a detailed, step-by-step workflow for test suite generation and validation. While the procedures are optional, once selected, their rules are binding.

---

### ✅ Step 2: Apply Testing Requirements  
The following rules shall apply to all test generation efforts, regardless of the interface:

| Rule ID | Requirement                                                                 |
|---------|------------------------------------------------------------------------------|
| R01     | All public methods must have at least one test.                            |
| R02     | Constructors must be tested if they perform logic or state manipulation.    |
| R03     | Edge cases, null inputs, and boundary values must be explicitly tested.     |
| R04     | Dependencies must be mocked, faked, or isolated unless integration is intended. |
| R05     | All test suites shall use a standardized SUT factory method (e.g., `CreateSUT`). |
| R06     | Tests that can be structured using Arrange–Act–Assert **shall** follow that structure. If not feasible, the test must still be implemented using a clear, maintainable alternative. |

---

### ✅ Step 3: Developer Signoff  
All completed test suites shall be explicitly signed off by the developer:

> “To the best of my ability, I confirm that the tests adequately and correctly cover the system under test.”

**Purpose:** This signoff serves as a formal declaration of **developer ownership and accountability** for the test coverage and correctness of the system under test.

---

## 📚 Supporting Documents

- [`Testing.ChatGPTInterface.Procedure.md`](./Testing.ChatGPTInterface.Procedure.md)
- [`Testing.Copilot.Procedure.md`](./Testing.Copilot.Procedure.md)
- [`ReusableTestingPatterns.md`](./ReusableTestingPatterns.md)
- [`Documentation.Structure.Standard.md`](./Documentation.Structure.Standard.md)
- [`Documentation.NamingConventions.md`](./Documentation.NamingConventions.md)

---

## 🧠 Continuous Improvement

This process is subject to change through retrospective review and pattern discovery. Proposed updates may be initiated by developers or AI during post-test review.
