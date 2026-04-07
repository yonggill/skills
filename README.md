# skills

General-purpose skills for Claude Code.

## Available Skills

| Skill | Description |
|-------|-------------|
| [pscan](pscan/) | Project context scanner — analyzes source code, architecture, and structure to generate a comprehensive context document |
| [revealjs-ppt](revealjs-ppt/) | reveal.js 기반 프레젠테이션 생성 — 발표 유형별 구조, 디자인 시스템, 레이아웃/컴포넌트 적용하여 CDN 기반 단일 HTML 출력 |

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
