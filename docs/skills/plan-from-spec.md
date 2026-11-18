# Skill: Plan from Spec

> This skill expects a SPEC.md to exist within a spec directory. SPEC.md is a requirements document written by you or your project team, so the skill treats it as trusted intent. It still reviews the spec for gaps, conflicts, and trade-offs. To plan from an imported issue instead, use [Plan from Issue](./plan-from-issue.md).

Since this skill is generic, and used for the spec-driven workflow, it can reside in one of two places:

- `~/.kiro/skills/plan-from-spec/SKILL.md` for global use in any project on your machine.
- `path/to/your/project/.kiro/skills/plan-from-spec/SKILL.md` if you want to store it with individual projects.

It can be invoked with `/plan-from-spec` plus a spec directory, or just ask to "plan" or "review" a SPEC.md. If you don't name a directory, it uses the active editor file or asks.

What it does:

- **Setup:** It stops if there's no SPEC.md. If the directory also has an ISSUE.md, it asks which one to plan from. If PLAN.md already exists, it resumes the iteration instead of starting over.
- **Project context:** It reads AGENTS.md, the architecture docs, steering, the changelog, sibling specs, and git history for the affected files, so the plan fits your project.
- **Spec review:** Each requirement in the spec gets an ID and a verdict with evidence: clear and feasible, ambiguous, conflicting, incomplete, or needs runtime verification. It also lists what the spec leaves out and the trade-offs it makes without saying so.
- **Given decisions:** Decisions your spec states outright go into the plan as locked. The skill only reopens one when it conflicts with another requirement, a project constraint, security, or the code.
- **Four-lens review:** Solutions architect, security analyst, software engineer, and cloud engineer, each with its own checklist.
- **Architecture fit:** The architect lens works out what your application's architecture is from the repository, then checks every resource the spec names against it. A spec that asks for EC2 or Redshift in a serverless application gets a question with the compliant alternative, not silent acceptance or silent replacement. If the spec leaves resources open or asks for a recommendation, the plan proposes a resource set with alternatives.
- **Gaps and tangents:** Related fixes are classified as include, spin off, or note only. Spin-offs are only recommended until you confirm them, and it never expands scope silently.
- **PLAN.md:** The structure runs from summary, assessment, current state, review, gaps, approach, related improvements, and risks to locked decisions. Open questions come last. Each question has options, a recommendation, and an Answer: line for you.
- **Iteration:** Answered questions move to the locked decisions table, and the affected sections are updated. The four-lens review runs again on the consequences, and new questions are added if an answer conflicts with something or weakens security. Question numbers never change. It tells you which spec requirements your answers change, but never edits SPEC.md.
- **Locking:** The plan locks when nothing is pending and every spin-off has a disposition. It then asks before moving to requirements.md, and it never writes that file itself.

[View example skill: plan-from-spec](../../examples/skills/plan-from-spec/SKILL.md)
