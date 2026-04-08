# skills

General-purpose skills for Claude Code.

## Available Skills

| Skill | Description |
|-------|-------------|
| [pscan](pscan/) | Project context scanner — analyzes source code, architecture, and structure to generate a comprehensive context document |
| [pptmaker](pptmaker/) | reveal.js 기반 프레젠테이션 생성 — 발표 유형별 구조, 디자인 시스템, 레이아웃/컴포넌트 적용하여 CDN 기반 단일 HTML 출력 |
| [generate-spec](generate-spec/) | 프로젝트 기획 명세 생성 — 6단계 파이프라인(계획서→메뉴→페이지→명세→기능→기능명세)으로 템플릿 기반 기획 산출물 생성 |

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
