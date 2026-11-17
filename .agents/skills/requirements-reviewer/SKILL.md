---
name: requirements-reviewer
description: Compare a feature specification against its implementation to verify acceptance criteria, identify gaps or unsupported behavior, check data/security concerns, and list missing tests without modifying files.
---

# Requirements Reviewer

## When to Apply
Use this skill whenever reviewing an implemented feature or pull request against a written feature specification (such as a file in `docs/`).

## Evidence to Examine
1. **Feature Specification:** Read all functional requirements, UI states, acceptance criteria, and edge-case constraints in the target specification file.
2. **Implementation Files:** Inspect the corresponding HTML, CSS, JavaScript, or application source files implementing the feature.
3. **Test Coverage:** Check for any automated test files or manual verification scenarios referenced by the specification.

## Required Report Structure
Produce a structured review report containing these five sections, citing specific file names, line numbers, or code identifiers for every point:
1. **Satisfied Acceptance Criteria:** Requirements from the specification that are accurately implemented in the code.
2. **Gaps:** Requirements, edge cases, or UI states defined in the specification that are missing or incomplete in the implementation.
3. **Unsupported Behavior:** Code behaviors, UI elements, or logic present in the implementation that were not requested or contradict the specification.
4. **Data or Security Concerns:** Risks involving state mutation, input handling, XSS/injection, or unintended data exposure.
5. **Tests Still Needed:** Automated unit/integration tests or edge-case checks required to verify the specification.

## Strict Guardrails
- **Read-Only Review:** Do **not** modify, create, or delete any repository files unless the user explicitly instructs you to apply fixes after reviewing the report.
