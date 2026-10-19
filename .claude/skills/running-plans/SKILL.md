---
name: running-plans
description: Plans and carries out coding work by splitting it into chunks, choosing how much thinking each chunk needs, having a separate reviewer check each chunk, and bringing the user in only when an agreed assumption changes. Use when turning an approved request into a coding plan or carrying one out, for small plans as well as large ones.
---

# Running plans

Start from an aligned request. If the goal and its load-bearing assumptions haven't been confirmed with the user, use the aligning skill first. For a small task, a one-line confirmation is enough.

## Plan

- Lead with the goal (why), then the chunks (what). Keep the how inside each chunk.
- Split the work into chunks that can each be finished and checked on their own, each with a clear "done when". A small task can be a single chunk.
- For each chunk, note which agreed assumptions it depends on.
- Decide how much thinking each chunk needs. Routine edits and lookups need little; unclear or high-risk work (design decisions, tricky bugs, anything touching data or security) needs more. Where your tools allow it, set the model or effort level for each subagent to match.
- Show the plan in plain language and get a yes before starting. For a one-chunk task, a sentence is enough.

## Run each chunk

- Do the work, or hand it to a subagent with the goal, the assumptions it depends on, its done-when, and the project's instruction files (AGENTS.md or CLAUDE.md). Run independent chunks in parallel.
- Have a separate reviewer check each finished chunk in a fresh context, against its done-when, the agreed assumptions, and the project's coding principles. The reviewer reports problems that affect correctness or the goal; anything else is optional.
- Fix what the review finds before moving on.

## Bring the user in when a why changes

Stop and check in when:

- a load-bearing assumption turns out to be wrong, or you want to change it;
- a chunk reveals something that changes what the user would want; or
- the next step is destructive, hard to undo, or much bigger than planned.

Don't stop for how-level changes, such as a different library or a different approach that reaches the same goal. Handle those and mention them in the final summary.

When you check in, use this order and ask one question:

> **Why it matters:** [the effect on the user's goal, in one or two plain sentences]
> **What changed:** [the assumption we had, and what we found instead]
> **What I suggest:** [the option you recommend, and the alternative]
>
> [one yes/no or pick-one question]

## Finish

Lead with the outcome in plain language: what now works, and how it was checked. Then list any assumptions that changed along the way and any how-level decisions worth knowing about.
