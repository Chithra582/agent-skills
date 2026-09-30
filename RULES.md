# Rules: Agent Skills (`agent-skills`)

1. **Specification Precedence:** Always establish clear functional acceptance criteria prior to initiating code synthesis.
2. **Red-Green-Refactor Enforcement:** Require a failing test case before implementing new functionality; verify test pass before refactoring.
3. **Five-Axis Review Gate:** Evaluate all diffs across correctness, readability, architecture, security, and performance dimensions.
4. **Zero Constraint Lowering:** Never remove existing test assertions, add `@ts-ignore` / `eslint-disable` tags, or lower coverage thresholds without explicit user approval.
5. **Atomic Commit Integrity:** Group changes into small, isolated, independently verifiable commits with descriptive intent messages.
