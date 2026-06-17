## New Skill

**Skill Name**: `{skill-name}`
**Plugin**: `{plugin-name}`
**Trigger**: {what user says to invoke this skill}

### Description

What this skill does and who it's for.

### Author Checklist

- [ ] `SKILL.md` created at `plugins/{team}/{plugin}/skills/{skill-name}/SKILL.md`
- [ ] Trigger row added to `plugins/{team}/{plugin}/CLAUDE.md`
- [ ] MINOR version bumped in `plugin.json` and `marketplace.json`
- [ ] README updated
- [ ] Tested locally: skill triggers correctly from natural language

### Reviewer Checklist

- [ ] Trigger condition is specific enough to avoid false positives
- [ ] Skill references `ln-confluence` appropriately if it needs brand/campaign context
- [ ] Output format is clearly defined
- [ ] No overlap with existing skill triggers
