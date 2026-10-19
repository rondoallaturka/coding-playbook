# Installing this playbook

This file is for an agent setting up the playbook on a user's machine. Read it in full before changing anything.

## What's here

| File | What it does | Usual home |
| --- | --- | --- |
| `personal/communication.md` | How the user wants agents to talk to them and ask questions, in every session, coding or not | Personal `~/.claude/CLAUDE.md` |
| `.claude/skills/aligning/` | Aligning with the user before a plan: one Socratic question at a time, then a yes/no on the load-bearing assumptions | Personal skills (not coding-specific) |
| `.claude/skills/running-plans/` | Running coding plans: chunks, effort per chunk, a reviewer per chunk, check-ins when a why changes | Personal skills, or per project |
| `.claude/skills/debugging/` | Finding and fixing root causes | Personal skills, or per project |
| `.claude/skills/building-ui/` | UI states, accessibility, looking at the result | Personal skills, or per project |
| `AGENTS.md` (imported by `CLAUDE.md`) | Coding principles | Each project's root, or personal `~/.claude/CLAUDE.md` |

Claude Code looks for personal skills at `~/.claude/skills/<name>/SKILL.md`. A clone of this repo inside `~/.claude/skills/` doesn't load the skills inside it by itself; each skill folder has to be linked or copied there.

## Start with an alignment session

Before changing any settings, follow `.claude/skills/aligning/SKILL.md` with the user: one question at a time, starting light. The user already has instructions and skills of their own, so these questions usually matter most:

1. **What overlaps or conflicts?** First read their `~/.claude/CLAUDE.md`, `~/.claude/skills/`, and the instruction files of projects they name. Look for older versions of these rules, such as a `coding-principles` skill. Conflicting instructions make agents pick one arbitrarily, so each conflict needs a decision: replace, merge, or keep.
2. **Personal or per project?** Personal pieces apply everywhere; project pieces travel with the repo and its team.
3. **Copy or link?** Linking keeps the user's setup current with `git pull` on this repo: `@path/to/file` imports in CLAUDE.md, symlinks for skill folders. Copying lets them edit freely.

Then confirm with a short, plain-language list of what will change where, and wait for a yes.

## Make the changes

- Merge into existing files rather than overwriting them, and show the user what changed.
- Make sure every file you edit is backed up or tracked in git first, so it can be undone.
- Afterwards, start a fresh session and check that the instructions loaded (`/context`) and that the skills are available.
