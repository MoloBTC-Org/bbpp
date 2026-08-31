# Background Reference: Bitcoin Client Landscape
## Treating Major Core Releases as Competing Clients + Alternative Implementations

**Status**: Working reference document  
**Date**: 2026-08-14 (updated 2026-08-30)  
**Purpose**: Provide a structured view of the open field for protocol development and alternative-client evaluation. Major Bitcoin Core releases are listed as successive “clients” with distinct consensus-readiness and policy postures. Independent and derivative clients (including the Monetary Node proposal) are included for comparative study.

This document supports the Bitcoin Best Practice Protocol (BBPP) charter work. It is descriptive, not normative.

---

## 1. Conceptual Frame

- **Consensus** = rules that determine block and transaction validity. Divergence risks chain splits.
- **Policy** = what a node will relay, accept into its mempool, or prefer when building templates. Fully local.
- Each major Core release can be read as a product with its own default policy personality and soft-fork readiness.
- Alternative clients compete primarily on policy defaults, performance characteristics, filtering philosophy, and governance process while remaining consensus-compatible.

### 1.1 Policy vs Consensus at the Miner Signalling Level (SV2 context)

A practical distinction relevant to template sovereignty:

- **Dynamic policy** (what SV2 Job Declaration alone primarily delivers): the miner can select transactions, prioritise fees, and apply non-standard filters under a *shared* consensus ruleset. The pool’s node still validates and can reject the template. Soft-fork signalling bits remain gated by the pool’s chosen node implementation.
- **Dynamic consensus** (what DATUM-style designs enable): the miner’s own node builds and broadcasts the template. The pool coordinates rewards only. Hashrate can therefore point at different consensus implementations or signalling preferences without a single-node acceptance chokepoint.

SV2 alone decentralises policy under a common ruleset; genuine ability for hashrate to “vote” with competing consensus views requires removing the pool-node validation gate (DATUM, P2Pool-style, or equivalent). This is why the highest-ranked efficiency stack pairs Knots (policy) with DATUM (template sovereignty).

### 1.2 Node Markets by Primary Purpose

Different implementations optimise for different operators. Best practice includes choosing the best fit:

| Primary Market | Core Need | Leading Examples | Efficiency Angle |
|----------------|-----------|------------------|------------------|
| **Proof-of-Work / Template Sovereignty** | Clean, low-stale, miner-controlled templates; maximise fraction of hashes that are non-stale and fully credited | Knots + DATUM (leader); BitcoinPR (emerging integrated); Braiins co-located small-scale; Core + solo / SV2 JD | Directly multiplies firmware J/TH gains by reducing stale and spam taxes |
| **Home / Ordinary Validating** | Low resource cost, spam resistance, unilateral sovereignty for wallet users | Knots, Bit-Block, Core (pruned), Monetary Node proposals | Permanent-bulk minimisation lowers hardware floor |
| **Enterprise / Wallet Backend** | High-availability Electrum/Esplora serving, reduced multi-process overhead | rbitcoin (archive model, in-process indexes); Core + Fulcrum | Operational cost of serving, not primarily permanent-bulk or template quality |
| **Compact-state / Light** | Dramatically lower UTXO or validation footprint while remaining validating or near-validating | utreexod, Floresta, Neutrino (filters) | Attacks live-state cost; complementary to policy approaches |

BBPP’s physics-locked efficiency vision prioritises the **Proof-of-Work / Template Sovereignty** row (hashes-per-joule via clean templates + low stale) while the same model benefits home validating nodes through reduced permanent non-monetary bulk. Enterprise wallet-backend optimisations are legitimate adjacent work but are not the primary focus.

---

## 2. Bitcoin Core Releases as Successive “Clients”

