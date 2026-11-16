# Skill: Update AWS Managed Lambda Layers

This skill looks up the latest Lambda Insights and AWS Parameters and Secrets Lambda Extension layer ARNs in the AWS documentation. It then updates the layer ARNs kept in the Mappings section of `application-infrastructure/template.yml`.

It can be installed in one of two places:

- `~/.kiro/skills/update-aws-lambda-layers/SKILL.md` for use in any project on your machine.
- `path/to/your/project/.kiro/skills/update-aws-lambda-layers/SKILL.md` if you want to keep it with one project.

Invoke it with `/update-aws-lambda-layers`, or ask the agent to update or check Lambda layer ARNs or extension versions.

What it does:

- **Finds your layers and regions:** Reads the regions already defined in the template, for both x86-64 and ARM64. It also checks whether each layer is mapped (`FindInMap`) or resolved from an AWS public parameter (`{{resolve:ssm:...}}`).
- **Leaves `resolve` layers alone:** A layer resolved from an AWS public parameter always gets the latest version at deploy time, so the skill does not update it or convert it to a Mapping. It adds a Mapping for that layer only if a region you deploy to has no public parameter, and it asks first.
- **Keeps Lambda Insights mapped:** Lambda Insights has no public parameter, so its ARNs stay in Mappings and are updated.
- **Fetches current ARNs:** Reads the latest version table on each AWS documentation page for the layers that are mapped.
- **Updates in place:** Replaces only the ARN values and source comments, and keeps the YAML format.
- **Reports changes:** Lists old and new versions per region and architecture, names the `resolve` layers it left untouched, or says that nothing changed.

It reads public AWS documentation pages and changes `template.yml`, so review the diff before you deploy.

[View example skill: update-aws-lambda-layers](../../examples/skills/update-aws-lambda-layers/SKILL.md)
