# skills

General-purpose skills for Claude Code.

## Available Skills

| Skill | Description |
|-------|-------------|
| [pscan](pscan/) | Project context scanner — analyzes source code, architecture, and structure to generate a comprehensive context document |

## Installation

Clone into `~/.claude/skills/`:

```bash
git clone git@github.com:yonggill/skills.git ~/.claude/skills
```

Or copy individual skill directories.

## Usage

In Claude Code, invoke by slash command or natural language:

```
/pscan              # Scan current project
/pscan generate     # Force full regeneration
```

See each skill's README for details.
