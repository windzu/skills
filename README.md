# Wind's Claude Skills

Personal collection of Claude Code skills for specialized tasks.

## Repository Structure

```
skills/
├── .claude-plugin/       # Claude Code plugin configuration
│   └── manifest.json
├── skills/               # Custom skills directory
│   └── <skill-name>/     # Each skill in its own folder
│       └── SKILL.md      # Skill definition file
├── template/             # Skill template for creating new skills
│   └── SKILL.md
├── .gitignore
└── README.md
```

## What are Skills?

Skills are folders of instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks. Each skill contains a `SKILL.md` file with YAML frontmatter and instructions.

## Creating a New Skill

1. Copy the `template/SKILL.md` to a new folder under `skills/`:
   ```bash
   mkdir skills/my-new-skill
   cp template/SKILL.md skills/my-new-skill/SKILL.md
   ```

2. Edit the `SKILL.md` file:
   - Update the `name` field (lowercase, use hyphens)
   - Write a clear `description`
   - Add your instructions and examples

3. Commit and push to GitHub

## Installing Skills

### In Claude Code

Add this repository as a plugin marketplace:
```bash
/plugin marketplace add windzu/skills
```

Then install specific skills:
```bash
/plugin install <skill-name>@windzu-skills
```

### From Local Directory

```bash
/plugin add /path/to/skills/skills/<skill-name>
```

## SKILL.md Format

```markdown
---
name: skill-name
description: Description of what the skill does and when to use it
---

# Skill Name

Instructions for Claude to follow...
```

## Available Skills

| Skill Name | Description |
|------------|-------------|
| docker-dev-env | Create Docker-based development environments with docker-compose |

## License

MIT
