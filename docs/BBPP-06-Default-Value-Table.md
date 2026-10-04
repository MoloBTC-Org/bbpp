# BBPP Default-Value Table
## Policy knobs only. Not consensus. Operator escape on every row.

**Status**: Draft for discussion. **V3 flag check 2026-09-29** (Dimitri / Bit-Block V3 + Knots Legacy `V29.3.0.20260920`). Keys he listed are marked. Keys he did not list stay “unconfirmed — delete if `-help` rejects.”  
**Date**: 2026-09-06  
**Parent**: BBPP-00-Charter.md, BBPP-02-Best-Practice-Guidelines.md, research/ultimate-client-scope.md  
**Applies to**: configuration of an existing consensus-valid node (Bit-Block, Knots, Core). This table is the first `src/` payload later — a defaults layer, not a new validator.

Every row is **policy**. A transaction rejected here can still be valid in a block. A block containing it must still be validated. Filtering changes *your* mempool, *your* relay, and *your* template. It does not delete history.

Names follow current Knots / Bit-Block / Core option strings. Confirm with `bitcoind -help` on the binary you run. Silent default changes in a minor release are a Charter defect.

---

## 1. How to read a row

| Column | Meaning |
|--------|---------|
| Knob | Startup / `bitcoin.conf` name |
| BBPP default | Principled starting point |
| Operator escape | How to loosen without forking consensus |
| Three-force rationale | Node tax / miner hashes-per-joule / software amplifier |
| Metric | What you publish if you claim the default works |

If a knob cannot be measured, it is not a BBPP default. It is a preference.

---

## 2. Admission and relay (the product)

| Knob | BBPP default | Operator escape | Three-force rationale | Metric |
|------|--------------|-----------------|----------------------|--------|
| `datacarrier` | V3 stock: **on** with size 0. BBPP cares about **size**, not the boolean. Leave on. | `datacarrier=0` if you want the old pairing | Size 0 already refuses payload. Fighting the boolean is folklore. | Same as size |
| `datacarriersize` | **`0`** (V3 stock) | `42` if you only want a commitment | Content budget vs pointer. 100000 is not BBPP. | Carrier vbytes in mempool / templates |
| `datacarriercost` | **unconfirmed on V3** — not in the 29 Sep paste. Do not put in conf until `-help` shows it | — | Knots-class cost weighting | — |
| `permitbaremultisig` | `0` | `=1` | Bare multisig is a UTXO-set embedding channel. | New bare-multisig outputs per 1000 blocks |
| `permitbarepubkey` | `0` | `=1` | Old embedding and PQ-exposure vector. Not needed for ordinary payments. | New bare-pubkey outputs per 1000 blocks |
| `rejectparasites` | **`1`** (V3 on) | `=0` | Overlay / CAT-21-class. Not “all inscriptions.” | Reject histogram |
| `rejecttokens` | **`1`** (V3 on) | `=0` | Overlay tokens are not live BTC claims. | Reject histogram |
| BIP-110-as-policy family (V3, all **on**) | all seven **on** | toggle any one off | Policy only. Not consensus on the SHA-256 line. Distinct from `rejectparasites` / `rejecttokens`. Dimitri (1 Oct): **three of these already lived passively in the codebase; four are new.** Which three is not specified — treat the family as one product. A switch should apply the *intended purpose* (the related knobs move together), not leave a half-set. | Which of the seven fired |
| `antispamscriptpubkeysize` | on | off | BIP-110 rule 1 — oversized scriptPubKey | — |
| `antispampushdatasize` | on | off | Rule 2 — large push / witness item | — |
| `antispamwitnessversion` | on | off | Rule 3 — undefined witness / tapleaf version | — |
| `antispamtaprootannex` | on | off | Rule 4 — annex | — |
| `antispamcontrolblocksize` | on | off | Rule 5 — oversized control block | — |
| `antispamopsuccess` | on | off | Rule 6 — OP_SUCCESS* | — |
| `antispamtapscriptif` | on | off | Rule 7 — OP_IF / OP_NOTIF in Tapscript (envelope path) | — |
| `spkreuse` | record V3 stock (`allow`) | GUI name differs from conf | Not a BBPP shipping fight this week | — |
| `acceptnonstddatacarrier` | `0` | `=1` | Extra embedding path. Default-deny. | Nonstandard-carrier rejects |

Bit-Block already ships `datacarriersize=0` as an enforced starting point with full operator override. That is the closest living expression of this table on the policy axis.

