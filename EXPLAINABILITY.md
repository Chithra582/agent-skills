# EXPLAINABILITY — Agent Skills

> **Admissibility & Transparency Report for OpenGAP / Agent Passport**  
> *Agent Name:* Agent Skills (`agent-skills`)  
> *Specification:* OpenGAP v0.1.0  
> *Domain:* Developer Tools / Autonomous Engineering Quality Gates & Agent Skills Runtime  

---

## 1. Overview & Operational Purpose

The **Agent Skills** system (`agent-skills`) is an autonomous software engineering quality-gate and methodology framework designed for AI coding agents. Created to package battle-tested engineering practices into modular, machine-executable skills, the agent guides projects across the entire software development lifecycle: from requirement specification (`/spec`), atomic planning (`/plan`), and test-driven implementation (`/build`), to multi-axis code reviews (`/review`), constraint verification (`CONSTRAINTS.md`), and web performance optimization (`/webperf`).

The agent's primary operational purpose is to enforce deterministic quality gates, preventing autonomous models from lowering code health, skipping tests, or introducing architectural regressions during rapid software development cycles.

---

## 2. How the Agent Decides (Decision-Making Logic)

Agent Skills operates across a deterministic, multi-stage engineering decision pipeline that grounds every implementation step in verifiable quality contracts:

```
[User Slash Command / Prompt] ──> [Specification & Readiness Gate] ──> [Atomic Task Planner]
                                                                                     │
                                                                                     ▼
[Five-Axis Review & Merge Gate] <── [Test-Driven Refactor Proof] <── [Slice Implementation Loop]
```

### 2.1 Specification & Requirement Discovery
- **Decision:** Determines whether a user request has sufficient clarity to proceed to planning or requires requirement interrogation.
- **Rules:**
  - Evaluates user prompt against requirement readiness criteria (problem statement, user persona, edge cases, acceptance criteria).
  - Triggers interactive single-question interviews (`/spec` / `interview-me`) if core parameters or non-goals are underspecified.
  - Generates structured PRD documentation before authorizing implementation phases.

### 2.2 Atomic Task Decomposition & Sequencing
- **Decision:** Breaks high-level requirements into small, independently verifiable implementation units.
- **Rules:**
  - Enforces atomic sizing: each planned task must touch minimal files and take under 15 minutes of agent work.
  - Sequences tasks with strict dependency ordering (type contracts -> domain models -> business logic -> UI components).
  - Pairs every task with an explicit verification command (unit test, curl command, or linter check).

### 2.3 Test-Driven Implementation & Refactoring Gates
- **Decision:** Dictates when code modifications can be committed to the working branch.
- **Rules:**
  - Strictly requires a failing test reproducing the target behavior before code synthesis begins.
  - Implements minimal code required to transition tests from red to green.
  - Disallows modifying or deleting existing tests without explicit human confirmation.

### 2.4 Five-Axis Code Review & Merge Gatekeeping
- **Decision:** Approves or blocks proposed changes prior to merging into main branches.
- **Rules:**
  - Reviews candidate diffs across five explicit axes: Correctness, Readability, Architecture, Security, and Performance.
  - Categorizes findings with severity tags (`[Critical]`, `[Required]`, `[Suggestion]`).
  - Mandates resolution of all `[Critical]` and `[Required]` findings before merge authorization.

---

## 3. Data Sources & Inputs Used

| Data Input | Source | Purpose | Data Handling & Privacy |
|---|---|---|---|
| **Interactive User Prompts & Slash Commands** | Terminal CLI / IDE Chat input | Captures developer feature intents and commands | Kept in local session context |
| **Repository Source Code & Diff Trees** | Local git workspace on host disk | Analyzes code structure, types, and modified lines | Analyzed in-place, zero external storage |
| **Project Constraints & Configuration** | `CONSTRAINTS.md`, `package.json`, linter configs | Reads quality thresholds and stack dependencies | Evaluated deterministically against local diffs |
| **Test Execution & Linter Results** | Local runtime test runners (vitest, jest, eslint) | Proves implementation correctness and style health | Captured via process stdout/stderr |

Agent Skills complies with operational security and privacy standards:
- **No Cloud Data Exfiltration:** Source code, test scripts, and diff artifacts remain strictly on the host workstation.
- **Zero Suppression Policy:** Automated diff inspection blocks suppression flags (`--no-verify`, `skip-tests`, `@ts-nocheck`) from reaching production branches.
- **Atomic Rollback Capability:** Implementations are committed task-by-task; failed slices can be reverted independently without loss of previous progress.
- **Human Governance Primacy:** The developer holds full authority over PRD approvals, constraint thresholds, and merge permissions.

---

## 4. Known Limitations & Failure Modes

Reviewers, auditors, and users should note the following operational constraints:

1. **Underspecified User Prompts:**
   - *Limitation:* Vague requirements can lead to speculative architecture choices.
   - *Mitigation:* Interactive single-question interrogation loop (`interview-me`) to clarify ambiguous requirements before coding.

2. **Flaky or Non-Deterministic Test Suites:**
   - *Limitation:* Timing-dependent tests can cause false negative verification gates.
   - *Mitigation:* Multiple test retry runs and isolation of non-deterministic async test cases.

3. **Silent Threshold Degradation:**
   - *Limitation:* Autonomous agents may attempt to silence linters with suppression comments to pass checks.
   - *Mitigation:* Explicit constraint scanning that rejects `@ts-ignore` or `eslint-disable` additions in diffs.

4. **Context Window Exhaustion on Large Monorepos:**
   - *Limitation:* Loading extensive repositories into context can exceed token budgets.
   - *Mitigation:* Modular skill loading, file-specific scoping, and targeted context engineering.

---

## 5. Verification, Safety & Human Oversight

- **Real-Time Human Approval Gate:** Agents require explicit user sign-off on generated PRDs and task breakdown plans before writing code.
- **Emergency Session Interrupt:** Developers can interrupt any autonomous implementation or test loop immediately via standard process signals.
- **Step Quota Guardrails:** Autonomous task runs (`/build auto`) are bounded by explicit task limits ($N \le 10$ steps) to prevent runaway execution.
- **Structured Audit Logging:** Every executed review finding, test result, and constraint violation is preserved in structured audit logs.
