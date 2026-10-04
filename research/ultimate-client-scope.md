# Ultimate Client Scope
## UTXO-native, consensus-identical, minimum residual mass

**Status**: Research / scope. Does not amend the Charter.  
**Date**: 2026-09-06  
**Parent**: BBPP-00-Charter.md, BBPP-04-What-BBPP-Is-Is-Not.md, docs/roadmap.md  
**Method**: question → delete → simplify → accelerate → automate last. Search, reuse, write only if the problem remains.

This note is the destination shape of a BBPP client. It is not a license to open `src/` early. It is not a clean-room romance. It is what must remain after deletion.

---

## 1. One sentence

A BBPP client is a fully validating Bitcoin node and mining-template engine whose software mass and whose default admission policy are both built to keep the permanent dataset focused on **live monetary claims** — UTXOs that can move — and to make **deadweight bits** expensive, visible, and optional to the hot path.

Consensus stays Bitcoin. The rewrite, if it ever happens, is of *arrangement and defaults*, not of validity.

---

## 2. Two kinds of bits (Landauer classifier)

Landauer’s principle: logically irreversible erasure of one bit requires at least \(k_{\mathrm{B}} T \ln 2\) of work. A public PoW ledger is worse than a single memory: every validating node must retain the bit, refresh it, ship it, and pay the I/O tax forever.

Use Landauer as a **floor and a classifier**, not as a node energy invoice. Real disks, replication, IBD, cooling, and refresh sit many orders of magnitude above that bound. Do not claim a BBPP node operates near the thermodynamic limit.

| Class | What it is | Can it move? | Thermodynamic character | BBPP default |
|-------|------------|--------------|-------------------------|--------------|
| **Live monetary** | UTXO set + minimal undo/history required to validate it | Yes | Working memory of the monetary system | Hot path. Optimise. Keep small. |
| **Witness of liveness** | Headers, coinbase uniqueness, scripts needed to prove a UTXO is valid | Indirectly | Necessary overhead of trustless validation | Keep; compact where honest |
| **Deadweight** | Permanent non-UTXO payloads no later spend extinguishes as value | No | Irreversible memory imposed on every future node | Cold; filtered at policy edge; excluded from default templates; measured |

If a construction creates a spendable UTXO of economic meaning, it is live. If it is an envelope every node must carry after the fee is gone, it is deadweight.

**Measurement rule**

- Do not publish “Landauer joules saved.”
- Do publish: live UTXO bytes vs deadweight admitted by default policy; template size and predicted stale work; IBD time and chainstate RAM on a named hardware profile; hashes-per-joule or orphan differential for filtered vs unfiltered templates.
- The only Landauer sentence allowed: *permanent deadweight is an irreversible information tax replicated N times, where N is the number of validating nodes. Policy that admits it by default is a choice to levy that tax.*

---

## 3. What “rewrite” is allowed to mean

The best part is no part. If you do not add back at least 10% of what you deleted, you did not delete enough. The best code is the code you never wrote.

A ground-up *product* can be assembled from the smallest honest pieces. A ground-up *consensus implementation* is how you reintroduce consensus bugs and call it purity.

### 3.1 Sacred (do not rewrite first)

- Validity of transactions and blocks
- Difficulty, subsidy, halving, script semantics consensus already defines
- Any check whose disagreement would split the chain

These may later be *re-expressed* only after:

1. differential validation against a current Bitcoin reference on historical and adversarial blocks,
2. a named test corpus,
3. a written reason that the existing expression is the part that should not exist.

Until those three exist, consensus is imported or isolated, not invented.

### 3.2 Rewrite surface (this is the actual client)

1. **Admission policy** — mempool and relay defaults that refuse deadweight unless the operator opts in.
2. **Template generator** — local, sovereign, filtered.
3. **UTXO engine** — hot structure around live claims.
4. **Storage split** — live state hot; historical bulk cold; deadweight never indexed as a product feature.
5. **Operator surface** — few knobs, each named, each reversible, each with a metric.
6. **Measurement hooks** — first-class.

Wallet GUI, ordinal explorers, token overlays, and “platform” RPC are not the client.

### 3.3 Binary leanness

- No dependency that is not load-bearing for validation, policy, templates, or measurement.
- No hidden indexer for deadweight.
- No silent default change in a minor release.
- Prefer standard library and existing Bitcoin primitives over a new framework.
- Delete RPC, indexes, and subsystems that exist only to make deadweight convenient.
- Performance work that only makes large data-heavy blocks “fine” is out of scope.

---

## 4. Sequence mapped onto this repo

| Step | Action | Current status |
|------|--------|----------------|
| 0 | Question every requirement | Charter + this note |
| 1 | Delete: default-value table; what we will not relay, template, or index | This push: BBPP-06 |
| 2 | Simplify: configuration layer on an existing consensus-valid node | Later — first `src/` |
| 3 | Accelerate: measure IBD, chainstate, template propagate, orphan contribution | Recipe + scripts in this push |
| 4 | Automate / rewrite UTXO engine only when the config layer and measurements say remaining mass is the problem | Destination. Not current roadmap |

Shipping a rewrite before step 2 automates a process that should have been deleted.

---

## 5. End-state architecture (target, not schedule)

`[network] → policy gate (deadweight default-deny) → mempool (monetary packages, full-RBF) → template (local, filtered, timed) → consensus verify (identical rules, isolated) → UTXO hot set → header / undo → cold archive (optional) → metrics`

- The policy gate is the product.
- The UTXO set is the only structure that deserves heroic engineering.
- The consensus module has no feature roadmap of its own.
- Deadweight, if the operator forces it in, is a documented deviation, not a supported content type.

---

## 6. Success metrics for a future binary

A BBPP binary may use the name only if all of the following are true:

1. Differential consensus agreement with Bitcoin on the primary line.
2. Default policy refuses deadweight admission; every relaxation is an explicit operator flag.
3. Published split: live UTXO bytes vs permanent non-UTXO bytes touched by default configuration.
4. Published template differential: filtered vs unfiltered size and, where measurable, stale/orphan or relay latency.
5. Binary and dependency mass treated as a defect to be deleted.
6. No indexer, RPC, or docs path whose purpose is to make deadweight envelopes first-class. (“Spamrootinals” is an internal nickname only — see the classifier footnote.)

Failure of (1) is not a BBPP client. It is another coin.

---

## 7. What this note does not authorise

- Opening a clean-room consensus implementation because the vision is beautiful.
- A hard fork, a ticker, or “32 MB for physics.”
- Treating Landauer joules as a marketing energy number.
- Declaring other clients illegitimate for different defaults.
- Shipping because the folder exists.

Bit-Block / Knots are not a humiliation; they are the deleted-parts list we have not had to write yet. Use them as the configuration substrate. Let a rewrite earn its way in through numbers.
