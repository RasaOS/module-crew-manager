# module-crew-manager

**Version:** 0.1.0 · `rasa.module.crew.manager` · public

The **manager tier** of a galt crew, as a RasaOS module: the manager tier of a galt crew (galt ADR 0053): the conduct of a manager crew, the one session the person talks to, which plans across repos and runs a child lead crew in each; and the extra conduct a child lead reads.

A crew has three tiers, each its own module: [`module-crew-manager`](https://github.com/RasaOS/module-crew-manager) → [`module-crew-lead`](https://github.com/RasaOS/module-crew-lead) → [`module-crew-member`](https://github.com/RasaOS/module-crew-member).

## The cards (`content/crew/manager/`)

| Card | When | Source |
|---|---|---|
| `manager` | the ask spans more than one repo: the manager plans once and runs a child lead crew per repo | galt `router/src/crew/manager.ts` `managerConduct()` at `737a098` |
| `child` | this lead crew is a child of a manager crew; it is read on top of its own lead card | galt `router/src/crew/manager.ts` `childConduct()` at `737a098` |

A card is one markdown file: `key: value` header lines, a blank line, then the conduct (galt ADR 0052 D1, `tags:` from ADR 0054 D2). `{cli}`, `{crew}`, `{level}`, `{approves}`, `{order}` (manager) and `{manager}`, `{cli}`, `{crew}` (child) are filled by galt when the lead reads the card.

## Using it

- **Install into a repo** (the brain layer): the cards land in `.claude/crew/manager/`, where galt finds a repo's own cards.
- **Load into a session:** `.claude-plugin/plugin.json` makes the repo loadable (galt ADR 0064).
- **Source of truth today:** galt's in-code copies (`packages/router/src/crew/`) are what runs. This repo is a snapshot of them until galt reads its cards from here, with its code as the fallback.

## Changing a card

Change it here in a PR. `bin/check-cards` must be GREEN (`RASA_SCHEMA_DIR=~/rAI/rasa-os/schema bin/check-cards`). Bump the version: patch for wording, minor for a new card or header key. Until galt reads from here, mirror the change into galt's copy.