`rejectparasites` is not “all inscriptions.” Often CAT-21-class.

---

## 3. Monetary reliability (keep the live path cheap)

| Knob | BBPP default | Operator escape | Three-force rationale | Metric |
|------|--------------|-----------------|----------------------|--------|
| Full-RBF (`mempoolfullrbf` / `mempoolreplacement=fee,-optin`) | **on** | opt-in-only if the operator insists | Replacement should be a fee bid, not an envelope workaround. | Replacement rate; stuck-tx reports |
| Package relay / TRUC (`mempooltruc`) | `accept` or `enforce` where sane — never `reject` as default | `reject` | Live monetary packages are the opposite of deadweight. | 1p1c accept rate; Lightning failures attributable to policy |
| `minrelaytxfee` | leave at implementation default unless measured | raise to shed dust floods | Raising without measurement also sheds poor-but-live payments. | Mempool bytes; sub-threshold rejects that later confirmed |
| `dustrelayfee` / `dustdynamic` | V3 stock: dustdynamic **off**. Leave stock unless sheeted | `dustdynamic=3*target:6` as an experiment | Uneconomic outputs become UTXO residents | UTXO count below 3× spend-cost |
| `bytespersigop` | implementation default or slightly stricter | loosen | Sigop stuffing is a template and validation tax. | Sigops per template |

---

## 4. Templates (miner hashes-per-joule)

| Knob | BBPP default | Operator escape | Three-force rationale | Metric |
|------|--------------|-----------------|----------------------|--------|
| Template source | **local policy on this node** | pool-supplied template, named | A template you did not filter is someone else’s junk in your joules. | Stale / empty-work; template vbytes; time-to-first-seen of your blocks |
| Apply §2 filters to GBT / DATUM / SV2 | **yes** | explicit “unfiltered job” profile | Asymmetry here is how spam still lands in your block. | Filtered vs unfiltered weight, same tip |
| `blockmintxfee` | at or above `minrelaytxfee` | lower | Do not mine below what you will relay. | Included-tx feerate histogram |
| `blockmaxweight` / `blockmaxsize` | do **not** raise as a BBPP default | operator-local cap downward allowed | Software must not invert the bulk tax. | Orphan rate vs weight; propagate time |
| DATUM | Job-2 only: `datum=1` / `-datum` / GUI “Mine with DATUM”. Job-1 leave **off** | `datum=0` | Wires hasher to this mempool. Does not by itself loosen §2 filters. Companion: `zmqpubtemplatehint*` | Job on silicon matches `getblocktemplate` on this datadir |
| `corepolicy` | **never set** (V3 stock off) | — | Resets toward Core. Not a DATUM flag. | — |

---

## 5. Node resource posture (home validator)

| Knob | BBPP default | Operator escape | Three-force rationale | Metric |
|------|--------------|-----------------|----------------------|--------|
| `prune` | **on** for home validators (e.g. 550+) | `prune=0` archival | Historical bulk is not the live UTXO. | Disk bytes; IBD hours |
| `txindex` | **off** unless a named backend requires it | `txindex=1` | Serving tax, not monetary-validation tax. | Index bytes; reindex hours |
| other indexes | off unless the job card says so | enable per job | Each index needs a name and a user. | Extra disk; extra IBD |
| `maxmempool` | implementation default | raise/lower | Working memory, not an archive of deadweight. | Mempool bytes vs reject histogram |
| `persistmempool` | on | off | Restart should not throw away live bids. | Time-to-useful-mempool after restart |
| RPC / wallet surface | minimum for the job | enable wallet, REST, ZMQ as named extras | Unused surfaces are attack surface and mass. | Enabled subsystems list |

---

## 6. Explicit non-defaults

- `datacarriersize=100000` or any uncapped-carrier default
- inscription / token / parasite filters off by default
- `permitbaremultisig=1` by default
- block-size or weight hike sold as quantum readiness, Landauer, or “efficiency”
- `txindex=1` on a home validator with no backend that needs it
- any default whose only defence is “Core does it now”

---

## 7. Migration and honesty

- Changing a BBPP default requires a Charter-impact note: which force moves, which metric will be published, what the operator escape is.
- No silent default flip in a patch release.
- A node that loosens every row is still a fine Bitcoin node. It is not running BBPP defaults. That is allowed. The name is not.

**Companions**: BBPP-07, BBPP-10, research/live-vs-deadweight-classifier.md, research/measurement-recipe-deadweight.md.
