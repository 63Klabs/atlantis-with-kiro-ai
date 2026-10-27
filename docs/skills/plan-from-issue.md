# Skill: Plan from Issue

> This skill expects an ISSUE.md to exist within a spec directory. ISSUE.md can be generated using a separate skill that pulls in an issue from Jira, GitHub, or other issue tracker. **Only pull in trusted issues from trusted sources reviewed by humans first!**

Since this skill is generic, and used for the spec-driven workflow, it can reside in one of two places:

- `~/.kiro/skills/plan-from-issue/SKILL.md` for global use in any project on your machine.
- `path/to/your/project/.kiro/skills/plan-from-issue/SKILL.md` if you want to store it with individual projects. 

It can be invoked with `/plan-from-issue` plus a spec directory, or just ask to "plan" or "review" an ISSUE.md. If you don't name a directory, it uses the active editor file or asks.

What it does:

- **Setup:** It stops if there's no ISSUE.md. If PLAN.md already exists, it resumes the iteration instead of starting over.
- **Project context:** It reads AGENTS.md, the architecture docs, steering, the changelog, sibling specs, and git history for the affected files. Past fixes are often deliberate, so the plan must not regress them. This is what keeps the skill generic across your projects.
- **Claim verification:** Each assertion in the issue gets a verdict with path:line evidence: confirmed, partial, not confirmed, or needs runtime verification. Your steering rule is built in: it never dismisses a reported problem just because the code looks fine.
- **Three-lens review:** Security analyst, software engineer, and cloud engineer, each with its own checklist.
- **Gaps and tangents:** Related fixes are classified as include, spin off, or note only. Spin-offs are only recommended until you confirm them, and it never expands scope silently.
- **PLAN.md:** The structure runs from summary, assessment, current state, review, gaps, approach, related improvements, and risks to locked decisions. Open questions come last. Each question has options, a recommendation, and an Answer: line for you.
- **Iteration:** Answered questions move to the locked decisions table, and the affected sections are updated. The three-lens review runs again on the consequences, and new questions are added if an answer conflicts with something or weakens security. Question numbers never change.
- **Locking:** The plan locks when nothing is pending and every spin-off has a disposition. It then asks before moving to requirements.md, and it never writes that file itself.

[View example skill: plan-from-issue](../../examples/skills/plan-from-issue/SKILL.md)