# Bitcoin Best Practice Protocol (BBPP)

**Framework first. Explicit client later. Identical consensus.**

A purpose-driven project for Bitcoin (and other UTXO proof-of-work payment networks) that treats *monetary efficiency* as something you can measure, not a slogan.

License: [BSOL v1.0](LICENSE.md) · [Governance](GOVERNANCE.md) · [Contributing](CONTRIBUTING.md)  
Org: [MoloBTC-Org](https://github.com/MoloBTC-Org)  
Status: documentation repository. `src/` is reserved. No BBPP binary yet.

**GitHub About:** *Framework and future client for monetary-efficient Bitcoin nodes. Identical consensus. Policy and defaults may differ. Documentation first.*  
**Topics:** `bitcoin` · `bitcoin-protocol` · `full-node` · `bitcoin-knots` · `mining` · `proof-of-work` · `documentation` · `open-source` · `self-custody` · `sovereignty`

---

## Three forces (the Charter in one screen)

1. **Node.** Permanent non-UTXO data is a tax on every future validating node.
2. **Miner.** Heavy, slow-propagating templates tax hashes-per-joule (stale work, junk in the block).
3. **Software.** Performance amplifies both pressures. It does not invert them.

Policy, defaults, and operations may differ. Consensus on the primary line does not.

---

## Read in this order

| # | Document | What it settles |
|---|----------|-----------------|
| 1 | [Charter](docs/BBPP-00-Charter.md) | Purpose, Transmutable Physics, Non-Goals, success metrics |
| 2 | [What BBPP is / is not](docs/BBPP-04-What-BBPP-Is-Is-Not.md) | One-page boundary |
| 3 | [Client landscape](docs/BBPP-Background-Client-Landscape.md) | Core-as-successive-clients; Knots, Bit-Block, DATUM, ProductionReady, Monetary Node, Purity, compact-state stacks |
| 4 | [Best-practice guidelines](docs/BBPP-02-Best-Practice-Guidelines.md) | Defaults, templates, measurement, wallet hygiene |
| 5 | [Participation standards](docs/BBPP-01-Participation-Standards.md) | Who may change what |
| 6 | [Lessons learned](docs/BBPP-03-Lessons-Learned-Alternative-Clients.md) | What other implementations already taught |
| 7 | [Roadmap](docs/roadmap.md) | Now / next / later / not-on-roadmap |

Then [CONTRIBUTING.md](CONTRIBUTING.md) if you are opening an issue or PR.

### Research (not Charter)

These files must not rewrite purpose or consensus.

| File | What it is |
|------|------------|
| [Quantum for non-math people](research/quantum-physics-barriers.md) | Locked-box picture, Shor vs Grover, hygiene checklist, BIP-360/361/SHRINCS map. Capacity ≠ security. |
| [Template generation / DMTG](research/template-generation-dmtg.md) | Sovereign vs supplier vs carousel templates. DATUM ≠ SV2 Job Declaration. |
| [research/README.md](research/README.md) | Folder rule: adjacent maps only |

---

## Where this line sits (2026-09-03)

| Axis | Closest shipping expression | Note |
|------|-----------------------------|------|
| Policy defaults + flexibility | **Bit-Block V2** | Knots fork; strong anti-spam defaults; LND backend guides (30 Aug). `txindex=1` is a real disk tax. |
| Template sovereignty | **Knots + DATUM** | Miner-built templates; pool coordinates rewards. BitcoinPR is the integrated experimental Rust neighbour. |
| Conservative third client | **ProductionReady** | Not shipped. OCEAN said DATUM will support it when it does. |
| Hard-fork boundary | BIP-110 / **Bitcoin Purity** / possible Blake2b | Documented. Not this line. |
| Compact state | utreexod, Floresta, Neutrino | Different market (live-state cost). |

OCEAN (30 Aug 2026): remains SHA-256; no PoW change; DATUM talks to Core and any valid node including non-BIP-110 Knots. Efficiency-oriented *new* clients are first-class only if someone actually tests them. That ask is recorded; it is not a guarantee.

---

## Repository layout

```
bbpp/
├── README.md                 ← this file
├── LICENSE.md
├── GOVERNANCE.md
├── CONTRIBUTING.md
├── docs/                     normative
│   ├── BBPP-00-Charter.md
│   ├── BBPP-01-Participation-Standards.md
│   ├── BBPP-02-Best-Practice-Guidelines.md
│   ├── BBPP-03-Lessons-Learned-Alternative-Clients.md
│   ├── BBPP-04-What-BBPP-Is-Is-Not.md
│   ├── BBPP-Background-Client-Landscape.md
│   └── roadmap.md
├── research/                 adjacent, non-normative
│   ├── quantum-physics-barriers.md
│   ├── template-generation-dmtg.md
│   ├── measurements/
│   └── references/
├── scripts/                  empty until we measure
├── src/                      reserved
└── .github/ISSUE_TEMPLATE/
    ├── question.md
    └── landscape-update.md
```

---

## Non-goals

- Changing Bitcoin consensus or launching a ticker on the primary line.
- Selling a block-size hike as “quantum readiness.”
- Maximising arbitrary on-chain data.
- Treating other clients as illegitimate for different *defaults*.

Hard forks are welcomed for anyone who chooses that path. They are not BBPP.

---

## Contribute

1. Read the [Charter](docs/BBPP-00-Charter.md).
2. Open a [landscape-update](.github/ISSUE_TEMPLATE/landscape-update.md) issue for new clients, releases, or measured policy changes.
3. Questions: [question template](.github/ISSUE_TEMPLATE/question.md).
4. Do not send consensus-change PRs here.

Claims of “best practice” stay tethered to the three-force model and to measurable outcomes. Best practice includes choosing the stack that fits the job (home node ≠ miner template node ≠ enterprise backend).
