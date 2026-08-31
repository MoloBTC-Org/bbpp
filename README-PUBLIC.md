# Bitcoin Best Practice Protocol (BBPP)

**Framework first. Explicit client later. Identical consensus.**

BBPP is a purpose-driven project for Bitcoin (and compatible UTXO PoW networks) that treats monetary efficiency as a measurable engineering goal:

1. Permanent non-UTXO data is a tax on every validating node.
2. Heavy, slow-propagating templates tax miner hashes-per-joule.
3. Software performance amplifies both pressures; it does not invert them.

Differentiation is policy, defaults, and operations — not a new coin.

License: [Bitcoin Sovereign Open Source License (BSOL) v1.0](LICENSE.md)

---

## Start here

| Document | Role |
|----------|------|
| [Charter](docs/00-charter.md) | Purpose, three-force model, Transmutable Physics, Non-Goals |
| [What BBPP is / is not](docs/04-what-bbpp-is-is-not.md) | One-page boundary |
| [Client landscape](docs/background-client-landscape.md) | Core releases as successive clients; Knots, Bit-Block, miner stacks, Monetary Node, Purity, etc. |
| [Best-practice guidelines](docs/02-best-practice-guidelines.md) | Defaults, templates, measurement |
| [Participation standards](docs/01-participation-standards.md) | How to contribute |
| [Lessons learned](docs/03-lessons-learned-alternative-clients.md) | What other implementations taught |

Research (not Charter):

- [Quantum for non-math people](research/quantum-physics-barriers.md) — self-custody hygiene, Shor vs Grover, resource floor, BIP map; not Charter
- [Template generation / DMTG](research/template-generation-dmtg.md) — sovereign vs supplier vs carousel

---

## Status (2026-08-29)

- Purpose is locked. Hard fork is a **non-goal** for the primary line; hard-forking is welcomed for anyone who chooses that path.
- Shipping closest allies on the *policy* axis: **Bit-Block V2** (strong defaults + flexibility). On the *template-sovereignty* axis: **Knots + DATUM**.
- This repository is documentation. `src/` is reserved. No BBPP binary yet.
- Quantum / PQ signature work stays under `research/`. BIP assigned ≠ activated.

---

## Repo layout

```
docs/        normative project documents
research/    adjacent maps (quantum, template markets) — do not change the Charter
scripts/     measurement helpers (empty)
src/         reserved for a future client
```

Full tree: see `REPO-TREE.md` in the working set, or the `docs/roadmap.md` once published.

---

## Non-goals (short)

- Changing Bitcoin consensus or launching a ticker.
- Maximising arbitrary on-chain data.
- Claiming other clients are illegitimate for different defaults.

Boundary cases (BIP-110 / Purity / BCH / possible Blake2b) are documented in the landscape. They are not this line.

---

## Contribute

Read [Participation standards](docs/01-participation-standards.md).  
Open an issue for landscape updates (new client, new release, measured policy change).  
Do not send consensus-change PRs to this repo.
