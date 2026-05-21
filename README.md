# Discernment Skills

A Claude Code [plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces) providing five composable skills for **discernment** — the work of deciding *well* when an AI is happy to hand you a confident answer for everything.

The skills don't make the call for you. They sharpen the question before you prompt, separate confidence from correctness after you get an answer, keep the decision and the accountability with you, let you audit a later plan against the judgment you encoded, and score the call once it has played out so the judgment gets corrected by reality.

## The shape

Three single-purpose skills compose by writing into a per-decision file named after the decision. `revisit` reopens that file later to score the call against what happened; `analysis` audits any plan against it.

```
aim               →  writes ## Aim          ┐
cross-check       →  writes ## Cross-check  ├─→  discernment-<slug>.md
own               →  writes ## Own          ┘            │
                                                         ├─→  revisit   ─→  scores the call later, writes ## Revisit
                                                         └─→  analysis  ─→  audits a plan against it
```

Each of the first three is independently useful — run `aim` on a decision and stop there if that's all you need. They compose because they share one file format.

## The five skills

| Skill | Use when | Writes |
|-------|----------|--------|
| **`aim`** | Starting a decision or framing a question for AI | `## Aim` |
| **`cross-check`** | You have an AI answer you need to pressure-test | `## Cross-check` |
| **`own`** | About to commit to a decision | `## Own` |
| **`revisit`** | A past call has had time to play out and you want to score it | `## Revisit` |
| **`analysis`** | You have a plan/proposal to audit against what you already encoded | reads all sections |

## The decision file

Each decision gets its own file, named after it: `discernment-<slug>.md` (e.g. `discernment-pricing.md`, `discernment-atlas-hardening.md`). `aim` derives the slug from the decision and creates the file from this template; the other skills locate it by globbing `discernment-*.md` and append to it.

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

`revisit` later appends a timestamped `## Revisit — YYYY-MM-DD` section each time you score the call against what happened; these stack, so one decision can carry several.

**Multiple parallel decisions:** each lives in its own `discernment-<slug>.md`, so they don't collide. When more than one exists in a directory, the reading skills ask which decision you mean (or you can name the file).

## Install

```bash
# Add this repo as a marketplace (local path, GitHub shorthand, or git URL all work)
/plugin marketplace add borkweb/discernment-skills
#   or, from a local clone:
/plugin marketplace add /path/to/discernment-skills

# Install the plugin
/plugin install discernment@discernment-skills
```

Once installed, the skills are namespaced under the plugin:

- `/discernment:aim`
- `/discernment:cross-check`
- `/discernment:own`
- `/discernment:revisit`
- `/discernment:analysis`

They also trigger automatically when your request matches their description (e.g. "help me think through whether to…", "is this answer right?", "I'm going to call it").

## A full pass

1. **Aim** — `aim` walks you through the real decision, your criteria, your signal vs. noise sources, and the question only you would ask. It hands back a sharpened prompt and seeds the decision's `discernment-<slug>.md`.
2. **Cross-check** — paste an AI answer into `cross-check`. It scores the answer against your own criteria and argues the strongest case against it, side by side.
3. **Own** — `own` stops before commitment, surfaces what's on the table, and captures the call, the reasoning in your words, the watch list that'll tell future-you if you were wrong, and a `Revisit by:` date.
4. **Revisit** — when that date comes due, run `revisit`. It walks your watch list against what actually happened, renders a verdict, reads how well-calibrated you and the AI were, and appends a `## Revisit` section so the lesson sticks.
5. **Audit anytime** — run `analysis` on a plan, proposal, or P2 post. It returns a gap report: what you encoded vs. what the plan addresses vs. what's missing.

## Repository layout

```
discernment-skills/
├── .claude-plugin/
│   └── marketplace.json              # marketplace catalog
├── plugins/
│   └── discernment/
│       ├── .claude-plugin/
│       │   └── plugin.json           # plugin manifest
│       └── skills/
│           ├── aim/SKILL.md
│           ├── cross-check/SKILL.md
│           ├── own/SKILL.md
│           ├── revisit/SKILL.md
│           └── analysis/SKILL.md
├── README.md
└── LICENSE
```

## License

MIT — see [LICENSE](LICENSE).
