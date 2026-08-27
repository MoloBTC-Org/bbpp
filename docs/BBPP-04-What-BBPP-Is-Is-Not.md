# What BBPP Is / Is Not
## One-Page Clarity Statement — Draft v0.1

**Status**: Draft  
**Date**: 2026-08-16  
**Parent**: BBPP-00-Charter.md

---

### What BBPP Is

- A purpose-driven full-node and mining-oriented software expression of a **physics-locked efficiency model** for UTXO-based Proof-of-Work monetary ledgers.
- The model rests on three reinforcing forces:  
  (1) nodes permanently pay for every byte of non-monetary historical data,  
  (2) miners permanently pay (orphan risk / hashes-per-joule) for heavy blocks,  
  (3) high-performance software amplifies both pressures rather than masking them.
- First concrete release targeted at the **BTC SHA-256** chain with the strongest set of monetary-efficiency defaults we can currently define.
- **Consensus-compatible by construction**. Differentiation occurs only at policy defaults, performance engineering, and operational focus.
- **Unilateral**: any operator may adopt or leave without permission or chain split.
- An open invitation to the efficiency ideal. The underlying physics apply to any compatible network or fully validating implementation (BTC, BCH, future Blake2B or other PoW payment networks).
- An overarching best-practice framework that can recognise, document, and encourage alignment across multiple implementations (including existing clients such as Bit-Block, Knots, and others) while still planning its own explicit client in due course.
- An attempt to practise Best Practice also in how we engage the commons, communicate with stakeholders, and handle information.

### What BBPP Is Not

- A consensus change, soft fork, hard fork, or new coin.
- A claim that other clients, chains, or policy preferences are illegitimate.
- A requirement that users accept every default. Configurability for local hardware and preference is intentional and separate from the principled defaults.
- An ideological purity test. The test is measurable alignment with node cost, miner hashes-per-joule, and software amplification of lean operation.
- A finished product. It is a directed, iterative effort whose first release prioritises the strongest defaults justifiable from the physics.
- A replacement for existing good work. Clients such as Bit-Block (strict anti-spam defaults on a Knots base, full customisability, consensus-compatible) already express key elements of the same purpose and are welcomed as valuable expressions of the efficiency ideal.

---

### Relationship to Current Implementations

Bit-Block (launched 2026-08-16 by Dimitri-H) is the closest currently shipping client to the BBPP “best set of defaults” posture on the policy axis: Knots-derived, `datacarriersize=0` enforced by default, rejection of non-Bitcoin token/asset overlays, full customisability retained, additional practical hardening and IBD options, and explicitly aimed at the legacy (non-hard-fork) chain.  

BBPP treats such implementations as allies and potential reference points. The framework can sit above or alongside them as a shared language of purpose, metrics, and engagement standards while the project continues toward its own explicit client when the time is right.

---

**End of Clarity Statement**
