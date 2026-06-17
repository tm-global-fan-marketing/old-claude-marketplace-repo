## New Plugin

**Plugin Name**: `{plugin-name}`
**Team**: `{team-name}`
**Category**: `{category}`
**Initial Skills**: {count}

### Description

What this plugin provides and who should install it.

### Author Checklist

- [ ] Plugin name starts with `tm-marketing-` prefix
- [ ] `plugin.json` has all required fields (name, description, version, author, homepage, repository)
- [ ] Plugin registered in `.claude-plugin/marketplace.json` with correct relative `source` path
- [ ] At least one skill included under `skills/{skill-name}/SKILL.md`
- [ ] Plugin has its own `CLAUDE.md` with skill trigger table
- [ ] `.mcp.json` included if plugin requires MCP connectors
- [ ] Tested locally: installed the plugin and verified skills activate in Claude
- [ ] README updated with plugin listing

### Reviewer Checklist

- [ ] Plugin name follows `tm-marketing-{role}` naming pattern
- [ ] No name conflicts with existing plugins in marketplace.json
- [ ] `marketplace.json` version matches `plugin.json` version
- [ ] Category and tags are appropriate
- [ ] All skills have clear, specific trigger conditions
