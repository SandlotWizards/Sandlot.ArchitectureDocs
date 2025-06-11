# 🧪 Testing.ChatGPTInterface.Procedure.md

## ⚠ Canonical Enforcement Notice

This document defines a **canonical testing procedure**.  
Use of this procedure is optional. However, once adopted for a given test or test suite, all instructions and structures herein must be followed without deviation by developers and AI agents.

---

## 📘 Purpose

To define the step-by-step procedure for generating and validating test suites using the ChatGPT interface.  
This procedure ensures clarity, consistency, and accountability during AI-assisted test development.

---

## 🗂 Scope

This procedure applies only when test generation is performed interactively using ChatGPT.  
It does not apply to Copilot CLI or manual test development workflows.

---

## ✅ Step-by-Step Testing Process

### ✅ Step 1: Create the Test Project and Pre-Load Classes  
**Title:** *Test Project Initialization*

**Requirement:**  
The developer shall create a test project whose name clearly indicates what is being tested. While the name does not need to follow a strict namespace pattern, it must be **unambiguous and descriptive** of the system(s) under test (SUT).

**Actions:**
- Choose a project name that clearly reflects the scope of the test (e.g., `UserServiceTests`, `SchedulerDomainTests`, `SolutionCentralCLITests`).
- Pre-load the project with the class files that require test suites.
  - Each file must represent a real system under test (SUT), not a placeholder.

---

### ✅ Step 2: Check for Missing Classes Required by AI  
**Title:** *Dependency Review and Completion*

**Requirement:**  
The AI agent shall review the contents of the test project and the pre-loaded SUT classes. It shall determine whether any **additional classes are needed** to eliminate ambiguity and assumptions during test generation.

**Actions (AI):**
- Display a table of missing required classes:

| Class Name         | Namespace                    |
|--------------------|------------------------------|
| `SomeHelper`       | `SharedKernel.Helpers`       |
| `EmployeeState`    | `HRDocuments.Domain.States`  |

- If nothing is missing, state:
  > “I have everything I need to generate a test suite for {TestClassName}. Do you wish for me to proceed?”

---

### ✅ Step 3: AI Determines and Displays Test Requirements  
**Title:** *Test Suite Requirements Preview and Confirmation*

**Requirement:**  
Before generating any test code, the AI shall analyze the SUT and identify all required test scenarios. These shall be presented in a table:

| Test Method Name                  | Description                                           |
|----------------------------------|-------------------------------------------------------|
| `ValidInput_ReturnsSuccess`      | Tests that a valid input returns a success result.   |
| `NullDependency_ThrowsException` | Tests that a null dependency causes an exception.    |

**Actions (Developer):**
- Review the table
- Confirm with:  
  > “Confirmed. Please proceed.”  
- If not confirmed, AI and developer shall resolve the discrepancy before continuing.

---

### ✅ Step 4: Generate and Display the Full Test Suite  
**Title:** *Inline Test Suite Generation*

**Requirement:**  
The AI shall generate the complete test suite with **no placeholders** and display it **fully and inline** — not zipped, not in canvas.

---

### ✅ Step 5: Developer Reviews IntelliSense Errors and Reports Them  
**Title:** *Hover, Snip, and Submit*

**Requirement:**  
The developer shall:
- Use the Windows Snipping Tool in **3–5 second delay mode**
- Hover over **squiggly-underlined IntelliSense errors** in Visual Studio
- Paste the resulting image directly into the chat

No transcription or retyping is permitted.

---

### ✅ Step 6: AI Reviews Errors, Repairs Code, and Evaluates for Pattern Inclusion  
**Title:** *Diagnose, Repair, and Learn*

**Requirement:**  
The AI shall:
- Analyze error images
- Regenerate the test suite with appropriate fixes
- Preserve all working logic unless broader rewrite is needed
- Determine if the issue is a pattern worth capturing

If yes, the AI shall state:
> “This is a candidate for inclusion in the reusable testing patterns matrix. Item is saved, pending the retrospective review.”

---

### ✅ Step 7: Repeat Until Developer Confirms Test Suite Is Valid  
**Title:** *Check-Act Loop for Test Suite Validation*

**Requirement:**  
This loop shall repeat until the developer explicitly states:

> “Confirmed — test suite is good.”

---

### ✅ Step 8: Developer Confirms Completion and Signs Off  
**Title:** *Developer Signoff and Closure*

**Requirement:**  
The developer shall confirm:

> “To the best of my ability, I confirm that the tests adequately and correctly cover the system under test.”

---

## 🔁 Looping Instructions

- The full process shall be repeated for **each class or object** requiring a test suite.
- Developer prompts next test with:  
  > “Next”

---

## 🧠 Retrospective Review and Documentation Updates  
**Title:** *Retrospective and Knowledge Capture*

**Requirement:**  
At the end of all test suites:
- AI shall present a list of:
  - All reusable pattern candidates
  - Any suggested updates to this testing process
- Developer will approve or reject inclusion in:
  - `ReusableTestingPatterns.md`
  - `Testing.Process.md`

---

## 📊 Quality Attributes Matrix

| Attribute                | Description                                                                                  | Our Process Evaluation                                                                 |
|--------------------------|----------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| **Clarity**              | The process is unambiguous and easy to follow                                               | ✅ Highly explicit, step-by-step with AI/Dev roles clearly separated                   |
| **Repeatability**        | The process yields consistent results when followed by different agents                     | ✅ Loop behavior is well defined; instructions are deterministic                       |
| **Completeness**         | All necessary steps and decisions are accounted for                                         | ✅ Includes prep, execution, validation, and retrospective                            |
| **Traceability**         | Actions and decisions are traceable to inputs and test logic                                | ✅ Test requirements are previewed and confirmed; issues are logged via screenshots    |
| **Correctability**       | Errors and gaps are caught early and fed back into the process                              | ✅ Check-act loop and error capture built in                                           |
| **Learnability**         | Process encourages improvement by capturing reusable insights                               | ✅ Includes reusable pattern recognition and retrospective feedback loop              |
| **Human–AI Collaboration** | Process explicitly coordinates AI and developer responsibilities                        | ✅ Steps alternate clearly between AI and Developer roles                              |
| **Extensibility**        | New steps or conditions can be added without rewriting the entire flow                      | ✅ Modular structure allows clean extension                                            |
| **Governance-Friendly**  | Signoff and checkpoints make it suitable for audit or compliance                            | ✅ Developer confirmation and pattern history are embedded                            |
| **Voluntary But Binding**| Can be adopted optionally, but mandates strict adherence once invoked                       | ✅ Clearly defined at the top of the document                                          |

---

## 📚 Supporting Documents

- [`Testing.Process.md`](./Testing.Process.md)
- [`ReusableTestingPatterns.md`](./ReusableTestingPatterns.md)
- [`Documentation.Structure.Standard.md`](./Documentation.Structure.Standard.md)
- [`Documentation.NamingConventions.md`](./Documentation.NamingConventions.md)