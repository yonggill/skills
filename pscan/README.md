# pscan — Project Context Scanner

Analyze project source code, architecture, and structure to generate a comprehensive context document. Load it at the start of a session for instant, full project understanding.

## Usage

```
/pscan              # Smart: generate if missing, update if stale, load if fresh
/pscan generate     # Force full regeneration
```

Or say "프로젝트 스캔" in natural language.

## How It Works

### Phase 1: Assess

Checks if `projectology.md` exists and compares its `git-hash` with current HEAD.

| Condition | Action |
|-----------|--------|
| Document missing | → Full Analysis |
| `generate` argument | → Full Analysis |
| 0 files changed since last scan | → Load document into context, done |
| < 30 files changed | → Incremental Update |
| ≥ 30 files changed | → Full Analysis |

### Phase 2: Full Analysis

Launches an Explore agent that reads the entire project:

1. **Config files** — Package.swift, package.json, Cargo.toml, etc.
2. **Entry points** — App main, index.ts, main.go, etc.
3. **Key interfaces/protocols** — The architecture's skeleton
4. **Every source file** — First 30-50 lines each for accurate role descriptions
5. **Test structure** — Grouped by feature area
6. **Scripts** — Each script's purpose

Framework auto-detection adjusts focus (Swift/Node/Rust/Go/Python/JVM/Multi-service).

### Phase 3: Incremental Update

For small changes (< 30 files): reads only changed files, determines which document sections are affected, and merges updates into the existing document.

### Phase 4: Synthesis

Compiles findings into a structured document:

- **Identity** — What the project does, who it's for
- **Stack** — Language, framework, build system, key deps
- **Architecture** — Pattern, layers, data flow, key abstractions
- **Modules** — Each module's responsibility, key files, dependencies
- **File Map** — Every source file with one-line role description
- **Key Flows** — 3-5 most important user-facing journeys
- **Data Models** — Core entities, relationships, storage
- **Build & Deploy** — Exact commands
- **Conventions** — Non-obvious project-specific patterns

### Phase 5: Save

Writes to `projectology.md` at the project root with git hash in frontmatter for freshness tracking. The file is tracked by git (not gitignored) so team members can share project context.

## Output

| Project Size | Target Tokens |
|-------------|---------------|
| Small (< 50 files) | ~3,000 |
| Medium (50-200 files) | ~6,000 |
| Large (200+ files) | ~10,000 |

## Installation

Copy the `pscan/` directory to `~/.claude/skills/`:

```
~/.claude/skills/pscan/SKILL.md
```

## Notes

- **Complements CLAUDE.md.** CLAUDE.md = instructions ("how to work"). pscan = understanding ("what the project is"). They don't overlap.
- **`projectology.md` should be tracked by git.** It is version-controlled so team members can share project context without regenerating.
- **No code snippets in output.** Describes patterns and relationships — code changes, descriptions endure.
