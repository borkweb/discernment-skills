---
name: check-against-discernment
description: Use when the user has a plan, proposal, spec, P2 post, or roadmap and wants to audit it against the discernment they've already encoded for this domain. Triggered by "does this plan hold up", "audit this against my discernment", "check this proposal", "does this address what I care about", or any moment when a draft needs to be tested against the user's stated criteria. Reads the plan's discernment-<slug>.md file and surfaces gaps between what the plan addresses and what the user said counts. Use this when auditing a written plan or proposal against an existing discernment-<slug>.md file; to pressure-test a bare answer or recommendation with no recorded discernment, use cross-check-the-signal.
---

# Check against discernment

The user has already encoded what a good answer looks like for this domain — criteria, signal sources, validation bar, the part only they can decide. This skill takes a plan and audits it against that encoded discernment.

## Steps

1. Decide which discernment to audit against — deterministically, in this order. **Don't infer if the user has been explicit:**
   1. If the user pasted the discernment content as text, or named a specific file (e.g. `discernment-pricing.md` or a path), use exactly that. If a named file isn't found, say so and re-list the available `discernment-*.md` files (drop to step 2) — don't treat a typo'd name as "no discernment encoded."
   2. Otherwise, ask which discernment file to use — and list the `discernment-*.md` files in the working directory so they can pick one. Ask even when only one file exists; don't auto-select it.
   3. Only if the user still doesn't name one (e.g. "you pick"), fall back to inference: glob `discernment-*.md`; if exactly one exists, use it; if several, match the one whose decision fits the plan under review, and if none clearly fits, return to step 2 rather than guessing.

   Treat the chosen discernment as insufficient to audit against if it doesn't exist, or if any of the three sections — Aim, Cross-check, Own — is empty or placeholder-only. If so, stop, name which section is missing and which skill fills it (`aim-the-question`, `cross-check-the-signal`, `own-the-call`), and don't run an audit against a hollow file.

2. Ask for the plan, proposal, or draft to audit. Get the actual text or file path.

3. For each section of that file, check the plan against it:
   - **Against Aim**: Does the plan answer the question the user said they'd ask, or a generic version? Are the signal sources cited? Are any noise sources leaning on the argument — and if a noise source is the *primary or sole* justification (not just mentioned in passing), flag it as a top-tier gap, because the decision is resting on evidence the user chose to exclude.
   - **Against Cross-check**: Does the plan show its validation work? Does it meet the validation bar set for this stakes level? Where are unaddressed disagreements?
   - **Against Own**: Does the plan respect the part only the user can decide, or does it route around it? Does it commit the user to something their judgment said they wouldn't? Watch for verb-level reversals of the encoded call — e.g. "defer" encoded but "cancel" in the plan, "timebox" encoded but "open-ended" in the plan — and quote both words side by side.

4. Return a gap report as a table. Three columns: what the user encoded, what the plan addresses, what's missing or mismatched. Be specific — quote the plan and quote the discernment-file line it's failing. Order the rows worst-first: lead with anything that violates `The call` or the validation bar. If the plan makes material commitments that no encoded criterion covers, add them in a final row marked "unscored by your discernment — decide if it belongs" rather than dropping them silently.

5. Close with one line: the single highest-priority gap to fix before this plan ships.
