---
name: cross-check
description: Use when the user has an AI-generated answer, analysis, or recommendation they need to pressure-test before trusting. Triggered by "is this right", "pressure-test this", "I don't trust this answer", "validate this", or any moment where confidence and correctness need to be separated. Runs a validation rubric and an adversarial pass over the answer, then writes the Cross-check section of the decision's discernment-<slug>.md file. Use this for a standalone answer or recommendation; to audit a written plan, proposal, or roadmap against discernment already recorded in a discernment-<slug>.md file, use analysis.
---

# Cross-check the signal

AI hands back something confident. This skill separates confidence from correctness — by validating the data underneath and arguing the strongest case against the answer.

## Steps

1. Find the decision's file: look for `discernment-*.md` in the working directory (e.g. `discernment-pricing.md`). If exactly one exists, use it; if several, ask which decision this answer belongs to; if none exists or its `## Aim` is empty, ask the user to run `aim` first, or to give the decision context inline. Use the `## Aim` section to know what the user already decided counts as a good answer and which sources are signal.

2. Get the AI-generated answer or analysis on the table verbatim. If `### AI recommendation under test` is already populated under `## Cross-check` — e.g. `aim` answered the decision directly — use that and confirm it with the user, rather than re-asking; otherwise ask the user for the answer.

3. Ask one question at a time. Don't paraphrase.
   1. How would you pressure-test this answer? What would you check first?
   2. What does "clean enough" data look like for this decision? When would you walk away?
   3. Where are your sources likely to disagree on this — and how do you read disagreement?
   4. What's the validation bar that matches the stakes? Low and reversible gets a glance; high and hard-to-undo gets the full interrogation.

4. Run the rubric. For each criterion the user named in `## Aim`, mark pass / fail / uncertain against the AI answer. Surface which failed and why.

5. Calibrate confidence. Go through the AI answer claim by claim and tag each substantive claim: **high** (verified against a signal source named in `## Aim`, or directly observable), **medium** (inferred from pattern or adjacent evidence), **low** (filling a gap — best guess, please verify). For every low- and medium-confidence claim, note what would raise it: a source to check, a test to run, a person to ask. Don't smooth the uncertainty out — if a claim is a guess, it should read like one. This is what tells the user where to spend verification time and where they can move fast.

6. Run the adversarial pass. Take the role of a skeptical reviewer who disagrees with this answer. Argue the strongest case against it — the assumptions most likely to fail, the evidence that's missing, the decisions that would look wrong in hindsight. Return the pushback and the original answer side by side.

7. Write the `## Cross-check` section of that file with the user's pressure-test approach, "clean enough" definition, disagreement read, and validation bar — then record, in the same section and under these exact subheadings so `own` can find them: `### AI recommendation under test` (the answer verbatim, or a one-line summary), `### Rubric result` (which criteria passed / failed / uncertain), and `### Confidence calibration` (the per-claim tags). These have to survive in the file, not just in this chat.
