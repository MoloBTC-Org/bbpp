# Proposed GitHub tree — MoloBTC-Org/bbpp

**Status**: Target layout (docs-first → reserved code)  
**Date**: 2026-08-29  
**Today on GitHub**: `LICENSE.md` + `README.md` + `docs/*.md` (flat dump).  
**Aim**: same documents, public README, research separated, room to grow without a second migration.

```
bbpp/
├── README.md                          # public entry (not the workdir dump)
├── LICENSE.md                         # BSOL v1.0 (already present)
├── CONTRIBUTING.md                    # points at docs/01
├── CODE_OF_CONDUCT.md                 # optional; keep short or skip
│
├── docs/                              # normative project documents
│   ├── 00-charter.md
│   ├── 01-participation-standards.md
│   ├── 02-best-practice-guidelines.md
│   ├── 03-lessons-learned-alternative-clients.md
│   ├── 04-what-bbpp-is-is-not.md
│   ├── background-client-landscape.md
│   └── roadmap.md                     # short living list (new, thin)
│
├── research/                          # adjacent, non-normative
│   ├── README.md                      # “these files do not change the Charter”
│   ├── quantum-physics-barriers.md    # already written
│   ├── template-generation-dmtg.md    # DMTG / PyBLOCK carousel (to land)
│   ├── measurements/                  # size, fee-density, orphan notes
│   │   └── .gitkeep
│   └── references/                    # pointers only, no copies of others’ code
│       └── .gitkeep
│
├── scripts/                           # measurement / analysis helpers later
│   └── .gitkeep
│
├── src/                               # RESERVED — no client code yet
│   └── .gitkeep
│
└── .github/
    ├── ISSUE_TEMPLATE/
    │   ├── question.md
    │   └── landscape-update.md
    └── workflows/
        └── docs-lint.yml              # later: markdown link check
```

## Mapping from current workdir / current GitHub

| Now | Target |
|-----|--------|
| `BBPP-00-Charter.md` | `docs/00-charter.md` |
| `BBPP-01-Participation-Standards.md` | `docs/01-participation-standards.md` |
| `BBPP-02-Best-Practice-Guidelines.md` | `docs/02-best-practice-guidelines.md` |
| `BBPP-03-Lessons-Learned-Alternative-Clients.md` | `docs/03-lessons-learned-alternative-clients.md` |
| `BBPP-04-What-BBPP-Is-Is-Not.md` | `docs/04-what-bbpp-is-is-not.md` |
| `BBPP-Background-Client-Landscape.md` | `docs/background-client-landscape.md` |
| `BBPP-README.md` (internal index + workdir path) | replace with public root `README.md` |
| `research/BBPP-Quantum-Physics-Barriers.md` | `research/quantum-physics-barriers.md` |
| BSOL `LICENSE.md` | keep at root |
| PyBLOCK / DMTG notes (thread only) | `research/template-generation-dmtg.md` |
| Quantum / Purity / Bit-Block V2 updates | already in Landscape; keep there |

Renaming off the `BBPP-` prefix inside `docs/` is optional. Either keep the prefix for grep-familiarity or drop it now while the tree is still small. Do not do both later.

## What each top-level folder is for

- **`docs/`** — claims that bind the project: purpose, participation, defaults, landscape. Change these with review.
- **`research/`** — maps and caveats that must not leak into Charter (quantum BIPs, template markets, measurements).
- **`scripts/`** — fee-density / strip / policy audits when we have them. Empty until then.
- **`src/`** — explicit empty. Signals “client later” without pretending code exists.
- **`.github/`** — issues for landscape updates beat silent README drift.

## What not to add yet

- Multiple client profiles under `src/` (Knots-defaults vs modular flags) — too early.
- Copies of Knots, Bit-Block, Monetary Node, or Purity trees.
- A `whitepaper.pdf` until Charter + Landscape have been stable for a pass.

## Move order (one afternoon)

1. Write public `README.md` (see companion draft in this folder).
2. Add `CONTRIBUTING.md` (10–20 lines pointing at `docs/01`).
3. Add `research/README.md` + `.gitkeep` in `src/`, `scripts/`, `research/measurements/`.
4. Rename/move existing docs into `docs/` if not already there on GitHub.
5. Land `research/template-generation-dmtg.md` from the PyBLOCK / DMTG thread (next content patch, not required for the tree).
6. Thin `docs/roadmap.md`: three bullets only — docs stable, landscape current, code still reserved.

Do not wait for code to create `src/`. The empty directory is the point.
