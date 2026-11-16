---
inclusion: fileMatch
fileMatchPattern: ['examples/**', 'docs/**']
---
# Maintaining Skills and Steering Examples

This repository stores skills, steering files, and AGENTS.md examples that the Atlantis MCP server serves to other projects. Anything under `examples/` is copied into projects this repository knows nothing about. Write each file for that reader.

## File names

- Use lowercase kebab-case, spell-check the name, and make it describe the content. A name that no longer matches the content is a bug (`spec-naming-convention.md`, not `spec-naming-convention-release-level-changelog.md`).
- The `atlantis-` **prefix** is reserved for steering and skills that do not apply outside the Atlantis framework (`atlantis-multi-resource-src.md`, `atlantis-platform-resources`). Do not use it for anything a non-Atlantis project could use.
- When a topic has a generic file and an Atlantis-specific file, the generic file has no Atlantis marker and the Atlantis file carries `atlantis` as the **last** word: `naming-conventions-cloudformation.md` and `naming-conventions-cloudformation-atlantis.md`. Keep Atlantis rules out of the generic file.
- When content depends on the kind of repository, end the steering name with the repository type: `-package` (one version in `package.json`) or `-application` (several components, one release version in `CHANGELOG.md`). Every example, URL, and command in that file must fit that type.

## Keep files generic

- Do not hard-code one repository's values: organization or repo names, issue URLs, template filenames, version numbers, spec names, runtimes, AMI IDs, or team and cost-center values.
- Use obvious placeholders in examples (`example-org/example-package`, `example-app`, `orders-api`). Where a real value is needed, write a rule that says where the agent reads it (for example `bugs.url` in `package.json`, or existing links in `CHANGELOG.md`). Never tell the agent to guess.
- Keep each topic in one file. When two files overlap, make one authoritative and state which wins. Remove contradictions between files.
- Verify claims about the Atlantis platform with the Atlantis MCP tools (`search_documentation`, `validate_naming`) before writing them. If a claim cannot be verified, soften it or leave it out.

## Keep files concise

- The reader is an agent. Include only rules that change what it does. Do not teach what an agent already knows (PEP 8, React basics, shell script structure, argument parsing).
- Prefer a table of rules plus one short example over several examples of the same rule. Do not add full example modules, repeated summaries, or "when in doubt" sections.
- State each rule once, in plain imperative language, and name stop conditions ("Stop and ask the user").
- Choose `inclusion` deliberately. Use `always` only for rules that must apply with no matching file open, and keep those short. Use `fileMatch` with the narrowest pattern that works for everything else.
- As a guide, a naming file is under about 100 lines, and a convention with several decision tables stays under about 200.

## Changelog conventions

- Use the `(unreleased)` marker only, never `- unreleased`.
- Use one category order in every changelog file: Security, Fixed, Breaking Changes, Added, Changed, Deprecated, Removed, Dependencies.
- Spec links are `.kiro/specs/<directory>/`, relative to `CHANGELOG.md` at the repository root.
- Spec directory versions always come from the `(unreleased)` heading. Each `changelog-convention-*` file says how that heading is created for its repository type, and no skill edits `CHANGELOG.md` for it.

## Documentation

- Every file in `examples/steering/`, `examples/skills/`, and `examples/agents-md/` has a matching short page in the same folder under `docs/`, following the layout of the existing pages: title, when it loads or how to invoke it, a link to the example, what it covers, and where to copy it.
- Write for the person choosing what to install. Say when to use the file. Do not explain how its internals work.
- Add each page to the README index in its folder.

## Changing or removing a file

- Rename or delete with the docs page and README entry in the same change.
- Search the whole repository for the old file name. Skills and steering files refer to each other by name.
- Before rewriting an existing file, give the user findings and numbered questions, wait for the answers, then rewrite.
