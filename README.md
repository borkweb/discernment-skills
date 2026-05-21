# Discernment Skills

A Claude Code [plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces) providing three composable skills for **discernment** — the work of deciding *well* when an AI is happy to hand you a confident answer for everything.

The skills don't make the call for you. They sharpen the question before you prompt, separate confidence from correctness after you get an answer, and keep the decision and the accountability with you.

## The shape

Three single-purpose skills compose by writing into a per-decision file named after the decision.

```
aim          →  writes ## Aim          ┐
cross-check  →  writes ## Cross-check  ├─→  discernment-<slug>.md
own          →  writes ## Own          ┘
```

Each is independently useful — run `aim` on a decision and stop there if that's all you need. They compose because they share one file format.

## The three skills

| Skill | Use when | Writes |
|-------|----------|--------|
| **`aim`** | Starting a decision or framing a question for AI | `## Aim` |
| **`cross-check`** | You have an AI answer you need to pressure-test | `## Cross-check` |
| **`own`** | About to commit to a decision | `## Own` |

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
```

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

They also trigger automatically when your request matches their description (e.g. "help me think through whether to…", "is this answer right?", "I'm going to call it").

## A full pass

1. **Aim** — `aim` walks you through the real decision, your criteria, your signal vs. noise sources, and the question only you would ask. It hands back a sharpened prompt and seeds the decision's `discernment-<slug>.md`.
2. **Cross-check** — paste an AI answer into `cross-check`. It scores the answer against your own criteria and argues the strongest case against it, side by side.
3. **Own** — `own` stops before commitment, surfaces what's on the table, and captures the call, the reasoning in your words, and the watch list that'll tell future-you if you were wrong.

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
│           └── own/SKILL.md
├── README.md
└── LICENSE
```

## License

MIT — see [LICENSE](LICENSE).
