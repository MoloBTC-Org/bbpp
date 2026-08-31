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
| [Charter](docs/BBPP-00-Charter.md) | Purpose, three-force model, Transmutable Physics, Non-Goals |
| [What BBPP is / is not](docs/BBPP-04-What-BBPP-Is-Is-Not.md) | One-page boundary |
| [Client landscape](docs/BBPP-Background-Client-Landscape.md) | Core releases as successive clients; Knots, Bit-Block, miner stacks, Monetary Node, Purity, etc. |
| [Best-practice guidelines](docs/BBPP-02-Best-Practice-Guidelines.md) | Defaults, templates, measurement |
| [Participation standards](docs/BBPP-01-Participation-Standards.md) | How to contribute |
| [Lessons learned](docs/BBPP-03-Lessons-Learned-Alternative-Clients.md) | What other implementations taught |
| [Roadmap](docs/roadmap.md) | Now / next / later / not-on-roadmap |

Research (not Charter):

- [Quantum for non-math people](research/quantum-physics-barriers.md) — self-custody hygiene, Shor vs Grover, resource floor, BIP map; not Charter
- [Template generation / DMTG](research/template-generation-dmtg.md) — sovereign vs supplier vs carousel

---

## Status (2026-08-31)

- Purpose is locked. Hard fork is a **non-goal** for the primary line; hard-forking is welcomed for anyone who chooses that path.
- Shipping closest allies on the *policy* axis: **Bit-Block V2** (strong defaults + flexibility; LND backend guides 30 Aug). On the *template-sovereignty* axis: **Knots + DATUM**.
- OCEAN (30 Aug) remains SHA-256; DATUM stays client-facing (Core, non-BIP110 Knots, ProductionReady when shipped). Efficiency-oriented new clients still need an explicit test path.
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

See [docs/roadmap.md](docs/roadmap.md).

---

## Non-goals (short)

- Changing Bitcoin consensus or launching a ticker.
- Maximising arbitrary on-chain data.
- Claiming other clients are illegitimate for different defaults.

Boundary cases (BIP-110 / Purity / BCH / possible Blake2b) are documented in the landscape. They are not this line.

---

## Contribute

Read [Participation standards](docs/BBPP-01-Participation-Standards.md) and [CONTRIBUTING.md](CONTRIBUTING.md).  
Open an issue for landscape updates (new client, new release, measured policy change).  
Do not send consensus-change PRs to this repo.
