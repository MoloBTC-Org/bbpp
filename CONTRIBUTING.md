# Contributing to BBPP

This repository is documentation-first. Code under `src/` is reserved and empty on purpose.

## Before you open a PR

1. Read the [Charter](docs/00-charter.md). If the change does not serve the three-force model, it does not belong here.
2. Read [Participation standards](docs/01-participation-standards.md) — that document is the full bar.
3. Decide the folder:
   - Normative claim (purpose, defaults, non-goals) → `docs/`
   - Map, measurement, or adjacent physics → `research/`
   - Consensus rule change → **do not open a PR here**

## What we accept

- Corrections of fact in the landscape (new client, new release, measured policy change).
- Clarifications that keep consensus identical and policy unilateral.
- Measurement notes with hardware profile and method.
- Drafts that improve communication boundaries (see `research/quantum-physics-barriers.md`).

## What we reject

- Consensus changes, new tickers, hard-fork activation schedules for the primary BBPP line.
- Defaults whose only effect is to make permanent non-monetary data cheaper to store.
- “BIP assigned = Bitcoin upgraded” language.
- Copies of other projects’ source trees.

## How to propose

- Issue first for landscape updates (`landscape-update` template).
- One concern per PR. State the Charter metric you are moving.
- If a default changes, say what an operator sets to opt out.

Questions: use the `question` issue template. Do not treat Grok or any model as a substitute for the documents.
