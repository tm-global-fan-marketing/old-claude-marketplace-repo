# TM Marketing Claude Code Marketplace — Contributor Guidelines

## Version Bumps (REQUIRED)

When modifying any file inside a `plugins/` directory, you MUST bump the plugin version:

1. **`plugin.json`** — increment the `"version"` field inside `plugins/{team}/{plugin}/.claude/plugin.json`
2. **`marketplace.json`** — update the matching `"version"` in `.claude-plugin/marketplace.json`
3. **`README.md`** — update the version in the plugins table

### Which version component to bump

- **PATCH** (1.0.0 → 1.0.1): Bug fixes, typo corrections, minor wording changes
- **MINOR** (1.0.0 → 1.1.0): New skills, significant workflow improvements, new features
- **MAJOR** (1.0.0 → 2.0.0): Breaking changes, complete rewrites, removed skills

## Adding a New Plugin

1. Create `plugins/{team}/{plugin-name}/` directory
2. Add `.claude/plugin.json` with name, description, version, author, homepage, repository
3. Add `skills/{skill-name}/SKILL.md` for each skill
4. Add `.mcp.json` if the plugin needs MCP connectors
5. Register the plugin in `.claude-plugin/marketplace.json`
6. Update `README.md` plugins table
7. Raise an MR using the `new-plugin` template

### Plugin Naming

Plugin names must follow the `tm-marketing-{role}` pattern:

| Team | Prefix | Directory |
|---|---|---|
| Central Marketing | `tm-marketing` | `plugins/tm-marketing/` |

## Adding a New Skill to an Existing Plugin

1. Create `plugins/{team}/{plugin}/skills/{skill-name}/SKILL.md`
2. Add a trigger row to `plugins/{team}/{plugin}/CLAUDE.md`
3. Bump MINOR version in `plugin.json` and `marketplace.json`
4. Update `README.md`
