# Live vs Deadweight Classifier
## Worked examples. Research note. Does not amend the Charter.

**Status**: Research  
**Date**: 2026-09-06  
**Parent**: research/ultimate-client-scope.md, BBPP-00-Charter.md  
**Test**: can this bit be extinguished by a spend that moves a monetary claim, or does every future node only get to keep storing it?

Landauer reminder, once: irreversible bits replicated across every validator are a physical tax. Classifier, not a joule invoice.

---

## 1. The test

1. Does this output (or witness) exist so that **bitcoin can move later**?
2. When it is spent, does the reason it occupied space go away because value moved — or does a payload remain in history with no further monetary job?
3. If every node deleted it from *hot* state after validation, would anyone lose the ability to spend a BTC claim they actually hold?

- **Live** if (1) is yes and (3) would break a real spend.
- **Witness of liveness** if it is headers, undo, or script without which you cannot prove a UTXO is valid.
- **Deadweight** if the dominant future operation is “still be stored.”

Classify the dominant effect, then say the residual.

---

## 2. Live monetary (hot path)

| Example | Why live | Residual |
|---------|----------|----------|
| P2WPKH / P2WSH payment | Spend script exists to move sats | Script bytes in history after spend; UTXO drops from hot set |
| P2TR key-path payment | Same | Key revealed on spend (wallet hygiene / PQ note). Still a live claim |
| 2-of-3 P2WSH multisig treasury | Multiple keys, one monetary claim | Larger script than single-sig. Still live. Not *bare* multisig embedding |
| Lightning funding output | 2-of-2 that will be spent cooperatively or via penalty | Channel data off-chain; L1 output is live |
| Consolidation tx | Reduces live-set count | UTXO hygiene |
| Ordinary change | Remaining claim after a spend | Dust change that can never pay its own fee is live-set *bloat* |

These are the bits BBPP software is allowed to work hard for.

---

## 3. Witness of liveness

| Example | Why it stays | Not an excuse for |
|---------|--------------|-------------------|
| Block headers | PoW chain of proof | Inflating header-adjacent bulk |
| Coinbase + BIP34 height | Uniqueness / subsidy audit | Arbitrary coinbase graffiti as a product |
| Undo / prevout for reorg depth you handle | Safety of validation | Archiving the entire witness stack on a home node |
| Script required to show a UTXO is spendable | Without it you are not a full node | Re-encoding a JPEG in that script |

A pruned home node keeps enough of this to validate new blocks and to know its own UTXOs. That is the job-1 floor.

---

## 4. Deadweight (default-deny at policy)

| Example | Pattern | Why deadweight | Policy lever |
|---------|---------|----------------|--------------|
| Large OP_RETURN | `OP_RETURN` + payload | Never spent. Pure permanent bulk | `datacarrier=0` / tiny `datacarriersize` |
| Commitment-sized OP_RETURN | `OP_RETURN` + 20–32B hash + tiny tag | Pointer, not content. Still non-UTXO permanent bytes | Operator turns carrier on and caps ~42 |
| Inscription / envelope | Witness `OP_FALSE OP_IF … OP_ENDIF` on a reveal spend | Payload rides the witness discount; after reveal every IBD still pays | Envelope filter on; do not index |
| Bare multisig as a data dump | `m <blobs that are not keys> n OP_CHECKMULTISIG` | UTXO-set residents that look spendable and usually are not | `permitbaremultisig=0` |
| Unspendable P2TR-shaped data outputs | Random 32-byte tweaks no one has the key for | Live-set pollution | dust + standardness; never loosen dust to “fix” this |
| Stamps / Counterparty / token overlays | Protocol identifiers in carrier or script | Non-BTC claims parasitising BTC validation | `rejecttokens`, `rejectparasites` |
| BRC-20 / inscription-indexed “balances” | Indexer fiction over envelope data | The token is not a BTC UTXO | filters on; no indexer in the binary |

---

### Footnote: “spamrootinals”

A working nickname used in internal notes. **Made-up word.** It is not a protocol term, a BIP, or a court finding.

It bunches several non-monetary embedding styles that show up as deadweight under the test above: Taproot/Ordinals-style witness inscriptions, related envelope reveals, and Stamps-class overlays. Use the three-question test and the table rows. Do not treat the nickname as a classifier of its own.

---

## 5. Edges people weaponise

**“The inscription sat in a real taproot output.”**  
The output may be a live 330-sat dust UTXO. The witness payload is deadweight. Classify both. Policy may admit the dust spend and still refuse the envelope at relay/template. Consensus will still accept the block if a miner includes it.

**“OP_RETURN is better than fake UTXOs.”**  
Lesser evil. OP_RETURN does not sit in the hot UTXO set. It still sits in permanent history. BBPP default is not “please use OP_RETURN for JPEGs.”

**“Multisig is how institutions custody.”**  
P2WSH / P2TR script-path multisig is live. Bare multisig as an embedding trick is deadweight. The knob is `permitbaremultisig`, not “ban multisig.”

**“Lightning needs datacarrier.”**  
Lightning needs a funding output and usually a serving node with ZMQ. It does not need 100 kB OP_RETURN. Small commitment = 42-byte escape, named.

**“Pruning deletes inscriptions, so home nodes are fine.”**  
Pruning drops *your* old blocks. It does not drop the tax on archival IBD, on miners who template the next envelope, or on every new node that must download the span before prune depth.

**“If we filter, we might miss a weird but live script.”**  
True. Publish false-positive reports. That is why every row has an operator escape. It is not why the default should be 100 kB carrier.

---

## 6. What the future UTXO engine may treat as hot

Only:

- outpoints that can still be spent
- scripts / control blocks required to accept a later spend
- undo for the reorg depth you advertise

Everything else is cold or absent on job 1. A later BBPP binary that builds a first-class inscription index has left the Charter even if consensus still matches.
