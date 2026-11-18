# AGENTS.md

This repository is a library of **skills**, **hooks**, **steering files**, and an **AGENTS.md** template for AI coding agents working with the [63Klabs Atlantis DevOps Platform](https://atlantis.63klabs.net). It contains no application code, build, or test suite. The content is Markdown (and, for hooks, JSON).

The files in `examples/` are not instructions for this repository. They are copied into other projects that this repository knows nothing about. In particular, `examples/agents-md/AGENTS.md` is a template for application repositories. Do not apply its rules here, and do not copy this file's content into it.

## Required reading

Before you create, edit, rename, or delete anything under `examples/` or `docs/`, read [`.kiro/steering/maintaining-examples.md`](.kiro/steering/maintaining-examples.md). It defines file naming, the `atlantis-` prefix rule, keeping files generic and concise, changelog conventions, the required docs page for each example, and the process for changing or removing a file. Where this file and that file disagree, that file wins.

## Layout

| Path | Contents | Published |
| --- | --- | --- |
| `examples/skills/{skill-name}/SKILL.md` | Skills | Yes |
| `examples/steering/{name}.md` | Steering files | Yes |
| `examples/hooks/` | Hooks (currently empty) | Yes |
| `examples/agents-md/AGENTS.md` | AGENTS.md template for application repositories | Yes |
| `docs/{skills,steering,agents-md,mcp}/` | One short page per example, plus a `README.md` index in each folder | No |
| `.kiro/steering/` | Steering for working on this repository | No |
| `CHANGELOG.md` | Release notes for the assets in `examples/` | No |

`docs/README.md` indexes the docs folders. The root `README.md` is the public landing page.

## How content is released

1. Publishing a GitHub release triggers `.github/workflows/deploy-to-s3.yml`.
2. The workflow stages only `examples/agents-md`, `examples/hooks`, and `examples/steering` as they are. It flattens each `examples/skills/{name}/SKILL.md` to `skills/{name}.md`. Anything else under `examples/` is excluded.
3. It uploads the staged tree as `agent_assets.zip` and also syncs it unzipped to `agent_assets/` under the same S3 prefix. The sync uses `--delete`, so a file removed from `examples/` disappears from S3 on the next release.
4. The Atlantis MCP server indexes and serves the files from S3. S3 is used so access is fast, versioned, and independent of GitHub throttling or outages.

Consequences for changes:

- Merging to the default branch does not publish. Only a published release does.
- A skill must stay in a `{skill-name}/SKILL.md` folder under `examples/skills/`. A bare `.md` file there is not picked up.
- A new top-level folder under `examples/` is not published until it is added to `INCLUDE_DIRS` in the workflow. Ask the user before changing the workflow.
- `examples/hooks/` is empty, and git does not track empty folders. Add a file when you add the first hook.
- The workflow reads AWS settings from GitHub secrets and variables. Never write account IDs, bucket names, or credentials into this repository.

## Working rules

- Every file under `examples/` needs a matching page under `docs/` and an entry in that folder's `README.md`, in the same change. Rename and delete follow the same rule. After a rename or delete, search the whole repository for the old name, because skills and steering refer to each other by name.
- Keep `examples/` files free of values specific to this repository or any one organization. Use placeholders such as `example-org/example-package`.
- Verify claims about the Atlantis platform with the Atlantis MCP tools (`search_documentation`, `validate_naming`) before you write them. If you cannot verify a claim, soften it or leave it out.
- Before you rewrite an existing example, give the user your findings and numbered questions, and wait for the answers.
- Record each change to `examples/` or `docs/` in `CHANGELOG.md`, under the `(unreleased)` heading. Use the category order in `maintaining-examples.md`, and name each asset by its published path (for example `skills/{skill-name}` or `steering/{file-name}.md`). Do not set a release date or version heading yourself. Ask the user to confirm the version if no `(unreleased)` heading exists.
- Do not create a release, tag, or push to a remote unless the user asks.

## Related resources

- [Atlantis MCP server](https://mcp.atlantis.63klabs.net) and its [Kiro integration guide](https://mcp.atlantis.63klabs.net/docs/integration/kiro.html)
- [Atlantis DevOps Platform](https://atlantis.63klabs.net)
