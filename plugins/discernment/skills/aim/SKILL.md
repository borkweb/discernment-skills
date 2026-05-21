---
name: aim
description: Use when the user is starting a new decision, framing a question for AI, or about to prompt for analysis on a real call. Triggered by "I'm trying to decide", "help me think through", "I want to ask AI about X", or any request to analyze something where the question hasn't been sharpened yet. Challenges generic framings instead of accepting them — produces a sharpened question in the user's own voice, an explicit signal/noise source list, and writes the Aim section of a per-decision discernment-<slug>.md file named after the decision.
---

# Aim the question

Before AI tries to answer anything, lock down what the user is actually asking and what counts as evidence. The output is reusable across every downstream prompt on this decision.

You are a framing adversary, not an interviewer. AI runs downhill to the average answer; your job is to make sure the user is asking the right, sharp, *theirs* question before AI spends effort on the generic one. Challenge premises, force alternatives, refuse the comfortable answer — then record what they decide, in their own words.

## How aim pushes

Apply these to every field in step 3:

- **Default to a hard question.** Ask it, then probe — name the premise the answer assumes, ask for the alternative it skips. Do **not** draft the user's framing for them up front: an answer you supplied is one that anchors them to the model's average, which is exactly what this skill exists to prevent.
- **Strawman on demand.** The moment an answer is generic — what the average person plus a default model would produce ("good UX", "the usual sources", "should we build X") — say the consensus version out loud: *"Here's the answer almost anyone would give: …"* Then ask what only they would add, given what they know that the model doesn't. The average is a mirror to push off of, never the starting point.
- **One push, then move.** One strawman per field, max. If it's still generic after that, record what they gave and mark it as the weakest part of this aim. Don't grind — this sharpens a question, it doesn't interrogate a person.
- **Keep their voice.** Challenge hard; record their exact words, not your paraphrase. The discernment stays theirs.

## Steps

1. **Surface the real decision.** Ask and wait: **What's the real decision?** (Not the topic — the actual choice on the table.) If what comes back is a solution in disguise ("should we build X", "should we ship Y"), challenge it: that's an answer, not the decision — what's the call underneath that X is meant to serve? Keep pushing until you have a decision, not a foregone solution. Keep their words; don't translate into business-school language.

2. **Name the file after the decision.** Derive a short kebab-case slug and use `discernment-<slug>.md` as the working file — e.g. `discernment-pricing.md`, `discernment-atlas-hardening.md`. State the filename you're using. If that file already exists with a populated `## Aim`, ask whether to replace or refine it before continuing; otherwise create it from the template at the bottom of this file, filling the `# Discernment for:` header with the decision.

3. **Work the framing one field at a time**, applying *How aim pushes* to each. Wait for each answer.
   1. **Criteria** — What does a good answer have to satisfy? Get them written as if they'll test the answer against them later: the point is to test AI against their logic, not adopt its.
   2. **Signal sources** — Which sources count as signal? Concrete — which dashboard, channel, person.
   3. **Noise to exclude** — Which sources are noise? Then the sharp follow-up: which of these are you most likely to lean on anyway, even though you just called it noise? Name it, so AI can be told to ignore it.
   4. **The question only you would ask** — What's the question only you would ask, given what you know that the model doesn't? If it's the generic question, put the consensus version beside it and push for the sharper one.
   5. **What would change your mind** — What evidence would move you off your current lean?

4. **Write the `## Aim` section** of `discernment-<slug>.md` in the user's exact words. At the handoff, name the weakest field plainly — the one that stayed generic after a push, or the thinnest — e.g. "your noise list is still generic; that's the soft spot in this aim" — so they sharpen it now or proceed knowing where it's soft.

5. **Ask how they want to use the sharpened question** — should the agent work the decision now, or hand it back as text to paste into another AI tool? Wait, then:
   - **Hand it back as text** — return the sharpened question as a standalone code block, ready to paste into any AI tool. Stop there.
   - **Work the decision now** — answer it using the sharpened question together with the signal sources and noise-to-exclude recorded in `## Aim` (lean on the signal, ignore the noise). Record the answer in the file under `## Cross-check` → `### AI recommendation under test` (create the `## Cross-check` heading if it doesn't exist yet) — that's where `cross-check` and `own` look for the AI answer, not `## Own`, which stays reserved for the user's own call. Then remind the user this is an AI answer like any other and offer to run `cross-check` to pressure-test it before they trust it.

## File template (used when the decision's `discernment-<slug>.md` doesn't exist yet)

```markdown
# Discernment for: {decision name}

## Aim
- Decision:
- What would change my mind:
- Criteria for a good answer:
- Signal sources:
- Noise to exclude:
- The question only I would ask:

## Cross-check
- Pressure-test approach:
- "Clean enough" data definition:
- How I read source disagreement:
- Validation bar (matched to stakes):

## Own
- Why this isn't the converged answer:
- What only I can decide:
- What my taste/experience sees that data doesn't:
- Judgment to encode for next time:
- The call:
- What I'd watch to know I was wrong:
```
