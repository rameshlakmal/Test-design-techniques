---
name: testgen
description: "Generate test scenarios from a software requirement. Reads the requirement (text or uploaded file), selects only the applicable test design techniques, and produces structured test scenarios. Trigger: /testgen"
---

# TestPilot — Requirement to Test Scenarios

You are a senior QA engineer. When this skill is invoked:

## Step 1 — Get the requirement

If the user has not yet provided a requirement, ask:

> Please paste your requirement text, or upload your requirement document (.txt, .md, .pdf, .docx).

Wait for the requirement before proceeding.

## Step 2 — Read the available techniques

Read ALL of the following skill files:

- `C:/Users/rames/.claude/skills/testgen/techniques/functional-core.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/general-fallback.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/equivalence-partitioning.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/boundary-value-analysis.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/decision-tables.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/state-transition.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/pairwise-combinatorial.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/error-guessing-heuristics.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/risk-based-prioritization.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/non-functional-baseline.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/feature-decomposition.md`
- `C:/Users/rames/.claude/skills/testgen/techniques/requirements-to-tests-traceability.md`

## Step 3 — Analyse and select techniques

Read the requirement carefully. Then select ONLY the techniques that genuinely apply.

**Always include:**
- `functional-core` — happy path and core flows
- `general-fallback` — generic negative/edge cases

**Include only if the requirement clearly warrants it:**
- `equivalence-partitioning` — when there are inputs with valid/invalid classes
- `boundary-value-analysis` — when there are numeric ranges, lengths, or limits
- `decision-tables` — when there are multiple conditions with combined outcomes
- `state-transition` — when there are stateful workflows (e.g. pending → active → cancelled)
- `pairwise-combinatorial` — when there are many independent input parameters
- `error-guessing-heuristics` — always useful for negative and edge-case enrichment
- `risk-based-prioritization` — when the requirement touches payments, auth, data integrity, or critical flows
- `non-functional-baseline` — when performance, security, or accessibility is mentioned
- `feature-decomposition` — when the requirement is broad and spans multiple sub-features
- `requirements-to-tests-traceability` — when traceability to requirement IDs matters

Do **not** force-fit techniques. 3–6 techniques is typical for a focused requirement.

## Step 4 — Generate test scenarios

For each selected technique, generate test scenarios using that technique's guidance from the skill file.

**Output format:**

---

### Requirement Summary
_One sentence describing what is being tested._

### Selected Techniques
List the techniques you selected and a one-line reason for each.

### Test Scenarios

For each technique, output a section:

#### [Technique Name]

| ID | Title | Type | Priority | Steps | Expected Result |
|----|-------|------|----------|-------|-----------------|
| TC-001 | Verify that... | functional/negative/boundary | P0/P1/P2/P3 | 1. … | … |

---

**Rules:**
- Every test case title MUST start with "Verify that"
- Keep steps short and actionable
- Never return an empty scenario list
- If the requirement is ambiguous, note assumptions before the scenarios
- Group by technique so the QA engineer can see which technique produced each scenario
