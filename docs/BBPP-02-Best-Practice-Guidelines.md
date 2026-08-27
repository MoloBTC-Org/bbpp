# Bitcoin Best Practice Protocol
## Operational & Engineering Best-Practice Guidelines — Draft v0.1

**Status**: Draft  
**Date**: 2026-08-14  
**Parent documents**: BBPP-00-Charter.md, BBPP-01-Participation-Standards.md

---

### 1. Purpose of These Guidelines

These guidelines translate the Charter’s incentive model into concrete recommendations for:

- Default policy posture
- Performance engineering priorities
- Mining template construction
- Node operator configuration
- Ongoing measurement

They are living recommendations, not consensus rules.

---

### 2. Default Policy Posture (Recommended)

| Policy Area | BBPP Recommended Default Direction | Rationale |
|-------------|------------------------------------|---------|
| Data-carrier / OP_RETURN / inscription-style payloads | Strict / minimal by default | Permanent non-UTXO data is pure ongoing cost to every future node |
| Mempool acceptance of non-monetary embedding | Refuse by default; configurable | Aligns relay behaviour with long-term node economics |
| Full-RBF | Enabled (or easily enabled) | Supports clean fee-bumping without relying on data-heavy constructions |
| Package relay / TRUC | Supported where it improves lean monetary transaction reliability | Performance and Lightning-style use of monetary outputs |
| Dust / standardness | Conservative, monetary-use oriented | Avoid subsidising uneconomic outputs that bloat the UTXO set |

Operators who disagree must be able to relax these defaults via configuration. The project’s claim is about *defaults*, not about forcing a single policy on the entire network.

---

### 3. Performance Engineering Priorities

Order of preference for engineering effort:

1. **UTXO-set and validation efficiency**  
   Faster script verification, better caching, lower memory amplification for the live monetary state.

2. **Block validation and relay latency**  
   Especially for lean blocks. The goal is to widen the observable gap between clean and heavy blocks.

3. **IBD and initial chainstate construction**  
   Lower time and hardware requirements for a new fully validating node.

4. **I/O and storage layout**  
   Prefer designs that keep the hot monetary state cheap relative to historical bulk.

Explicitly lower priority: optimisations whose primary benefit is making large volumes of permanent non-monetary data cheap to process and store.

---

### 4. Mining & Template Construction Guidelines

- Prefer local policy filters that exclude non-monetary data from templates by default.
- Measure and publish (where practical) the contribution of filtered vs. unfiltered templates to orphan rates and effective hashes per joule.
- Support integration with tools that enable clean template generation (e.g., Datum-style gateways or equivalent).
- Treat template cleanliness as an operational lever of equal importance to hashrate and energy cost.

---

### 5. Node Operator Recommendations

1. Run with the project’s published default policy unless you have a specific, measured reason to deviate.
2. Monitor chainstate size, IBD time (when relevant), and validation latency on your hardware.
3. Prefer configurations that keep the live UTXO set hot and the historical bulk as cold as practical.
4. When evaluating alternative clients or versions, compare them on the Charter’s three metrics: node cost, orphan contribution, and software amplification of lean incentives.

---

### 6. Measurement & Reporting Norms

Meaningful claims should be accompanied by:

- Hardware profile used
- Workload description (lean monetary vs. data-heavy)
- Before/after or differential numbers
- Time period and network conditions (for orphan or propagation observations)

Anecdote is useful for discovery; measurement is required for “best practice” claims.

---

### 7. Evolution of These Guidelines

Changes to recommended defaults or priority order must:

- Reference the Charter’s incentive model
- Provide the expected impact on node cost, miner hashes-per-joule, or both
- Remain consensus-compatible

Rapid oscillation of defaults without new evidence is discouraged.

---

**End of Best-Practice Guidelines Draft**
