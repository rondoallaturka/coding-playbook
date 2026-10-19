---
name: aligning
description: Aligns with the user on what they actually want before planning or doing work where a wrong guess about the goal would waste real effort. Asks Socratic questions one at a time, then confirms the load-bearing assumptions in plain language. Use before drafting a plan for such work, or when the user asks to align before starting.
---

# Aligning

The goal is a shared understanding of what the user wants and why, before any plan exists. Plans most often go wrong because one load-bearing assumption was wrong and the user never saw it, either because it was buried in detail or because it was never stated. This skill makes those assumptions visible and gets them confirmed.

## Start light

Begin with a quick pass: restate the request in a sentence and find what you're least sure about. Look things up before asking: find out what the code, files, and tools can tell you, and save your questions for intent, priorities, and tradeoffs.

If a wrong guess would be cheap to fix, stop there: say what you'll do and your least certain assumption, then do it. Otherwise, ask questions only where you find real uncertainty, then confirm as below.

## One question at a time

- Each message asks exactly one question. If you use a question tool with options (like AskUserQuestion), put one question in it.
- Before writing it, decide which question would change the plan most if answered, and ask that one.
- Include your own view: what you'd suggest and why, or two to four options. Questions with no point of view frustrate people.
- After each answer, stop and think: what did this change, what is most uncertain now, and is it still worth asking? Reflect back what you heard in a sentence before the next question.
- Settle goals and constraints here. Questions about details can wait until the work reaches them.

## Socratic, from first principles

- Start from the underlying goal: what problem the user is solving and why it matters to them, before features or methods.
- Help the user think, not just answer. When a request rests on an assumption, ask the question that makes them examine it. They may not have worked out their own principles for this yet; helping them do that is part of the job.
- Test their thinking where it matters, but don't argue past one round. Their answer decides.

## What counts as load-bearing

An assumption deserves the user's attention when:

- much of the work depends on it, so being wrong would waste or undo a lot; or
- it reflects a belief about what matters (a first principle) that the user hasn't confirmed.

Technical choices the user doesn't care about are yours to make.

## Stop at 80/20

Don't get stuck in a question loop. Once the answers that drive most of the value are settled, stop asking and confirm. Tag each assumption by where it came from, because your own sense of certainty is unreliable; the important guesses are the ones to flag.

> Here's what I understand:
> - **Goal:** [why this matters, in one line]
> - [the few assumptions that matter, usually 2 to 5, each tagged *you said*, *from the code*, or *my guess*]
> - ⚠️ **Least certain:** [the important guesses]
>
> Is this right? Yes, or tell me what's off.

- If the user says yes, move on. If they correct something directly, update the list and move on; confirm again only if the correction changes other assumptions. If they say it's off without saying how, ask the one question that best resolves it.
- If a plan follows, put its outline under this confirmation so the user approves once.
- For work with several parts, save the goal, the assumptions, and what's out of scope to a short file that the plan, any helper agents, and reviewers can read.
