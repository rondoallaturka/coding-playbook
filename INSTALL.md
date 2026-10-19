# Installing the coding playbook

This file is for an agent setting up the coding playbook on a user's machine. Read it in full before changing anything.

## What's here

| File | What it does | Usual home |
| --- | --- | --- |
| `personal/communication.md` | How the user wants agents to talk to them and ask questions, in every Claude Code session on this computer, coding or not | Personal `~/.claude/CLAUDE.md` |
| `.claude/skills/aligning/` | Aligning with the user before a plan: one Socratic question at a time, then a yes/no on the load-bearing assumptions | Personal skills (not coding-specific) |
| `.claude/skills/running-plans/` | Running coding plans: chunks, effort per chunk, a reviewer per chunk, check-ins when a why changes | Personal skills, or per project |
| `.claude/skills/debugging/` | Finding and fixing root causes | Personal skills, or per project |
| `.claude/skills/building-ui/` | UI states, accessibility, looking at the result | Personal skills, or per project |
| `AGENTS.md` (imported by `CLAUDE.md`) | Coding principles | Each project's root, or personal `~/.claude/CLAUDE.md` |

Pick one home for each piece. A personal skill hides a project skill with the same name, and an `AGENTS.md` that is in both `~/.claude/CLAUDE.md` and a project loads twice.

Claude Code looks for personal skills at `~/.claude/skills/<name>/SKILL.md`. Keep the clone of this repo outside `~/.claude/skills/`, at a path that won't move (for example `~/code/coding-playbook`), on the `main` branch. Links into it stop working if it moves.

## Where this reaches

Files in `~/.claude/` apply to Claude Code on this computer. Personal skills there don't load in Cowork or cloud sessions, and Cowork skips `@` imports in `~/.claude/CLAUDE.md` that point outside the session folder. If the user wants these rules there too, paste the text of `communication.md` into `~/.claude/CLAUDE.md` instead of importing it, and add the skills to their claude.ai account. If you add a skill to the account, don't also install it in `~/.claude/skills/`, or it shows up twice.

## Start with an alignment session

Before changing any settings, follow `.claude/skills/aligning/SKILL.md` with the user. Read their setup first: `~/.claude/CLAUDE.md`, `~/.claude/skills/`, and the instruction files of any projects they name. Then cover:

1. **What overlaps or conflicts.** Look for older versions of these rules (for example a `coding-principles` skill), and compare skill descriptions as well as contents: two skills that trigger on the same words compete. Conflicting instructions make agents pick one at random.
2. **Personal or per project** for each piece.
3. **Copy or link.** Linking keeps the user's setup current when they `git pull` this repo; copying lets them edit freely.

Recommend an answer to each in plain words (for example, "I suggest linking, so you get updates automatically") and ask only for a yes. For conflicts, propose a decision for each in one list, usually replacing the older rule, and ask once. Ask separately only where the user's intent is unclear. Then confirm the full list of what will change where, and wait for a yes.

Skills under `~/.claude/skills/synced/` (shown as `anthropic-skills:<name>`) come from the user's claude.ai account. Don't edit or delete them on disk: changes aren't saved, and the next sync overwrites them. If one should go, ask the user to turn it off in their claude.ai skill settings.

## Make the changes

- Merge into existing files rather than overwriting them, and show the user what changed.
- Make sure every file you edit is backed up or tracked in git first, so it can be undone.
- To link: in `~/.claude/CLAUDE.md`, add an import with a full path starting with `~/`, such as `@~/code/coding-playbook/personal/communication.md`; put a backslash before any space in the path. For each skill, run `ln -s ~/code/coding-playbook/.claude/skills/<name> ~/.claude/skills/<name>`.
- Afterwards, ask the user, in plain steps, to open a new Claude Code session and type `/context` (the instruction files should be listed under memory files) and `/skills` (aligning, running-plans, debugging, and building-ui should be listed).
