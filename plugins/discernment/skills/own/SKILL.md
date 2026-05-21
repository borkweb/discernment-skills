---
name: own
description: Use when the user is about to commit to a decision and wants to capture the call, the reasoning, and the judgment behind it — separating the part AI can recommend from the part only they can decide. Triggered by "I'm going to call it", "ready to decide", "let me lock this in", or any moment before a real commitment. Adds a human-in-the-loop checkpoint and a decision-capture trail to the decision's discernment-<slug>.md file and returns a standalone capture block.
---

# Own the call

AI lays out options and a recommendation. The decision and the accountability stay with the user. This skill makes the call explicit, captures the reasoning in their words, and records the watch list that tells future-them if they were wrong.

## Steps

1. Find the decision's file: look for `discernment-*.md` in the working directory (e.g. `discernment-pricing.md`); if several exist, ask which decision this is. If `## Aim` and `## Cross-check` aren't populated, ask whether to proceed without them or run the earlier skills first.

2. Stop and surface what's about to be committed to. Read the decision and criteria from `## Aim`, and the AI recommendation, rubric result, and confidence calibration from the `### AI recommendation under test`, `### Rubric result`, and `### Confidence calibration` subheadings of `## Cross-check` (cross-check persisted them there — don't rely on chat memory). Summarize them in 5-6 lines, then wait for the user to confirm, redirect, or override before continuing.

3. Ask one question at a time. Don't paraphrase.
   1. What part of this decision wouldn't change even if AI argued the opposite — i.e. what only you can decide?
   2. What does your experience or taste see here that the data doesn't?
   3. What's one piece of judgment worth encoding so future-you doesn't reason from scratch?
   4. What's the call? State it in your own words.
   5. What would you watch to know you were wrong?
   6. When should future-you check back on this — a date, or a trigger that means it's time?

4. Run a premortem on the call. Imagine it's six months (or a quarter) from now and this decision has clearly failed. Generate the 2-3 most plausible failure stories — what went wrong, in what order, and why it wasn't caught in time. For each, name the assumption in the call that, if wrong, made the failure inevitable. Show these to the user and use them to sharpen the watch list from question 5: the failure signals are the things they watch for.

5. Write the `## Own` section of that file with: what only they can decide, what their taste sees, the judgment to encode, the call, the watch list (now drawn from the premortem), and the `Revisit by:` date — so `revisit-the-call` knows when to reopen it and score the call.

6. Return a standalone decision-capture block as a code block — the call, the reasoning in the user's words, the alternatives considered, the riskiest assumptions surfaced in the premortem, the watch list, and the date to revisit. Easy to paste into a P2 post, doc, or PR description.
