---
name: running-plans
description: Plans and carries out coding work by splitting it into chunks, matching thinking effort to each chunk, having each chunk reviewed, and bringing the user in only when an agreed assumption changes. Use when an agreed coding task has more than one step or touches several parts of the code, including small plans. Not needed for a single quick edit.
---

# Running plans

Start from an aligned request. If the goal and its load-bearing assumptions haven't been agreed, use the aligning skill first. For a small task, state the goal and your least certain assumption in one line and carry on without waiting.

## Plan

- Lead with the goal (why), then the chunks (what). Keep the how inside each chunk.
- Split the work into chunks that can each be finished and checked on their own, each with a clear "done when". A small task can be a single chunk.
- For each chunk, note which agreed assumptions it depends on.
- Show the plan in plain language and get a yes before starting. If you just confirmed assumptions with the aligning skill, include the plan there so the user answers once; in plan mode, the plan-approval prompt is the yes. For a single chunk where a wrong guess would be cheap to fix, say what you'll do in a sentence and start.

## Match thinking to the work

Agents misjudge how much effort a task needs unless they have a rule, so use this one:

- **Low:** quick, mechanical changes, such as a rename or a lookup.
- **Medium:** clearly scoped, everyday work.
- **High:** work where correctness matters or edge cases are likely: tricky bugs, design decisions, anything touching data, money, or security.
- **Higher levels:** only for the hardest problems; they can overthink.

Aligning and planning usually run fine at the session's current level. For the work itself, run hard chunks in helper agents (subagents) set to the level they need, where your tool lets you set it. If the whole plan is hard and you'll do it in the main conversation, recommend in one line that the user raise the session's effort level before you start.

## Run each chunk

- Give each helper agent the goal, the assumptions its chunk depends on, its done-when, what's out of scope, and the format to report back in. Helpers can't ask the user anything, so tell them: if an agreed assumption turns out wrong, stop and report back rather than guess.
- Run chunks in parallel only when they don't edit the same files or share state like a database or dev server. Otherwise run them one after another, or give each its own git worktree if your tool supports it.
- Have a separate reviewer check each finished chunk in a fresh context, against its done-when, the agreed assumptions, and the project's coding principles. The reviewer reports problems that affect correctness or the goal; anything else is optional. Match the review to the chunk: a small, low-risk chunk needs only a quick, low-effort review.
- Fix what the review finds. Re-review only substantial fixes; after two rounds, move on and list what's still open.
- Ask detail questions as soon as the work reaches them, not late in the work, when the answers matter less.

## Bring the user in when a why changes

Check in when:

- a load-bearing assumption turns out to be wrong, or you want to change it;
- a chunk reveals something that changes what the user would want;
- a step would cost money, need a new account or API key, or send the user's data to a new service; or
- the next step is destructive or hard to undo and wasn't approved in the plan, or the work is much bigger than planned.

Don't stop for how-level changes, such as a different library or a different approach that reaches the same goal. Handle those and mention them in the final summary. The exception is a how-level change that is destructive, hard to undo, or costs money: that is still a check-in.

While you wait for an answer, keep working on whatever doesn't depend on it, and pause only what does.

When you check in, use this order and ask one question:

> **Why it matters:** [the effect on the user's goal, in one or two plain sentences]
> **What changed:** [the assumption we had, and what we found instead]
> **What I suggest:** [the option you recommend, and the alternative]
>
> [one yes/no or pick-one question]

## Finish

Lead with what it means for the user's goal: what now works. Then say what changed and, in one line, how it was checked. Then list any assumptions that changed along the way and any how-level decisions worth knowing about.

End with a final check the user can answer quickly:

> **What changed:** [a few short lines]
> **Matters most:** [the one change that most affects the goal and assumptions agreed at the start, and why]
>
> [the one question whose answer would confirm that change is right]
