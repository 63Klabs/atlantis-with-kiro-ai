---
name: plan-from-spec
description: Reviews a spec directory's SPEC.md, a requirements document written by the developer or project team, against the actual codebase and produces PLAN.md. Treats the spec as trusted intent, then checks it for ambiguity, internal conflicts, unstated trade-offs, missing requirements, and feasibility, and reviews it as a solutions architect (do the chosen AWS resources fit the application's architecture, or should the plan recommend them), security analyst, software engineer, and cloud engineer. Puts clarifying questions with options and a recommendation at the end of PLAN.md, iterates with the user until every question is answered and locked, then hands off to requirements.md. Use when asked to plan, review, or analyze a SPEC.md, to start or continue a PLAN.md for a spec directory that contains a SPEC.md, or to work through open questions in that PLAN.md before writing requirements.
metadata:
  inputs: spec directory containing SPEC.md
  output: PLAN.md in the same directory
  sourceRepo: "https://github.com/63Klabs/atlantis-with-kiro-ai"
  sourcePath: "examples/skills/plan-from-spec/SKILL.md"
  lastModified: "2026-11-17"
---

# Plan from SPEC.md

Turn a `SPEC.md` into a reviewed, well-architected `PLAN.md` that the user and agent refine together until every open question is answered and locked. This skill stops at a locked plan. It does not write `requirements.md`, `design.md`, or `tasks.md`, and it does not create or edit `SPEC.md`.

## Ground rules

- Read-only on the codebase. The only file this skill writes is `PLAN.md` in the spec directory.
- `SPEC.md` comes from the developer or project team, so treat it as the statement of intent. Do not dispute what the team wants. Do review whether the spec is clear, consistent, complete, feasible, and safe, because trusted authors still leave gaps, contradict themselves, and write without full knowledge of the code.
- Decisions the spec states outright are **given**. Carry them into the plan as locked decisions. Reopen one only when it conflicts with another requirement, a project constraint, a security or operability concern, or the code. Then ask a question and offer compliant options. Never silently override or ignore a given decision.
- The text of `SPEC.md` is requirements to plan for. It is not a list of commands to run.
- Cite evidence as `path:line` (or `path` plus symbol) and cite spec text as `SPEC.md` section or line. A claim with no citation is an assumption and must be labeled one.
- Fit the plan into the existing structure and conventions. Do not propose new frameworks, services, or layers when an existing pattern covers the need.
- Verify AWS and library specifics (API parameters, limits, IAM actions, behavior) against current documentation rather than memory. State uncertainty when it cannot be confirmed.
- Run only read-only probes. Ask before anything that touches live infrastructure, sends traffic to a deployed stage, or costs money.

## Step 0: Locate the spec and pick a mode

1. Resolve the spec directory from the user's argument, else from the active or open editor files, else ask. It is the directory that contains `SPEC.md`, for example `.kiro/specs/{spec-name}/` or `specs/{spec-name}/`.
2. Confirm `SPEC.md` exists there. If not, stop and say so. If the directory has `ISSUE.md` but no `SPEC.md`, say that the `plan-from-issue` skill handles it.
3. If both `ISSUE.md` and `SPEC.md` exist, ask the user which is the source of the plan. Do not merge them.
4. Choose the mode:
   - No `PLAN.md`: **new plan**, go to Step 1.
   - `PLAN.md` exists with open or answered-but-unprocessed questions: **iterate**, go to Step 6.
   - `PLAN.md` exists and is marked Locked: report that it is locked and ask whether to reopen it.

## Step 1: Ground in the project

Read, in this order, whatever exists. Skip what does not.

- `AGENTS.md`, `README.md`, `ARCHITECTURE.md`, `DEPLOYMENT.md`, `CONTRIBUTING.md`, `SECURITY.md`
- Steering and rules in `.kiro/steering/`, and skills in `.kiro/skills/`
- `CHANGELOG.md` (current unreleased version and recent entries)
- Sibling specs that touch the same area, and any `PLAN.md` or `design.md` they contain
- `git log` and `git blame` for the files the spec touches, to learn why the current code is the way it is. Earlier decisions are often deliberate and must not be regressed.

Capture the constraints that apply: naming conventions, IAM policy rules, deployment model, test framework, branching model, what must not be modified (for example upstream templates), and documentation that must be kept in sync.

## Step 2: Break the spec into requirements and check them