| Era / Release | Approx. Period | Key Consensus Posture | Notable Default Policy Character | Character Summary |
|---------------|----------------|-----------------------|----------------------------------|-------------------|
| **0.9.x** | 2014 | Pre- and early-P2SH era rules | OP_RETURN first standardised at **40 bytes** | First modern policy era; intentional data-carrier standardness introduced |
| **0.11 – 0.12** | 2015–2016 | BIP66, CLTV; CSV preparation | OP_RETURN raised to **80 then 83 bytes**; opt-in RBF (BIP125) introduced | More expressive scripts + first replace-by-fee tooling; still conservative on data size |
| **0.13.0 / 0.13.1** | 2016 | SegWit validation code + activation parameters | Continuity with prior policy; focus on soft-fork readiness | The “SegWit-ready” client. 0.13.1 carries activation signalling |
| **0.14 – 0.16** | 2017–2018 | Full SegWit enforcement (post-activation) | Continued ~83-byte datacarrier; fee estimation & ancestor limits mature | Post-SegWit stabilisation era |
| **0.17 – 0.21** | 2018–2021 | Taproot code + activation parameters (0.21) | Still classic ~83-byte datacarrier default; opt-in RBF | “Taproot-ready” client series |
| **22.0 – 27.x** | 2021–2024 | Full Taproot enforcement | Relative policy stability on data limits; package-relay groundwork | Mature Taproot era; versioning drops leading zero |
| **28.0** | Oct 2024 | No new consensus rules | **Full-RBF enabled by default**; early 1p1c package relay & TRUC support | Major policy shift: replacement philosophy changes |
| **29.x – 30.0** | 2025 | No new consensus rules | **OP_RETURN / datacarriersize default dramatically raised** (~100 kB / effectively permissive); multi-OP_RETURN under aggregate limit | The “permissive data” client. Strongest recent divergence point vs. stricter derivatives |
| **31.x** | 2026 | No new consensus rules (as of latest) | Inherits 30.x data posture + further package/fee refinements | Incremental evolution of the post-30 defaults |

**Notes**  
- After a soft fork activates, later releases remain consensus-compatible with earlier post-activation releases.  
- The meaningful differences for operators are almost entirely in default policy and performance characteristics.  
- Exact byte limits and option names should be verified against the specific release notes.

---

## 3. Derivative and Independent Clients / Proposals

### 3.1 Bitcoin Knots
- **Base**: Bitcoin Core derivative.
- **Differentiation**: Stricter / more configurable policy defaults (historically tighter OP_RETURN / datacarrier stance, additional filtering options). Significant real-world node share.
- **Relevance**: Closest large-scale example of a policy-first alternative that remains consensus-compatible. Directly relevant to any lean-ledger client discussion.

### 3.1b Bit-Block (Dimitri-H / @Dimi_h) — launched 2026-08-16; V2 2026-08-23
- **Base**: Official fork of Bitcoin Knots (v28/v29 lineage).
- **Differentiation**: Strict anti-spam defaults by design (`datacarriersize=0` enforced, rejection of non-Bitcoin tokens and asset overlay protocols); fee subtraction from amounts enabled by default; full customisability retained (as flexible as Knots); enhanced input sanitization; optional faster IBD via Libbitcoin-style trusted checkpoint; SeedSigner-style high-entropy dice-roll wallet generation; rebranded GUI.
- **V2 (23 August 2026)**: Diffuses the inherited Knots “timebomb” (hard ~2-year expiry that bricks the node) into a one-time friendly upgrade reminder — the node continues validating; no forced shutdown. Lighter, less aggressive chainstate/LevelDB maintenance (fewer unnecessary rewrites). Cleaner version/copyright display. Builds for macOS, Windows, and Linux.
- **Companion project**: Knots Legacy — fork of the latest non-RDTS Knots version maintained for operators remaining on the original (non-PoW-transition) Bitcoin chain.
- **Lightning backend (2026-08-30)**: Published LND-on-Bit-Block guides for Windows, macOS, and Linux (plain .txt at bit-block.org/bit-block-bitcoin-development/; full text also posted by @Dimi_h). Stated purpose: Bit-Block remains the anti-spam L1 client; Lightning is “Bitcoin used as money.” Backend requirements called out honestly: `server=1`, `txindex=1`, ZMQ rawblock/rawtx; cookie RPC by default; LND uses its own aezeed seed, separate from the Bit-Block wallet. Windows has no `-daemon` (NSSM or leave the window open).
- **Status**: V2 publicly available via bit-block.org and GitHub (DimiH2025/Bit-Block); solo spare-time development. LN guides are documentation only — LND is still Lightning Labs software.
- **Relevance to BBPP**: Currently the closest shipping expression of the “strongest physics-backed defaults + retained user flexibility” posture on the policy axis while remaining fully consensus-compatible and unilateral. The V2 timebomb diffusion is a clear win for unilateral user choice. Explicitly aimed at the legacy chain. The LN guides treat L2 payments as the monetary use-case sitting *on* a lean L1 node — aligned with BBPP — but `txindex=1` is a real disk/reindex tax. Do not pretend a Lightning backend is free under the three-force model. Valuable reference implementation and natural ally for an overarching BBPP framework.

