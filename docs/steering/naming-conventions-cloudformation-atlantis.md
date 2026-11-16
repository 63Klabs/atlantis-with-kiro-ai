# Steering: Naming Conventions (CloudFormation/SAM, Atlantis)

Loads when template files named `template*` or `cfn*` with a `.yml` or `.yaml` extension are in use. Use it in templates deployed with the Atlantis platform.

[View example steering: naming-conventions-cloudformation-atlantis.md](../../examples/steering/naming-conventions-cloudformation-atlantis.md)

What it covers:

- **Parameters:** The `Prefix`, `ProjectId`, `StageId`, and `S3BucketNameOrgPrefix` parameters and their length and character limits.
- **Resource names:** `<Prefix>-<ProjectId>-<StageId>-<ResourceId>` with a `PascalCase` resource ID, and the shared-resource and service-role variants.
- **S3 buckets:** The account-regional and global bucket name patterns.
- **Checking names:** The agent validates planned names with the Atlantis MCP `validate_naming` tool.

Copy it to `.kiro/steering/` together with [Naming Conventions (CloudFormation/SAM)](./naming-conventions-cloudformation.md). Where the two differ on physical names, this file wins.
