---
name: plan-from-issue
description: Reviews a spec directory's ISSUE.md against the actual codebase and produces PLAN.md. Verifies the issue's claims, reviews as a security analyst, software engineer, and cloud engineer, finds gaps, recommends hardening and spin-off issues, and puts clarifying questions with options and a recommendation at the end of PLAN.md. Iterates with the user until every question is answered and locked, then hands off to requirements.md. Use when asked to plan, review, triage, or analyze an ISSUE.md, to start or continue a PLAN.md in a specs directory, or to work through open questions in PLAN.md before writing requirements.
metadata:
  inputs: spec directory containing ISSUE.md
  output: PLAN.md in the same directory
---

# Plan from ISSUE.md

Turn an `ISSUE.md` into a reviewed, well-architected `PLAN.md` that the user and agent refine together until every open question is answered and locked. This skill stops at a locked plan. It does not write `requirements.md`, `design.md`, or `tasks.md`, and it does not create or edit `ISSUE.md`.

## Ground rules

- Read-only on the codebase. The only file this skill writes is `PLAN.md` in the spec directory.
- Treat `ISSUE.md` as a set of claims, not facts. It may be imported from Jira or GitHub, may be stale, and may have been written without full knowledge of the code.
- Never dismiss a reported problem because the code "looks fine". If it cannot be confirmed by reading, mark it "needs runtime verification" and keep it in the plan.
- Cite evidence as `path:line` (or `path` plus symbol). A claim with no citation is an assumption and must be labeled one.
- Fit the fix into the existing structure and conventions. Do not propose new frameworks, services, or layers when an existing pattern covers it.
- Verify AWS and library specifics (API parameters, limits, IAM actions, behavior) against current documentation rather than memory. State uncertainty when it cannot be confirmed.
- Run only read-only probes. Ask before anything that touches live infrastructure, sends traffic to a deployed stage, or costs money.

## Step 0: Locate the spec and pick a mode

1. Resolve the spec directory from the user's argument, else from the active or open editor files, else ask.
2. Confirm `ISSUE.md` exists there. If not, stop and say so (a different skill produces it).
3. Choose the mode:
   - No `PLAN.md`: **new plan**, go to Step 1.
   - `PLAN.md` exists with open or answered-but-unprocessed questions: **iterate**, go to Step 6.
   - `PLAN.md` exists and is marked Locked: report that it is locked and ask whether to reopen it.

## Step 1: Ground in the project

Read, in this order, whatever exists. Skip what does not.

- `AGENTS.md`, `README.md`, `ARCHITECTURE.md`, `DEPLOYMENT.md`, `CONTRIBUTING.md`, `SECURITY.md`
- Steering and rules in `.kiro/steering/`, and skills in `.kiro/skills/`
- `CHANGELOG.md` (current unreleased version and recent entries)
- Sibling specs in `.kiro/specs/` that touch the same area, and any `PLAN.md` or `design.md` they contain
- `git log` and `git blame` for the files the issue implicates, to learn why the current code is the way it is. Earlier fixes are often deliberate and must not be regressed.

Capture the constraints that apply: naming conventions, IAM policy rules, deployment model, test framework, branching model, what must not be modified (for example upstream templates), and documentation that must be kept in sync.

## Step 2: Extract and verify the issue's claims

1. List every distinct assertion in `ISSUE.md`: symptoms, root-cause statements, file and line references, behavior of external services, proposed fixes, and stated impact.
2. Check each against the current code and configuration. Note the commit the issue was checked against and whether the code has moved since.
3. Record a verdict per claim:
   - **Confirmed**: evidence found, cited.
   - **Partially confirmed**: true with caveats, or true in some paths only.
   - **Not confirmed**: contradicted by the code, with evidence.
   - **Unverifiable by reading**: needs a runtime check. Say exactly what check.
4. Look for what the issue does not say: other callers of the same code, other code paths with the same flaw, duplicated logic, and tests that encode the current behavior and will need to change.

## Step 3: Review through three lenses

Apply each lens in full, even when the issue seems to belong to only one.

**Security analyst**
- Trust boundaries: which inputs are attacker-controlled, and where is that assumed otherwise?
- Abuse and bypass: authentication, authorization, rate limiting, input validation, injection, SSRF, path traversal, enumeration.
- Data exposure: secrets, PII, and sensitive values in logs, errors, responses, and caches.
- Fail-open versus fail-closed behavior on errors and missing configuration.
- IAM scope of anything touched, and whether least privilege holds with the change.
- Disclosure: if the issue describes an exploitable weakness, note whether the spec directory is published, and flag how the ISSUE and PLAN text should be handled before the fix ships.

**Software engineer**
- Correctness and edge cases, including empty, malformed, concurrent, and boundary inputs.
- Fit with existing patterns, modules, and naming. Duplicate implementations that should become one.
- Backward compatibility and migration of stored data or public contracts.
- Testability: which existing tests change, which are missing, where property-based tests fit.
- Maintainability, dependency footprint, and documentation that must be updated.

**Cloud engineer**
- Where the change lands in the deployed topology (edge, API layer, compute, data, async). What does each hop actually do to the request?
- Infrastructure-as-code impact: template changes, parameters, conditions, replacement versus in-place updates, stack boundaries owned elsewhere.
- IAM, KMS, and resource policy changes, with least privilege.
- Behavior across stages (test, beta, prod): config drift, logging levels, alarms, gradual deployment.
- Cost, scaling, quotas, and throttling. Observability: logs, metrics, alarms, tracing. Rollout and rollback.
- Operational runbook and deployment-pipeline implications.

