# Skill: Update AWS Managed Lambda Layers

This skill looks up the latest Lambda Insights and AWS Parameters and Secrets Lambda Extension layer ARNs in the AWS documentation. It then updates the Mappings section of `application-infrastructure/template.yml`.

It can be installed in one of two places:

- `~/.kiro/skills/update-aws-lambda-layers/SKILL.md` for use in any project on your machine.
- `path/to/your/project/.kiro/skills/update-aws-lambda-layers/SKILL.md` if you want to keep it with one project.

Invoke it with `/update-aws-lambda-layers`, or ask the agent to update or check Lambda layer ARNs or extension versions.

What it does:

- **Finds your regions:** Reads the regions already defined in the template, for both x86-64 and ARM64.
- **Fetches current ARNs:** Reads the latest version table on each AWS documentation page.
- **Updates in place:** Replaces only the ARN values and source comments, and keeps the YAML format.
- **Reports changes:** Lists old and new versions per region and architecture, or says that nothing changed.

It reads public AWS documentation pages and changes `template.yml`, so review the diff before you deploy.

[View example skill: update-aws-lambda-layers](../../examples/skills/update-aws-lambda-layers/SKILL.md)