### 3.1c Miner-Oriented / Template-Sovereignty Implementations

These are the nodes and gateways deliberately built so that the operator controlling the hashrate constructs (or tightly controls) block templates rather than accepting opaque pool work. This is the layer that most directly multiplies firmware-level hashes-per-joule gains by reducing stale shares and spam taxes.

| Stack | Maturity | Template Control | Protocols | Best Scale | Notes |
|-------|----------|------------------|-----------|------------|-------|
| **Bitcoin Knots + DATUM Gateway (Ocean)** | Production / mature | Highest policy granularity (anti-spam, size limits, selection) | Stratum V1 to ASICs + DATUM to pool; GBT from node | Solo/small to medium; growing industrial interest | **Current leader**. Miner builds template; pool only coordinates rewards. 50% fee discount on Ocean. Direct analogue of firmware “sweet-spot” tuning at the template layer. |
| **BitcoinPR** (BitcoinP(ure)R(ust)) | Experimental / early | Strong (own mempool + tip; Datum client; Knots-style filters; configurable coinbase) | Native Stratum V1 + SV2 Template Distribution + Datum client | Solo / small-to-medium (experimental limits large fleets) | Pure-Rust lean validator with *built-in* mining gateway. Removes extra process hop. Interop-tested against Core, Knots, btcd, libbitcoin. Source: github.com/BitcoinPR/BitcoinPR. |
| **Bitcoin Core + self-hosted solo** (Public Pool, ckpool, Hydrapool, etc.) or SV2 Job Declaration | Core = reference; solo software varies | Good (standard GBT; policy less granular than Knots by default) | Stratum V1 (solo); SV2 JD where supported | Solo/small excellent; medium/large via robust solo or SV2 pools | Reliable baseline. SV2 alone still routes through a pool node for acceptance (dynamic policy, not full dynamic consensus). |
| **Braiins Mini Miner + co-located pruned node + Braiins OS / SV2** | Hardware + firmware production; node co-location emerging | Standard Core (or Knots) templates; SV2 native in firmware | Native SV2 in Braiins OS | Solo / very small (single device or tiny fleet) | Tightest small-form-factor co-location of validation + hashing. Bandwidth and latency benefits of local work. |
| Emerging (Braidpool, pure P2P share-chains, other SV2 stacks) | Early / research | High potential by design | Custom / SV2-oriented | Currently small | Aim to eliminate central template authority entirely. |

**Key efficiency alignment**: Firmware (LuxOS, Braiins OS, etc.) optimises watts → hashes. The sovereign node layer optimises the *usefulness* of those hashes (low stale, clean monetary templates, continuous high-quality work). The two multiply. PoW-focused nodes remain underrepresented relative to general and wallet-backend implementations; Knots+DATUM is the clear production leader and BitcoinPR is the most integrated experimental alternative.

