# Bitcoin Best Practice Protocol (BBPP)
## Founding Charter — Draft v0.1

**Status**: Draft for discussion  
**Date**: 2026-08-14  
**Purpose**: Define the directing vision, incentive model, and non-negotiable principles for a purpose-driven Bitcoin full-node and mining-oriented client.

---

### 1. Purpose

Bitcoin Best Practice Protocol exists to implement and operate software that keeps Bitcoin’s permanent dataset focused on **mobile monetary claims** (the live UTXO set and the history required to validate them).

The client is optimised for the long-term economic and physical realities of a permissionless Proof-of-Work monetary ledger:

- Full nodes pay a continuous tax on every byte of permanent non-monetary data.
- Miners pay an orphan / hashes-per-joule tax on heavy, slow-propagating blocks.
- High-performance software engineering amplifies both pressures; it does not invert them.

BBPP therefore prioritises:

1. Minimal permanent non-UTXO data by default policy.
2. Lean, fast-propagating block templates.
3. Validation and relay performance that makes the cost of bloat visible and the advantage of leanness measurable.

Consensus rules remain identical to Bitcoin. Differentiation occurs at the policy, performance, and operational layers.

---

### 2. Core Incentive Model (Non-Negotiable)

| Actor | Primary Cost / Risk | Rational Preference | How BBPP Serves It |
|-------|---------------------|---------------------|--------------------|
| Node operator | Permanent storage + validation burden | Minimise non-UTXO historical data | Strict default filters; efficient UTXO handling; lower hardware floor |
| Miner | Stale shares, propagation delay | Lean, filtered templates | First-class clean template support; fast relay; measurable orphan reduction |
| Software | CPU, memory, I/O, latency | Efficient handling of live monetary state | Performance targets treated as first-class deliverables |

These three forces reinforce one another. BBPP treats alignment with them as the definition of best practice.

---

### 3. Design Principles

1. **Monetary-first permanent state**  
   The live UTXO set and the minimal history required to validate it are the only data categories that justify the full cost of a public PoW ledger. One-time data is treated as expensive by default.

2. **Unilateral policy, identical consensus**  
   BBPP never changes consensus rules. All differentiation is local policy, configuration defaults, and engineering priority. Operators may adopt or abandon it without permission or chain split.

3. **Performance as amplifier, not subsidiser**  
   Engineering effort is directed toward making lean operation cheaper and heavy operation more visibly costly. Optimisations that primarily make large data-heavy blocks “acceptable” are out of scope.

4. **Measurable claims**  
   Default policy choices and performance improvements must be accompanied by concrete metrics (chainstate size impact, IBD time, validation latency, estimated orphan contribution, etc.).

5. **Transparency over authority**  
   “Best practice” is a claim that must be continually demonstrated against the incentive model, not an assertion of exclusive correctness.

6. **Transmutable physics**  
   The three-force model is derived from the physical and economic regularities of any UTXO-based Proof-of-Work monetary ledger. It therefore applies, in principle, to Bitcoin (SHA-256), Bitcoin Cash, any future Blake2B or other PoW payment network, and any fully validating implementation thereof. BBPP software is one concrete expression of that model (beginning on the BTC SHA-256 chain). Any operator or implementation is free to move toward the same efficiency ideal under their chosen consensus rules. BBPP claims no exclusivity over the principles—only responsibility for the defaults and software it ships.

---

### 4. Non-Goals

- Changing Bitcoin’s (or any other chain’s) consensus rules, creating a new coin, or initiating a hard fork as part of the primary BBPP line.
- Hard forking is nevertheless welcomed and respected for any group that concludes such a path best serves their principles. The Declaration of Bitcoin Independence / BIP-110 trajectory and the historical Bitcoin Cash split are recognised as legitimate boundary cases.
- Maximising arbitrary data throughput or “innovation” that permanently inflates historical bulk.
- Competing on feature velocity for non-monetary use cases.
- Centralised control of policy or development process.
- Claiming that other implementations or chains are illegitimate for declining the same defaults.

---

### 5. Success Metrics (Long-Horizon)

- Ordinary operators can sustain fully validating nodes at measurably lower resource cost than the network average for equivalent validation.
- Operators using lean/clean templates show measurable reduction in effective orphan risk or improvement in hashes-per-joule contribution.
- Published differentials exist between the cost of the live monetary state and the cost of historical bulk under BBPP defaults.
- The first release ships the strongest set of physics-backed defaults we can currently define; subsequent releases improve measurement, performance, and configurability without diluting those defaults.
- Adoption occurs because operators and miners observe economic alignment, not because of social or political pressure.
- Best Practice also extends to how the project engages the commons, communicates with stakeholders, and handles information across the spectrum.

Node-specific variables (mempool size, exact OP_RETURN / datacarrier limits, filter aggressiveness, etc.) remain user-configurable so operators can optimise for local hardware and risk tolerance. These are the flexibility layer; they are distinct from the principled defaults.

---

### 6. Relationship to Other Clients and the Broader Field

BBPP sits in the same broad category as Bitcoin Knots, Bit-Block, ProductionReady’s intended conservative client, Monetary Node, and related efforts: software that prioritises monetary leanness and node accessibility while remaining consensus-compatible.

It differs by making the node–miner incentive dual and the role of performance engineering explicit founding principles, and by offering itself as an overarching best-practice framework that can recognise, document, and encourage alignment across multiple implementations.

Consensus compatibility with Bitcoin Core and all other fully validating implementations is mandatory. Implementation expression of the physics model (on BTC, BCH, or elsewhere) is welcomed.

---

**End of Charter Draft**  
This document is the root reference. All subsequent guidelines, participation standards, and technical decisions are subordinate to the incentive model and principles stated here.
