# Steering: Naming Conventions (CloudFormation/SAM)

Loads when template files named `template*` or `cfn*` with a `.yml` or `.yaml` extension are in use. Use it for any CloudFormation or SAM project, whether or not it uses Atlantis.

[View example steering: naming-conventions-cloudformation.md](../../examples/steering/naming-conventions-cloudformation.md)

What it covers:

- **Logical names:** `PascalCase` for parameters, logical IDs, conditions, mappings, and outputs, with acronyms written as words.
- **Existing templates:** The agent does not rename existing logical IDs, because a new ID replaces the resource.
- **Physical names:** Follow the pattern already in the template, and use lowercase for S3 buckets.
- **Tags:** `PascalCase` keys, and `serviceName:TagName` for service-specific tags.
- **Environment variables:** `UPPER_SNAKE_CASE` for Lambda variables.

Copy it to `.kiro/steering/` in your project. If you deploy with Atlantis, also add [Naming Conventions (CloudFormation/SAM, Atlantis)](./naming-conventions-cloudformation-atlantis.md). Edit the file pattern if your templates use other names.