### 3.2 ProductionReady (org + intended client)
- **Type**: 501(c)(3) nonprofit (Jimmy Song, Samson Mow, Parker Lewis, John Ratcliff et al.) funding a conservative third client.
- **Stated goals**: Preserve monetary properties; reduce Core monopoly; stability over feature expansion; build on Core rather than clean-room rewrite.
- **Status** (mid-2026): Funding / education organisation + design principles; client still early.
- **Relevance**: Explicitly monetary-conservative and anti-monopoly. Philosophical neighbour to BBPP. OCEAN (2026-08-30) stated DATUM will support ProductionReady when it ships.

### 3.3 Bitcoin Commons / BLVM (@BtcCommons / BTCDecoded)
- **Type**: Formal mathematical specification (Orange Paper) + Rust-based alternative full-node stack + forkable governance framework.
- **Claims**: Differential testing against Core with claimed zero consensus divergence across large mainnet history; emphasis on human-readable consensus rules and “coordination without authority.”
- **Status**: Active development; governance not fully activated.
- **Relevance**: Strongest current effort at independent implementation + formal spec. Complements rather than directly competes on policy defaults.

### 3.4 Monetary Node (@MarketAnarchy21 / monetarynode.org)
- **Type**: Proposed class of full node (intended primarily as Bitcoin Knots patchset; Core port invited). BIP draft stage (2026).
- **Core design**:
  - Fully validates every consensus rule and block exactly like a standard node.
  - After validation, **deletes non-monetary data** (inscriptions/Ordinals, stamps, certain OP_RETURN patterns, etc.) from the working UTXO set / chainstate.
  - Refuses to relay such data in the mempool.
  - Retains complete monetary/payment history, all block hashes, proof-of-work, and the ability to spend any valid output (spam outputs remain spendable via reconstruction if needed).
  - Maintains dual cryptographic state fingerprints (full legacy state + cleaned monetary state) bound to block hashes.
  - Aims for substantially smaller chainstate (~half the UTXO entries in published estimates), lower hardware requirements, and spam-free IBD between Monetary Nodes.
- **Key claims**: “The spam is deleted; the hashes are saved.” No fork, no consensus change, no confiscation, unilateral adoption.
- **Status** (August 2026): Draft BIP + measurement/strip scripts published (github.com/sambitcoin/BitcoinMonetaryNode). Demonstration (18 August 2026): stripped non-monetary carriers from 194,863 blocks (767,430–962,292); rebuilt every merkle root from retained txids and checked against headers — **0 failures**; ~33.5–37 GB of inscription/witness payload removed in the measured range. Reference Knots patchset not yet started. Not yet posted to bitcoin-dev.
- **Relevance to BBPP / lean-ledger discussion**: Directly operationalises the “minimise permanent non-UTXO data” incentive. Goes further than pure relay policy by actively pruning non-monetary data from the working chainstate after validation. The strip demonstration is the strongest current empirical evidence that merkle-verifiable spam removal is possible without changing block hashes. Worth close technical study. Edge cases around monetary-to-monetary IBD, dual-state verification, and long-term network effects remain active questions.

### 3.4b Bitcoin Purity (@HongShuning / saltduck/bitcoinpurity) — hard-fork boundary case
- **Base**: Fork of Bitcoin Knots `v29.4.knots20260508` on the BIP-110 *enforcement* minority lineage (not the Core majority chain).
- **Short-term consensus package** (documented as the active hard-fork rules):
  1. BIP110/RDTS rules made **permanently** active (no expiry).
  2. SHA256d retained; difficulty switched to 24-hour ASERT, anchored near BIP-110 enforcement height.
  3. Deep-reorg parking (local chain-selection policy, not consensus) to resist 51% attacks.
  4. No transaction-level replay protection — intentional claim that this *is* Bitcoin rather than “another coin.”
