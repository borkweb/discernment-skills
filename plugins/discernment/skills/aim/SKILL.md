---
name: aim
description: Use when the user is starting a new decision, framing a question for AI, or about to prompt for analysis on a real call. Triggered by "I'm trying to decide", "help me think through", "I want to ask AI about X", or any request to analyze something where the question hasn't been sharpened yet. Produces a sharpened question in the user's own voice, an explicit signal/noise source list, and writes the Aim section of a per-decision discernment-<slug>.md file named after the decision.
---

# Aim the question

Before AI tries to answer anything, lock down what the user is actually asking and what counts as evidence. The output is reusable across every downstream prompt on this decision.

## Steps

1. Ask the first question and wait: **What's the real decision?** (Not the topic — the actual choice on the table.) Keep the user's own words; don't paraphrase into business-school language.

2. Name the file after the decision. Derive a short kebab-case slug from the decision and use `discernment-<slug>.md` as the working file — e.g. `discernment-pricing.md`, `discernment-atlas-hardening.md`. State the filename you're using. If that file already exists with a populated `## Aim`, ask whether to replace or refine it before continuing; otherwise create it from the template at the bottom of this file, filling the `# Discernment for:` header with the decision.

3. Ask the rest one question at a time. Wait for each answer. Don't paraphrase — keep their voice.
   1. What does a good answer have to satisfy? Write criteria as if you'll test the answer against them later.
   2. Which sources count as signal? Be concrete — which dashboards, channels, people.
   3. Which sources are noise — what should AI ignore on this decision?
   4. What's the question only you would ask, given context the model doesn't have?

4. If any answer is generic ("good UX", "more data", "the usual sources"), ask ONE sharper follow-up before moving on. Only one.

5. Write the `## Aim` section of `discernment-<slug>.md` using the user's exact words.

6. Ask the user how they want to use the sharpened question: should the agent take it from here and work the decision now, or hand it back as text to paste into another AI tool? Wait for the answer.

7. Then, depending on the answer:
   - **Hand it back as text** — return the sharpened question as a standalone code block, ready to paste into any AI tool. Stop there.
   - **Work the decision now** — answer it using the sharpened question together with the signal sources and noise-to-exclude recorded in `## Aim` (lean on the signal, ignore the noise). Record the answer in the file under `## Cross-check` → `### AI recommendation under test` (create the `## Cross-check` heading if it doesn't exist yet) — that's where `cross-check` and `own` look for the AI answer, not `## Own`, which stays reserved for the user's own call. Then remind the user this is an AI answer like any other and offer to run `cross-check` on it to pressure-test it before they trust it.

## File template (used when the decision's `discernment-<slug>.md` doesn't exist yet)

```markdown
# Discernment for: {decision name}

## Aim
- Decision:
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
- What only I can decide:
- What my taste/experience sees that data doesn't:
- Judgment to encode for next time:
- The call:
- What I'd watch to know I was wrong:
- Revisit by:
```
