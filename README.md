# Wind's Claude Skills

Personal collection of Claude Code skills for specialized tasks.

## Repository Structure

```
skills/                           # Repository root (marketplace)
├── .claude-plugin/
│   └── marketplace.json          # Marketplace manifest
├── plugins/                      # Plugins directory
│   └── docker-dev-env/           # Plugin: docker-dev-env
│       └── skills/
│           └── docker-dev-env/   # Skill definition
│               ├── SKILL.md
│               ├── scripts/
│               └── references/
├── template/                     # Skill template for creating new skills
│   └── SKILL.md
├── .gitignore
└── README.md
```

## What are Skills?

Skills are folders of instructions, scripts, and resources that Claude loads dynamically to improve performance on specialized tasks. Each skill contains a `SKILL.md` file with YAML frontmatter and instructions.

## Creating a New Skill

1. Create a new plugin directory with a skill folder:
   ```bash
   mkdir -p plugins/my-new-skill/skills/my-new-skill
   cp template/SKILL.md plugins/my-new-skill/skills/my-new-skill/SKILL.md
   ```

2. Edit the `SKILL.md` file:
   - Update the `name` field (lowercase, use hyphens)
   - Write a clear `description`
   - Add your instructions and examples

3. Add the plugin entry to `.claude-plugin/marketplace.json`:
   ```json
   {
     "name": "my-new-skill",
     "description": "Description of the skill",
     "source": "./plugins/my-new-skill",
     "strict": false
   }
   ```

4. Commit and push to GitHub

## Installing Skills

### Method 1: Using Claude Code CLI (Recommended)

1. Add this repository as a plugin marketplace:
   ```bash
   /plugin marketplace add windzu/skills
   ```

2. Install specific skills:
   ```bash
   /plugin install <skill-name>@windzu-skills
   ```

### Method 2: Manual Configuration

If automatic installation doesn't work, follow these steps:

1. **Clone the repository** to Claude's marketplace directory:
   ```bash
   git clone git@github.com:windzu/skills.git ~/.claude/plugins/marketplaces/windzu-skills
   ```

2. **Enable the plugin** in `~/.claude/settings.json`:
   ```json
   {
     "enabledPlugins": {
       "docker-dev-env@windzu-skills": true
     }
   }
   ```

3. **Register the plugin** in `~/.claude/plugins/installed_plugins.json`:
   ```json
   {
     "version": 2,
     "plugins": {
       "docker-dev-env@windzu-skills": [
         {
           "scope": "user",
           "installPath": "/home/<username>/.claude/plugins/cache/windzu-skills/docker-dev-env/<version>",
           "version": "<version>",
           "installedAt": "2026-01-26T00:00:00.000Z",
           "lastUpdated": "2026-01-26T00:00:00.000Z",
           "gitCommitSha": "<version>"
         }
       ]
     }
   }
   ```

   > **Note:** The `installPath` must point to the **cache directory**, not the marketplace directory. Claude Code automatically copies plugins to `~/.claude/plugins/cache/` with a version hash.

4. **Restart Claude Code** to load the new skill.

### Verifying Installation

After installation, run:
```bash
/docker-dev-env
```

If the skill loads successfully, you'll see the Docker Development Environment workflow.

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