- **Post-adoption roadmap** (not yet specified as active rules): automatic double-spend freeze; SEAL-2 block header; remove Taproot and possibly SegWit; post-quantum signatures **and 32 MB block size**.
- **Status**: Early (initial commits / mainnet activation claimed at height 961637 per project docs). Distinct from the planned BLAKE2b PoW-change path discussed by other BIP-110 constituency members.
- **Relevance to BBPP**: Canonical **hard-fork boundary case**. The first four items stay inside a coherent monetary / anti-spam exit path and are welcomed as such under the Charter (hard fork is a non-goal for the *primary* BBPP line; hard-forking is welcomed for those who choose it). The later 32 MB / script-removal / post-quantum package diverges from the scarcity and permanent-bulk economics that BBPP treats as fundamental. Document accurately; do not treat as an aligned consensus-compatible client.

### 3.5 btcd (Go)
- **Type**: Independent full-node implementation written in Go.
- **Status**: Mature, actively maintained; parts of its libraries are widely reused (notably by LND).
- **Relevance**: Longest-running independent full implementation still in active use. Serves as the base for utreexod. Useful reference for cross-implementation testing and for understanding the ongoing cost of maintaining consensus parity outside Core.

### 3.6 utreexod (Calvin Kim / Utreexo)
- **Type**: btcd fork that implements Utreexo (hash-based accumulator for the UTXO set). Lead: Calvin Kim (@kcalvinalvinn). Related BIPs 181/182/183 (draft).
- **Core idea**: Represent the UTXO set as a forest of Merkle trees so that compact-state nodes can fully validate without storing the entire UTXO set. Bridge nodes attach proofs; compact nodes verify with tiny state (~hundreds of bytes for the accumulator roots in ideal cases).
- **Status** (mid-2026): Working mainnet-capable software; public test versions and ongoing P2P optimisation. OpenSats LTS support for continued work.
- **Relevance to BBPP**: Directly attacks the permanent cost of the live monetary state itself (the UTXO set), complementary to efforts that target non-monetary historical bulk. Demonstrates that radical reductions in node resource requirements are possible while remaining fully validating.

### 3.7 Floresta (Davidson Souza / Vinteum)
- **Type**: Rust compact-state Utreexo node. Uses libbitcoinkernel (Bitcoin Core’s validation engine) for consensus compatibility; combines pruning + Utreexo.
- **Notable results**: Demonstrated on very low-resource hardware (Raspberry Pi Zero class, Android via Mandacaru). Can run as standalone node or embeddable library; includes Electrum server capability in some configurations.
- **Relevance**: Practical proof that full validation + dramatically lower resource floor is achievable. Architecture choice (kernel wrapper) reduces consensus-divergence risk relative to clean-room reimplementations.

### 3.8 Neutrino (BIP 157/158 compact block filters)
- **Type**: Privacy-preserving light-client protocol (and reference implementations). Clients download headers + deterministic compact filters; match locally; fetch only relevant blocks. Does **not** perform full consensus validation.
- **Origin**: Lightning Labs (roasbeef et al.); widely used as LND backend and in mobile wallets.
- **Relevance**: Important point on the security/resource spectrum. Neutrino improves privacy over classic BIP-37 SPV and lowers the barrier for non-validating clients, but it is not a substitute for fully validating nodes. Any “alternative client” discussion must keep the validation vs. light-client distinction clear. Calvin Kim’s broader work on alternative implementations often sits alongside Neutrino in the same ecosystem conversations (e.g. bitcoin++ talks on the realities of building outside Core).

### 3.9 Other Historical / Independent Implementations
- **libbitcoin**: Toolkit and node components; historically significant independent codebase, known for performance orientation.
- Earlier alternative clients and experimental implementations exist but currently have limited production share.

