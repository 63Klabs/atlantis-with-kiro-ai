# Agents File (AGENTS.md)

`AGENTS.md` is a single instruction file that AI coding assistants read for project context. The example in this repository sets the guardrails for applications built on the Atlantis platform and deployed to AWS with serverless services.

To use it, copy the example to the root of your repository as `AGENTS.md`, then edit it for your project.

[View example: AGENTS.md](../../examples/agents-md/AGENTS.md)

What it sets:

- **Scope:** Application code and infrastructure only. Shared storage, networking, and pipelines stay with platform engineering.
- **Naming:** `Prefix-ProjectId-StageId-Resource`, including the three S3 bucket patterns.
- **Security:** Least-privilege IAM with no AWS managed policies, and secrets kept in Secrets Manager or SSM Parameter Store.
- **Deployment:** GitOps through pipelines only, with branches mapped to stages (`test`, `beta`, `main`).
- **Architecture:** Serverless, event-driven, modular, with small dependency lists and unit tests for new functions.
- **Documentation:** Which docs to update after a major change.

Before you use it:

- Replace the Atlantis-specific branch, naming, and organization details if your team differs.
- Remove rules that do not apply. An agent follows what the file says, so a rule your team does not follow leads to output your team will reject.