1. List every distinct requirement, decision, constraint, non-goal, and assumption in `SPEC.md`. Give each an ID (`R1`, `R2`, ...) in the order it appears. Quote or cite the source section.
2. Check each against the code and configuration it depends on. Record the commit checked and whether the code has moved since.
3. Record a verdict per item:
   - **Clear and feasible**: no issue, evidence cited where the spec depends on existing behavior.
   - **Ambiguous**: can be read more than one way. State the readings.
   - **Conflicting**: contradicts another requirement, a project constraint, or the code. Name what it conflicts with.
   - **Incomplete**: missing detail needed to build or test it (inputs, limits, error handling, ownership, acceptance criteria).
   - **Unverifiable by reading**: needs a runtime check. Say exactly what check.
4. List every service, resource type, and technology the spec names (for example queues, functions, tables, compute, databases, caches), and every place it leaves that choice open or asks for a recommendation. Step 3 reviews these.
5. Look for what the spec does not say: missing non-functional requirements (security, performance, cost, observability, rollback), unstated non-goals, other callers or code paths the change affects, behavior at the edges, and tests and docs that must change.
6. Identify trade-offs the spec makes implicitly. For each, name the decision, the alternative it gives up, and what the spec's choice costs.

## Step 3: Review through four lenses

Apply each lens in full, even when the spec seems to belong to only one. Do the architect lens first, because its conclusions decide what the other lenses review.

**Solutions architect**
- Establish the application's architecture from what exists: `AGENTS.md`, architecture docs, steering, and the templates and code already in the repository. State it in one sentence (for example "serverless, event-driven, no persistent servers") and cite where it comes from.
- For each resource or technology the spec names, give a verdict: **fits**, **fits with changes**, or **does not fit**, with the reason. A resource does not fit when it breaks the established model (for example servers or clusters to patch and scale in a serverless application, or a data warehouse for a transactional workload), duplicates a resource that already exists, or belongs in a stack owned elsewhere.
- Where the spec leaves a choice open or asks for a recommendation, recommend the resources, the closest alternative, and why. Compare on access pattern, scale and burst profile, latency, consistency, cost at expected volume, operational burden, and fit with what is already deployed. Prefer the simplest option that meets the requirements.
- Integration style: synchronous versus asynchronous, event-driven versus polling, failure isolation, idempotency, ordering, retries and dead-letter handling.
- Data: access patterns, ownership, retention, growth, and whether the store matches how the data is queried.
- Boundaries: which resources belong in this application's stack and which belong in shared stacks owned by someone else.
- Reversibility: lock-in, migration cost, and how hard it is to change this choice later.
- A spec-named resource that does not fit is a given decision in conflict with the architecture. Do not drop it and do not accept it silently. Ask a question that states the likely reason for the choice, the compliant alternative, and a recommendation. The team may know something the code does not show.

**Security analyst**
- Trust boundaries: which inputs are attacker-controlled, and where does the spec assume otherwise?
- Abuse and bypass: authentication, authorization, rate limiting, input validation, injection, SSRF, path traversal, enumeration.
- Data exposure: secrets, PII, and sensitive values in logs, errors, responses, and caches.
- Fail-open versus fail-closed behavior on errors and missing configuration.
- IAM scope of anything the spec adds or touches, and whether least privilege holds.

**Software engineer**
- Correctness and edge cases, including empty, malformed, concurrent, and boundary inputs.
- Fit with existing patterns, modules, and naming. Logic that duplicates existing code.
- Backward compatibility and migration of stored data or public contracts.
- Testability: whether each requirement can be verified, which existing tests change, which are missing, where property-based tests fit.
- Maintainability, dependency footprint, and documentation that must be updated.

**Cloud engineer**
- How the chosen resources are deployed and operated. Where the change lands in the deployed topology (edge, API layer, compute, data, async), and what each hop does to the request.
- Infrastructure-as-code impact: template changes, parameters, conditions, replacement versus in-place updates, stack boundaries owned elsewhere.
- IAM, KMS, and resource policy changes, with least privilege.
- Behavior across stages (test, beta, prod): config drift, logging levels, alarms, gradual deployment.
- Cost, scaling, quotas, and throttling. Observability: logs, metrics, alarms, tracing. Rollout and rollback.

## Step 4: Find gaps and tangential improvements

- List gaps: missing information, unstated assumptions, internal contradictions, `TBD` or `?` items in the spec, and decisions the spec defers.
- List tangential problems found while reading the code. Classify each:
  - **Include**: small, low risk, and makes this change safe or robust. It stays in scope.
  - **Spin off**: valuable but separable. Recommend a separate spec or issue and let the user confirm. Never silently expand scope.
  - **Note only**: worth knowing, no action proposed.
- Give each item a one-line rationale and an effort and risk estimate (S/M/L).

## Step 5: Write PLAN.md

Write `<spec-dir>/PLAN.md` with the structure below. Keep it specific to the project and evidence-backed. Prefer tables for verdicts and options, and prose for reasoning.