**Source note (2026-08-14)**: Calvin Kim’s talk “Realities of an alternative bitcoin implementation” (bitcoin++, https://youtu.be/MAG7zbsag1A) and related public material on btcd / utreexod / Floresta inform the entries above. Further detail is expected from the linked resources referenced in that presentation.

---

## 4. Comparative Lens for BBPP Evaluation

When assessing any client (including future BBPP releases) against the lean-ledger incentive model:

| Question | Why it matters |
|----------|----------------|
| Does it change consensus rules? | Must be “no” for Bitcoin compatibility. |
| What are the **default** policy settings on permanent non-monetary data? | Direct expression of node-cost philosophy. |
| Does it actively reduce working chainstate size after validation? | Monetary Node’s distinctive approach; others rely on relay policy + operator pruning. |
| How does it treat mining template construction? | Miner hashes-per-joule side of the incentive dual. |
| What performance claims are made, and are they measured on lean vs. heavy workloads? | Software-as-amplifier test. |
| Is adoption unilateral? | Required for no-permission ethos. |

---

## 5. Working Notes

- Core 28.0 (Full-RBF default) and Core 30.0 (large datacarrier default) are the two clearest recent policy inflection points inside the reference implementation.
- Knots remains the primary large-scale policy alternative currently deployed.
- **Bit-Block V2 (2026-08-23)** remains the closest shipping client to the BBPP “strongest defaults + retained flexibility” posture on the policy axis. V2 diffuses the Knots timebomb into a warning and lightens chainstate maintenance. Natural ally for the overarching BBPP framework.
- **Bit-Block + LND (2026-08-30)**: Official home-node Lightning guides (Win/macOS/Linux). Positions LN as the monetary L2 on an anti-spam L1. Record the `txindex=1` cost; LND seed ≠ node wallet seed. Complementary to OCEAN’s Lightning-*payout* work — different layer (home channels vs pool settlement).
- **Miner-oriented / template-sovereignty stack**: Knots + DATUM Gateway remains the production leader. BitcoinPR is the strongest integrated experimental pure-Rust alternative with native mining gateway + Datum client. Shared template markets (PyBLOCK suppliers + carousel) are in `research/template-generation-dmtg.md` — complementary to DATUM, not a substitute for miner-owned consensus signalling.
- **OCEAN / DATUM, 2026-08-30**: Luke Dashjr separated from OCEAN (resigned Chairman, CTO, director). Pool statement: remains on SHA-256; no PoW change; DATUM stays the product; pool-side open source promised early next year; Lightning payouts / SV2 cooperation continue. Mark Artymko: DATUM already talks to Core and any valid node including non-BIP110 Knots; ProductionReady to be supported when it ships. Knots-on-legacy-chain maintenance is the open risk he named, not DATUM’s client interface.
- **moloBTC question on that thread** (the right BBPP question): as efficiency-oriented alternative clients appear, will the gateway make a best effort to keep them first-class rather than treating “Core + later ProductionReady” as the only supported pair? Protocol-oriented efficiency is client-agnostic only if the pool actually tests new nodes. Record the ask; do not treat the reply as a guarantee for unshipped clients.
- SV2 Job Declaration alone delivers dynamic *policy*; DATUM-style designs are required for dynamic *consensus* signalling by hashrate.
- Monetary Node published a strip demonstration (194,863 blocks, 0 merkle failures, tens of GB removed). Still draft; Knots patchset not started. Strongest current empirical work on post-validation bulk reduction.
- **Bitcoin Purity** is the documented SHA256d hard-fork continuation of permanent RDTS on the BIP-110 minority lineage. Short-term package (permanent RDTS + ASERT + reorg parking + no replay protection) is a coherent exit path. Later 32 MB / script-change roadmap diverges from BBPP scarcity economics.
- The BIP-110 / Declaration of Bitcoin Independence / Purity / possible BLAKE2b-PoW trajectories remain the primary hard-fork boundary cases. BBPP documents them; it does not follow them.
- **Quantum / post-quantum** is adjacent research, not a client in this landscape. See `research/quantum-physics-barriers.md` (BIP-360 P2MR, BIP-361 sunset draft, SHRINCS, Hourglass). No PQ output is consensus. Do not treat BIP assignment as activation.
- utreexod + Floresta attack live-state cost; rbitcoin optimises the enterprise/wallet-backend market.

This landscape is expected to evolve. Update this reference as new major releases ship, new clients gain measurable share, or proposals move from draft to production binaries.

---

**End of Background Reference**  
File location: `/home/workdir/artifacts/BBPP-Background-Client-Landscape.md`
