# Coding playbook

Instruction files for AI coding agents (Claude Code, Cursor, Codex): a short set of working principles that loads in every session, and two skills that load only when they're relevant.

| File | Loads | Covers |
| --- | --- | --- |
| `AGENTS.md` | Every session | Scope, fitting the codebase, errors, tests, UI basics, communication |
| `CLAUDE.md` | Every session in Claude Code | Imports `AGENTS.md`, so Claude Code always reads it |
| `.claude/skills/debugging/` | When debugging | Reproduce, investigate, fix, verify, report |
| `.claude/skills/building-ui/` | When building or changing UI | Looking at the result, UI states, accessibility, design fit |

## Add to a project

From the project's root:

```bash
GUIDE=/path/to/this/repo
cp "$GUIDE/AGENTS.md" .
mkdir -p .claude/skills && cp -r "$GUIDE/.claude/skills/." .claude/skills/
[ -f CLAUDE.md ] || cp "$GUIDE/CLAUDE.md" .
```

Then:

1. Add a short section at the top of `AGENTS.md` with the project's build, test, lint, and run commands, plus anything an agent can't work out from the code: required environment variables, generated files not to edit, services to start. This is the most valuable part of the file, and the one part a template can't supply.
2. If the project already had a `CLAUDE.md`, add the line `@AGENTS.md` to it.
3. For Codex, which reads skills from `.agents/skills/`, also run `mkdir -p .agents && ln -s ../.claude/skills .agents/skills` (or copy the folder). Cursor reads `AGENTS.md` and `.claude/skills/` as they are; it also reads `.agents/skills/`, so with the link it may list each skill twice.

## Why it's built this way

- **A short always-on file, with procedures in skills.** Everything in `AGENTS.md` costs context in every session, and long instruction files get followed less reliably. Procedures that only apply sometimes load when they're needed.
- **Plain language, no ALL CAPS.** Current models follow instructions closely, and emphatic wording makes them over-apply rules. The files give reasons instead of raising their voice.
- **Effort matches the problem.** The debugging skill runs from "reproduce, fix, verify" for an obvious bug up to hypothesis-driven investigation for a hard one, instead of one fixed procedure for everything.
- **Every task has a real check.** For a bug, it's a reproduction that fails before the fix and passes after. For UI, it's looking at the rendered result in each state. Gaming the check (editing tests, suppressing errors, special-casing inputs) is ruled out explicitly, because it's the most common way agents go wrong.
- **No contradictions.** The files agree with each other, and where they differ from a project's own conventions, the project wins.
- **Hard guarantees belong in tooling.** Instructions are advisory. Anything that must never happen, like writing to production, editing migrations, or force-pushing, should be blocked with permissions or hooks, not with a sentence here.

## Keeping it useful

- Add a rule only after an agent makes the same mistake twice, and cut any rule the agent already follows without being told.
- Try a change on a few real tasks, with and without it, and keep it only if the agent's behavior improves.
- In Claude Code, `/doctor prompt-audit` flags instructions that are outdated, conflicting, or point at files that don't exist.

## Sources

- Anthropic: [Claude Code best practices](https://code.claude.com/docs/en/best-practices), [CLAUDE.md and memory](https://code.claude.com/docs/en/memory), [Skills](https://code.claude.com/docs/en/skills), [Skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices), [Prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices), [Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- OpenAI: [Codex best practices](https://developers.openai.com/codex/learn/best-practices), [Codex skills](https://developers.openai.com/codex/skills), [GPT-5 prompting guide](https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide)
- Cursor: [Rules](https://cursor.com/docs/context/rules), [Skills](https://cursor.com/docs/skills)
- Gloaguen et al., [Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?](https://arxiv.org/abs/2602.11988) (ICLR 2026)
- David Agans, *Debugging: The 9 Indispensable Rules* ([review](https://dwheeler.com/essays/debugging-agans.html))
- John Ousterhout and Robert Martin, [A Philosophy of Software Design vs. Clean Code](https://github.com/johnousterhout/aposd-vs-clean-code)
- Nielsen Norman Group, [10 usability heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/)