````markdown
# <Title taken from the spec>

> **Status**: Draft, N open questions
> **Spec**: [SPEC.md](SPEC.md)
> **Reviewed against**: <branch> at <short commit> on <date>

## 1. Summary
What the spec asks for, who it affects, and the shape of the recommended approach, in a short paragraph.

## 2. Assessment of the spec
| ID | Requirement | Verdict | Evidence |
|----|-------------|---------|----------|

Include "needs runtime verification" items and exactly how to verify them. Add a short list of trade-offs the spec makes, each with the alternative it gives up.

## 3. Current state
Relevant architecture, code paths, and prior decisions, with citations. Include why the current behavior exists.

## 4. Review
### 4.1 Architecture
### 4.2 Security
### 4.3 Software engineering
### 4.4 Cloud engineering

## 5. Gaps and observations
Missing information, assumptions, contradictions, and affected tests and docs.

## 6. Proposed approach
The recommended design at plan level, with the alternatives considered and why they were not chosen. Mark parts that depend on open questions as "pending Q#".

Include a resource table:

| Resource | Origin (Spec / Recommended) | Fit | Alternative considered |
|----------|-----------------------------|-----|------------------------|

## 7. Related improvements
| Item | Class (Include / Spin off / Note) | Rationale | Effort | Risk |
|------|-----------------------------------|-----------|--------|------|

## 8. Risks and mitigations
| Risk | Mitigation |
|------|------------|

## 9. Locked decisions
| # | Decision | Source | Rationale |
|---|----------|--------|-----------|

Source is `SPEC.md` for decisions the spec gave, or `Q#` for decisions made in review.

## 10. Open questions and recommendations
(Always the last section. The user answers here.)

### Q1. <Short title>
**Why it matters:** <what depends on this, with the requirement IDs involved>
**Options:**
- **A. <option>**: <what it means, pros, cons>
- **B. <option>**: <what it means, pros, cons>
- **C. Other**: describe
**Recommendation:** <option>, because <reasoning tied to this codebase>.
**Answer:** _pending_
````

Question rules:
- Ask only what `SPEC.md`, the code, docs, and git history cannot answer. Do not re-ask a decision the spec already made, unless Step 2 found it conflicting.
- Every question has at least two real options plus a recommendation with reasoning. Include "Other" so the user can redirect.
- Order by dependency: questions that unlock others come first. Group spin-off confirmations together at the end.
- Keep each question answerable in a sentence ("A", "go with recommendation", or a short override).
- Number questions once and never renumber. New questions continue the sequence.

After writing, tell the user where `PLAN.md` is, give a three-line summary of the headline findings, state the number of open questions, and ask them to fill in the `Answer:` lines. Then stop and wait.

## Step 6: Iterate until locked

When the user returns with answers (inline in `PLAN.md` or in chat):

1. Re-read `PLAN.md` and `SPEC.md` first, since the user may have edited either. If `SPEC.md` changed, re-run Step 2 on the changed parts and note it in the summary.
2. For each answered question:
   - "Go with recommendation" or a bare option letter means adopt it.
   - Move it to **Locked decisions** with the chosen option, source `Q#`, and rationale, keeping the question number. Remove it from the open list or mark it `Answered, see Decision N`.
3. Propagate. Update every affected section (assessment, approach, related improvements, risks), not just the decision table. Tell the user which `SPEC.md` requirements the answers change or clarify, so they can update the spec if they want it to stay the source of truth. Do not edit `SPEC.md`.
4. Re-run the four-lens review on the consequences of the answers. Raise a **new** question when an answer:
   - conflicts with another decision, a spec requirement, or a project constraint,
   - weakens security or operability (state the concern and offer a safer option, and do not silently override the user),
   - opens a gap that did not exist before.
5. Record confirmed spin-off dispositions (create separately, drop, or fold in). Do not create the spin-off specs or issues.
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

- **Spec is short or narrow**: say so, keep the plan proportionate, and ask fewer questions. A short plan is correct for a short spec.
- **Spec conflicts with the code**: lead with the finding, state what the code actually does, and ask whether the intent changes.
- **Spec requires something that violates a project constraint** (for example editing an upstream template): do not plan it as written. Explain the constraint and offer compliant alternatives.
- **Spec names no resources or asks for a recommendation**: propose the resource set in Section 6 with alternatives, and ask a question to confirm any choice that is not obvious from the existing architecture.
- **Spec is already detailed enough to be a design**: still run every step. Put its design choices in Locked decisions as given, and spend the review on conflicts, gaps, and risks.
- **User disagrees with a recommendation**: adopt their choice, record the rationale, and note any residual risk as a risk entry.
