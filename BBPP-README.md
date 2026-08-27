# Bitcoin Best Practice Protocol — Document Set (Draft)

**Created**: 2026-08-14  
**Updated**: 2026-08-25  
**Location**: `/home/workdir/artifacts/`

This folder contains the draft project documents for a purpose-driven alternative Bitcoin client (and overarching best-practice framework) grounded in the lean-ledger incentive model (node cost of permanent non-UTXO data + miner hashes-per-joule + software performance as amplifier).

## Documents

| File | Description |
|------|-------------|
| **BBPP-00-Charter.md** | Founding charter: purpose, three-force incentive model, Transmutable Physics, refined Non-Goals, success metrics. Root reference. |
| **BBPP-01-Participation-Standards.md** | Guidelines for contributors, reviewers, operators, and miners. |
| **BBPP-02-Best-Practice-Guidelines.md** | Operational and engineering recommendations: default policy posture, performance priorities, template construction, measurement norms. |
| **BBPP-03-Lessons-Learned-Alternative-Clients.md** | Practical lessons from alternative implementations. |
| **BBPP-04-What-BBPP-Is-Is-Not.md** | One-page clarity statement. Positions BBPP as both future explicit client and overarching framework. |
| **BBPP-Background-Client-Landscape.md** | Working reference: Core releases as successive clients + Knots, Bit-Block, **Miner-Oriented / Template-Sovereignty stacks (Knots+DATUM leader, BitcoinPR emerging)**, ProductionReady, Bitcoin Commons, Monetary Node, btcd, utreexod, Floresta, Neutrino, rbitcoin, boundary cases. Includes policy-vs-consensus (SV2) distinction and node markets by primary purpose. |
| **BBPP-README.md** | This index. |

## Current Strategic Picture (2026-08-17)

- **Purpose is locked**: physics-backed monetary efficiency, unilateral, consensus-compatible, transmutable across PoW payment networks.
- **Hard fork is a non-goal** for the primary BBPP line; hard forking is welcomed for others.
- **Node markets clarified**: Proof-of-Work / template-sovereignty nodes (Knots+DATUM leader; BitcoinPR emerging) are the primary fit for the hashes-per-joule efficiency vision. Home validating and enterprise wallet-backend nodes serve different markets and are documented accordingly.
- **Policy vs Consensus**: SV2 alone delivers dynamic policy; DATUM-style designs are required for dynamic consensus signalling by hashrate.
- **Bit-Block** remains the closest shipping expression of strong physics-backed defaults + flexibility on the general policy axis.
- BBPP functions as an overarching best-practice framework that can recognise and encourage aligned implementations while still planning its own explicit client in due course.
- Near-term work remains documentation and clarity; code shipping is further down the line.

## Next Suggested Steps

1. Optional light note in Lessons Learned on BitcoinPR and the miner-oriented taxonomy.
2. Continue monitoring Knots+DATUM, BitcoinPR, Bit-Block, Monetary Node, and related efforts.
3. Only after the purpose and landscape documents are stable, begin concrete default-value tables or modular architecture sketches.

All documents remain drafts. Claims of “best practice” stay tethered to the stated incentive model and to measurable outcomes. Best practice includes choosing the best fit for one’s actual purpose.
