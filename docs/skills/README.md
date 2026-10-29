# Skills

For Kiro, skills need to be installed as `.kiro/skills/{skill-name}/SKILL.md` in either the user (`~`) directory (globally) or project directory.

- `~/.kiro/skills/{skill-name}/SKILL.md` (global)
- `path/to/project/.kiro/skills/{skill-name}/SKILL.md` (project)

Other Agentic IDEs may store them in a different location.

Skill files are provided in a commonly accepted format recognized by many different Agentic platforms allowing them to be used outside of Kiro without having to convert or reformat.

Many skill files provided through this repository are not Atlantis specific, but adhere to the development workflow used for developing the Atlantis DevOps Platform. Any Atlantis specific skill file will be name with an `atlantis-` prefix such as (`atlantis-platform-resources`).

Skills are invoked in the agentic chat or CLI by typing `/{skill-name}`

To install a skill using the Atlantis MCP:

1. Ask your chat agent to list available Atlantis skills (it will call the Atlantis MCP)
2. Typically it will provide a list with descriptions allowing you to pick one or more to add to your project or global directory.
3. Once you have made your selection your agent will download the file and save it locally. (Make sure it save it in the proper location for example: `.kiro/skills/{skill-name}/SKILL.md` and not `.kiro/skills/{skill-name}.md`.)

Sometimes skills receive updates. You can have your Atlantis MCP check for differences between your local copy and the published copy and then decide if you want the new published copy.

Available Skills:

- Atlantis Platform Resources
- Audit Update NPM Packages
- Audit Update Python Packages
- Update AWS Managed Lambda Layers
- [Import Issues from GitHub](./import-issues-from-github.md)
- [Plan from Issue](./plan-from-issue.md)
