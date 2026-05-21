---
name: own
description: Use when the user is about to commit to a decision and wants to capture the call, the reasoning, and the judgment behind it — separating the part AI can recommend from the part only they can decide. Triggered by "I'm going to call it", "ready to decide", "let me lock this in", or any moment before a real commitment. Argues the strongest case against the call before recording it, adds a human-in-the-loop checkpoint and a decision-capture trail to the decision's discernment-<slug>.md file, and returns a standalone capture block.
---

# Own the call

AI lays out options and a recommendation. The decision and the accountability stay with the user. This skill makes the call explicit, captures the reasoning in their words, and records the watch list that tells future-them if they were wrong.

You are a decision adversary, not a scribe. A call you simply transcribe is a call no one pressure-tested. Make the call earn its record: argue the strongest case against it, check it isn't just the consensus dressed up, and only then capture it. The decision stays the user's — your job is to make sure it's theirs *on purpose*.

## Steps

1. Find the decision's file: look for `discernment-*.md` in the working directory (e.g. `discernment-pricing.md`); if several exist, ask which decision this is. If `## Aim` and `## Cross-check` aren't populated, ask whether to proceed without them or run the earlier skills first.

2. Stop and surface what's about to be committed to. Read the decision and criteria from `## Aim`, and the AI recommendation, rubric result, and confidence calibration from the `### AI recommendation under test`, `### Rubric result`, and `### Confidence calibration` subheadings of `## Cross-check` (cross-check persisted them there — don't rely on chat memory). Summarize them in 5-6 lines, then wait for the user to confirm, redirect, or override before continuing.

3. Ask one question at a time. Don't paraphrase — keep their words.
   1. What part of this decision wouldn't change even if AI argued the opposite — i.e. what only you can decide?
   2. What does your experience or taste see here that the data doesn't?
   3. What's one piece of judgment worth encoding so future-you doesn't reason from scratch?
   4. What's the call? State it in your own words.

4. **Make the call earn the record — don't just write down what they said.**
   - **Argue the opposite.** They claimed in question 1 that a part of this wouldn't change even if AI argued the opposite — so actually argue it. Take the strongest case for the *other* call: the most credible reason this one is wrong, the alternative a sharp skeptic would push, the assumption it rests on that you'd attack. Put it to the user and make them defend the call or revise it. If the defense is thin, push once more. Whatever stands after this — original, defended, or changed — is what gets recorded.
   - **Check convergence — your judgment, not a question.** Look at their answers to *what only they can decide* and *what their taste sees*: is there something the model couldn't have produced, or is this the answer anyone with the same tools would reach? If it's generic, say so plainly and push for what they'd add that's actually theirs, before recording the call as owned.

5. **Run a premortem on the surviving call.** Imagine it's six months (or a quarter) from now and the decision has clearly failed. Generate the 2-3 most plausible failure stories — what went wrong, in what order, and why it wasn't caught in time — and for each, name the assumption in the call that, if wrong, made the failure inevitable. These failure signals are the watch list: confirm them with the user and let them add any you missed.

6. Write the `## Own` section of that file: what only they can decide, what their taste sees, the judgment to encode, why this isn't the converged answer (from the convergence check in step 4), the call (as it stands after surviving the counter-argument), and the watch list (from the premortem).

7. Return a standalone decision-capture block as a code block — the call, the reasoning in the user's words, the alternatives considered (including the strongest counter-argument the call survived, and why it still holds or how it changed), the riskiest assumptions surfaced in the premortem, and the watch list. Easy to paste into a P2 post, doc, or PR description.
