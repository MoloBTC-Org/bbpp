# Research Note: Dynamic Monetary Template Generation

**Status**: Research — not Charter  
**Date**: 2026-08-29  
**Related**: `docs/02-best-practice-guidelines.md` §4, landscape §3.1c

---

## Definition

A **dynamic monetary template generator (DMTG)** is a process that:

1. Reads the local mempool.
2. Applies a hard monetary-only filter *before* selection (no datacarrier, no inscription envelopes, no token/parasite patterns the operator has marked non-monetary).
3. Packs survivors by effective fee rate under consensus weight and sigops limits.
4. Rebuilds on material mempool change (target: seconds, not minutes).
5. Emits a consensus-valid template for local Stratum/DATUM, a dedicated supplier endpoint, or a carousel.

Success metric: highest sustained fee density of *clean* templates, plus zero non-monetary transactions in the candidate set.

---

## Three deployment modes

| Mode | Who builds the template | Who hashes | Fit |
|------|-------------------------|------------|-----|
| **Sovereign** | Miner’s own node (Knots / Bit-Block / later BBPP) | Same operator | Maximum control. DATUM Gateway is the production pattern. No 1% leak. |
| **Supplier** | Independent node, no hashrate required | External miners | Monetises policy quality. Live example: PyBLOCK Template Suppliers (~1% of block if that template wins). |
| **Carousel / hybrid** | Many suppliers, jobs rotate | Miner chooses one port or rotation | Diversification. Miner can also keep a local DMTG as primary and sample others when fee density justifies it. |

DATUM-style stacks keep **dynamic consensus signalling** with the hashrate owner.  
A carousel of published templates is **dynamic policy sharing**. The pool or carousel operator still sits on the acceptance path unless the miner’s own node is the last validator.

SV2 Job Declaration alone ≠ DATUM. Do not collapse them.

---

## What one template does better than another

Templates differ because mempools, peers, and exact filter edges differ.

- **Fee packed** among monetary txs only.
- **Weight efficiency** (payments vs consolidations vs junk that survived a weak filter).
- **Freshness** (stale template = stale work = hashes-per-joule leak).
- **Policy fidelity** (does the published template actually match the claimed filter set).

A “better” structure is the one that stays clean *and* competitive on fees under a live mempool. Ideology without fee density will not attract hashrate; fee density without a filter reimports the permanent-bulk tax.

---

## Live reference (not an endorsement of pool custody)

PyBLOCK (BIP-110-oriented pool) runs dedicated supplier strata plus a carousel (`stratum+tcp://pool.pyblock.xyz:30000`). Knots required; templates checked spam-free; supplier earns 1% on-chain if a block is found on that template; miner ~98%; pool 1%. Also exposes DATUM and SV2 endpoints. Treat as a working market for clean templates, not as BBPP infrastructure.

---

## Out of scope for this note

- Consensus changes.
- Custodial payout design.
- Claiming carousel rotation equals template sovereignty.

When BBPP ships code, the first generator should be runnable in **sovereign mode** first. Supplier/carousel export is optional.
