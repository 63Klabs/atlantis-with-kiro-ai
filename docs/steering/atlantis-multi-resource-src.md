# Steering: Multi-Resource Source Layout

Loads when files under `application-infrastructure/` are in use. Use it when your project has, or will have, more than one Lambda function, a Lambda layer with its own dependencies, or a static site.

[View example steering: atlantis-multi-resource-src.md](../../examples/steering/atlantis-multi-resource-src.md)

What it covers:

- How to recognize the older single-folder `src/` layout.
- Moving to `src/lambda/<function-name>/`, one self-contained folder per function, before you add a second resource.
- Renaming the generic `AppFunction` logical ID and the CloudFormation changes that go with it.
- A buildspec loop that tests and audits each function separately.

Read the rename warning before you migrate. Changing a CloudFormation logical ID makes CloudFormation replace the resource, so set an explicit `FunctionName` first to keep the deployed function.
