# xtool-skill

Skill definition for using `xtool` to build and deploy iOS apps from SwiftPM-based projects.

## Files

- `SKILL.md`: Main skill content (setup, workflows, CLI parameters, troubleshooting).
- `LICENSE`: MIT License.

## Purpose

This repository provides a reusable skill document that helps agents and developers:

- Set up `xtool` on Linux/WSL and macOS.
- Build and install iOS apps with `xtool`.
- Configure `xtool.yml` including app extensions.
- Troubleshoot common device and signing issues.

## Source references

The skill content is based on official xtool documentation and verified local `xtool --help` output.

- https://xtool.sh/documentation/xtool/

## Install in AI coding tools

Use `SKILL.md` in this repo as the source skill file.

### Claude Code

1. Create a skill folder in your project or user config:
   - Project: `.claude/skills/xtool-ios-build/`
   - User: `~/.claude/skills/xtool-ios-build/`
2. Copy this repo's `SKILL.md` to:
   - `.claude/skills/xtool-ios-build/SKILL.md`
3. Run Claude Code and invoke the skill by slash command or task intent.

### Codex CLI (OpenAI Codex)

1. Install Codex CLI (if needed):

```bash
npm i -g @openai/codex
```

2. Create the skill path:
   - Project: `.agents/skills/xtool-ios-build/`
   - User: `~/.agents/skills/xtool-ios-build/`
3. Copy `SKILL.md` to `.../SKILL.md` in that folder.
4. Optional: add repo instructions in `AGENTS.md`.

### OpenCode

1. Create the skill folder:
   - Project: `.opencode/skills/xtool-ios-build/`
   - User: `~/.config/opencode/skills/xtool-ios-build/`
2. Copy this repo's `SKILL.md` into that folder.
3. Optional: add broader repo rules in `AGENTS.md`.

OpenCode also supports compatibility locations, including `.claude/skills/...` and `.agents/skills/...`.

### Amp (Sourcegraph Amp)

1. Install Amp (if needed):

```bash
curl -fsSL https://ampcode.com/install.sh | bash
```

2. Place the skill at:
   - Project: `.agents/skills/xtool-ios-build/SKILL.md`
   - User: `~/.config/agents/skills/xtool-ios-build/SKILL.md`
3. Optional: repo/user instructions can go in `AGENTS.md`.

## Tool-specific docs

- Claude Code memory: https://code.claude.com/docs/en/memory
- Claude Code skills: https://code.claude.com/docs/en/skills
- Codex CLI: https://developers.openai.com/codex/cli
- Codex AGENTS.md: https://developers.openai.com/codex/guides/agents-md
- Codex skills: https://developers.openai.com/codex/skills
- OpenCode rules: https://opencode.ai/docs/rules/
- OpenCode skills: https://opencode.ai/docs/skills/
- OpenCode config: https://opencode.ai/docs/config/
- Amp manual: https://ampcode.com/manual