## Step 4: Find gaps and tangential improvements

- List gaps: missing information, unstated assumptions, contradictions inside the issue, and decisions the issue defers.
- List tangential problems found while reading the code. Classify each:
  - **Include**: small, low risk, and makes this change safe or robust. It stays in scope.
  - **Spin off**: valuable but separable. Recommend a separate issue and let the user confirm. Never silently expand scope.
  - **Note only**: worth knowing, no action proposed.
- Give each item a one-line rationale and an effort and risk estimate (S/M/L).

## Step 5: Write PLAN.md

Write `<spec-dir>/PLAN.md` with the structure below. Keep it specific to the project and evidence-backed. Prefer tables for verdicts and options, and prose for reasoning.

````markdown
# <Title taken from the issue>

> **Status**: Draft, N open questions
> **Issue**: [ISSUE.md](ISSUE.md)
> **Reviewed against**: <branch> at <short commit> on <date>

## 1. Summary
What is wrong or wanted, who is affected, and the shape of the recommended fix, in a short paragraph.

## 2. Assessment of the issue
| # | Claim | Verdict | Evidence |
|---|-------|---------|----------|

Include "needs runtime verification" items and exactly how to verify them.

## 3. Current state
Relevant architecture, code paths, and prior decisions, with citations. Include why the current behavior exists.

## 4. Review
### 4.1 Security
### 4.2 Software engineering
### 4.3 Cloud engineering

## 5. Gaps and observations
Missing information, assumptions, contradictions, and affected tests and docs.

## 6. Proposed approach
The recommended design at plan level, with the alternatives considered and why they were not chosen. Mark parts that depend on open questions as "pending Q#".

## 7. Related improvements
| Item | Class (Include / Spin off / Note) | Rationale | Effort | Risk |
|------|-----------------------------------|-----------|--------|------|

## 8. Risks and mitigations
| Risk | Mitigation |
|------|------------|

## 9. Locked decisions
| # | Decision | Rationale |
|---|----------|-----------|

## 10. Open questions and recommendations
(Always the last section. The user answers here.)

### Q1. <Short title>
**Why it matters:** <what depends on this>
**Options:**
- **A. <option>**: <what it means, pros, cons>
- **B. <option>**: <what it means, pros, cons>
- **C. Other**: describe
**Recommendation:** <option>, because <reasoning tied to this codebase>.
**Answer:** _pending_
````

Question rules:
- Ask only what the code, docs, and git history cannot answer. Anything answerable by investigation gets investigated, not asked.
- Every question has at least two real options plus a recommendation with reasoning. Include "Other" so the user can redirect.
- Order by dependency: questions that unlock others come first. Group spin-off confirmations together at the end.
- Keep each question answerable in a sentence ("A", "go with recommendation", or a short override).
- Number questions once and never renumber. New questions continue the sequence.

After writing, tell the user where `PLAN.md` is, give a three-line summary of the headline findings, state the number of open questions, and ask them to fill in the `Answer:` lines. Then stop and wait.

## Step 6: Iterate until locked

When the user returns with answers (inline in `PLAN.md` or in chat):

1. Re-read `PLAN.md` first, since the user may have edited it.
2. For each answered question:
   - "Go with recommendation" or a bare option letter means adopt it.
   - Move it to **Locked decisions** with the chosen option and rationale, keeping the question number. Remove it from the open list or mark it `Answered, see Decision N`.
3. Propagate. Update every affected section (assessment, approach, related improvements, risks), not just the decision table.
4. Re-run the three-lens review on the consequences of the answers. Raise a **new** question when an answer:
   - conflicts with another decision or with a project constraint,
   - weakens security or operability (state the concern and offer a safer option, and do not silently override the user),
   - opens a gap that did not exist before.
5. Record confirmed spin-off dispositions (create separately, drop, or fold in). Do not create the spin-off issues. Offer to hand them to the issue-creation skill.
6. Update the status line, for example `Draft, 2 open questions`, and summarize what changed since the last pass in chat.
7. Ask for the remaining answers and stop.

Partial answers are fine. Lock what is answered and keep the rest open.

## Step 7: Lock the plan

The plan is ready to lock when all of these hold:

- No question is `pending`.
- No decision conflicts with another or with a project constraint.
- Every "pending Q#" marker in the approach is resolved.
- Every "needs runtime verification" item is either resolved or has an explicit decision on how and when it will be verified.
- Spin-off items each have a confirmed disposition.

Then:

1. Set the status line to `Locked` with the date.
2. Reduce Section 10 to `No open questions.` and keep the history in Section 9.
3. Ensure Section 6 reads as a complete, decision-free description of what will be built, so `requirements.md` can be derived from it.
4. Tell the user the plan is locked, list the confirmed spin-offs, and ask whether to proceed to `requirements.md`. Wait for their go-ahead.

## Edge cases

- **Issue is vague or very small**: say so, keep the plan proportionate, and ask fewer questions. A short plan is correct for a short issue.
- **Issue conflicts with the code**: lead with the finding, state what the code actually does, and ask whether the intent changes.
- **Issue proposes a fix that violates a project constraint** (for example editing an upstream template): do not plan it as written. Explain the constraint and offer compliant alternatives.
- **Issue is a security weakness in a published repository**: flag disclosure handling in Section 4.1 and keep exploit detail in `PLAN.md` to what the decisions require.
- **User disagrees with a recommendation**: adopt their choice, record the rationale, and note any residual risk as a risk entry.
