# Which Node For Which Job
## One-page card. Pulled from Landscape §1.2 and pinned to BBPP defaults.

**Status**: Draft  
**Date**: 2026-09-06  
**Parent**: BBPP-Background-Client-Landscape.md, BBPP-06-Default-Value-Table.md  
**Rule**: pick the job first. Then pick the binary. Then apply only the knobs that job needs.

BBPP defaults are built for rows 1 and 2. Rows 3 and 4 are legitimate Bitcoin jobs. They are not the BBPP shipping target.

---

## The card

| Job | What must be true | Binary starting point (2026) | BBPP defaults? | Turn on | Leave off |
|-----|-------------------|------------------------------|----------------|---------|-----------|
| **1. Home / ordinary validating** | You check your own money. Disk and RAM stay boring. Unilateral. | **Bit-Block V3**, or Knots + the default-value table | **Yes — default customer** | prune; §2 filters; full-RBF | txindex; explorer indexes; unfiltered carrier |
| **2. Template miner / PoW sovereignty** | The job that hits silicon is *your* filtered template. Stale work is the enemy. | **Bit-Block V3 or Knots + DATUM** (V3 has a setup switch) | **Yes — second default customer** | every §2 filter on GBT/DATUM; local template log | unfiltered pool carousel; raising block weight “for fill” |
| **3. Enterprise / wallet backend** | Electrum/Esplora/LND uptime. Serving cost dominates. | Same L1 + the serving stack the wallet speaks | **Partial** | what the backend documents (`server`, ZMQ, often `txindex`) | calling an indexer “lean home” |
| **4. Archival / compact-state / stripped store** | Keep everything, or shrink history after validation | Core archive; utreexod / Floresta; **Monetary Node store** (research) | **No as a shipping default** | prune=0 *or* compact/stripped store — never both by accident | mixing archive disk with “lean home” claims |

Lightning sits on **1 + 3**, not on a fifth row. LND-on-Bit-Block needs `server=1`, `txindex=1`, ZMQ. That is an enterprise-shaped tax on a home machine. Say so in the profile.

---

## Decision tests

**Job 1 if:** a pruned node plus a hardware wallet would let you sleep. You do not owe the network an inscription CDN.

**Job 2 if:** a fat template costs you stale shares you can measure. Policy only on relay but not on the job is theatre.

**Job 3 if:** someone else’s wallet software restarts when your index is late. Pay the index tax honestly.

**Job 4 if:** you are measuring history or compacting state. Allowed. Not the first BBPP binary.

---

## What this card refuses

- “Run Core defaults because it is the reference.” Reference equals consensus-readiness, not policy virtue.
- “Run an archive node to be a good citizen.” Citizenship here is validation of monetary claims.
- “Raise datacarriersize so Lightning works.” Lightning does not need 100 kB OP_RETURN. If a backend needs txindex, name txindex.
- Treating compact-state clients as enemies. They attack live-set cost. Complementary, not BBPP-identical.

---

## Profile snippet (job 1 / job 2)

Publish this with any metric claim:

```
job: home-validator | template-miner
binary: bit-block | knots | core
version: …
prune: …
txindex: 0|1
datacarrier / datacarriersize: …
permitbaremultisig: 0
rejectparasites / rejecttokens: …
inscription filter: on|off
template_path: local-gbt | datum | sv2 | pool-unfiltered
hardware: CPU / RAM / disk
```

No profile, no “best practice” claim.
