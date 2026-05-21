---
name: revisit
description: Use when a decision you already made and recorded has had time to play out, and you want to score it against what actually happened. Triggered by "how did that call turn out", "revisit this decision", "was I right", "check back on this", "score that decision", or a discernment file's `Revisit by:` date coming due. Reads the call, watch list, and confidence calibration from a decision's discernment-<slug>.md, walks the watch-list signals against reality, renders a verdict, reads how well-calibrated you and the AI were, and appends a timestamped Revisit section. Use this to close the loop on a past call; to pressure-test a fresh AI answer use cross-check, to audit a written plan use analysis.
---

# Revisit the call

A decision got made and the watch list got written. Time has passed. This skill scores the call against what actually happened — so the judgment you encoded gets corrected by reality instead of calcifying.

## Steps

1. Find the decision's file: look for `discernment-*.md` in the working directory; if several exist, ask which decision this is. The `## Own` section must be populated — if there's no recorded call, there's nothing to revisit; say so and point to `own`. Read the `Revisit by:` date in `## Own`: if it's still in the future, tell the user how long is left and ask whether to revisit early or wait.

2. Read back what was decided — don't rely on chat memory. From `## Own`: the call, what only they could decide, the judgment they encoded, and the watch list. From `## Aim`: the criteria for a good answer. From `## Cross-check`, if present: the `### Confidence calibration` tags. Summarize the call and its watch list in a few lines so the user is scoring against what they actually wrote, not a softened memory of it.

3. Ask one question at a time. Don't paraphrase.
   1. What's actually happened since? Get the outcome or current state on the table.
   2. Walk the watch list one signal at a time: did it fire, not fire, or is it still unclear? These were the things they said would tell them they were wrong.
   3. If `### Confidence calibration` exists: did the claims marked **high** hold up? How did the **low**-confidence ones resolve?

4. Render the verdict: **Right**, **Wrong**, **Mixed**, or **Too early to tell**. If too early — the watch-list signals haven't resolved — don't force it: update the `Revisit by:` date in `## Own` to a new date, say why, and stop here.

5. Read the calibration. In one or two lines each: were *you* over- or under-confident on this call, and was the *AI*? Point at the evidence — a watch-list signal that fired that you'd waved off, a "high" claim that failed, a "low" one you should have trusted. This is the pattern worth carrying into the next decision.

6. Capture the corrected judgment: knowing how it turned out, what would you encode now? Keep the user's own words. If the original judgment held, say so plainly — a confirmed call is a calibration win, not a non-event.

7. Append a timestamped `## Revisit — YYYY-MM-DD` section to the file (multiple revisits stack; never overwrite a prior one or the original `## Own`). Then return a standalone revisit-capture block as a code block, easy to paste into a P2 post, doc, or PR.

## Section appended to the decision's `discernment-<slug>.md`

```markdown
## Revisit — YYYY-MM-DD
- Outcome so far:
- Watch-list signals: <per signal — fired / didn't / unclear>
- Verdict: Right / Wrong / Mixed / Too early to tell
- Calibration: <you and the AI — over- or under-confident, with the evidence>
- Corrected judgment: <what you'd encode now>
```
