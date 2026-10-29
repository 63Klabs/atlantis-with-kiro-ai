# Steering: Python Dependency Management

Loads when `requirements*.txt` files are in use. Use it to decide which requirements file a package belongs in.

[View example steering: atlantis-python-dependency-management.md](../../examples/steering/atlantis-python-dependency-management.md)

The three files:

- **`requirements.txt`:** Code that runs in Lambda. Installed everywhere and deployed.
- **`requirements-test.txt`:** Packages needed only to run tests, such as pytest. Installed in CI, never packaged.
- **`requirements-dev.txt`:** Local development tools, such as boto3 and moto. Never installed in CI and never deployed.

The steering also covers install order for local development and CI, and asks the agent to keep your version pins and inline comments as they are.
