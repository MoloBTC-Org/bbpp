# Quantum for Non-Math People

**A research note on Bitcoin, Shor, Grover, and conscious self-custody**

**Status:** Research only — not Charter, not a consensus proposal  
**Date:** 29 August 2026  
**Audience:** Operators, communicators, self-custodians

**Purpose.** Give a reader who does not live in quantum circuits an accurate map of where the risk actually sits, what they can do today without a fork, and what later protocol work does and does not change. Prevent two failure modes: (1) “quantum is easy / 256-bit entropy is toast,” and (2) “quantum is fake / nothing to document.”

**Scope boundary.** BBPP’s Charter remains the three-force model (node permanent-bulk tax, miner hashes-per-joule, software as amplifier). Quantum signature physics is an adjacent layer. It does not rewrite those forces. This note supports best-practice self-custody. It does not champion coin freezes, larger default datacarriers, or a block-size hike sold as “quantum resistance.”

---

## 1. Start here: the locked box

You do not need qubits or block-weight maths to see the practical picture.

Think of a Bitcoin address as a locked box. While the box is unused, the public key is still wrapped behind a hash. The lock is extremely hard to pick with ordinary computers. The moment you spend, you show the key on the street. From that moment a future quantum machine running the right algorithm could copy the key and try to race you.

That is the whole first-order risk in one picture. Mining is not the story. A bigger block is not a stronger lock. A published key is the open door.

Everything below is only that picture made precise.

---

## 2. Two physics layers — do not collapse them

Conversations go wrong when people treat “quantum” as one blob. Bitcoin has two different mathematical objects and two different algorithms. They are not interchangeable.

| Layer | Object | Algorithm | What it means for Bitcoin |
|---|---|---|---|
| Ledger / node physics | Permanent bytes, validation joules, PoW | Classical SHA-256 | Charter ground. Not rewritten by this note. |
| Signature physics | secp256k1 discrete log once a public key is known | **Shor** | The first-order quantum problem. Wallet / spend security. |
| Hash search | SHA-256 nonce or preimage | **Grover** (quadratic only) | Absorbed by difficulty. Not the existential path. |

The rest of this note is almost entirely about the middle row.

---

## 3. Classical computers versus quantum computers

### 3.1 Ordinary machines (wallets and miners today)

Everyday computers, phones, and mining ASICs use bits. A bit is strictly 0 or 1. A Bitcoin private key is a very large random number. From it the wallet derives a public key using elliptic-curve mathematics on the secp256k1 curve. Going backwards — public key to private key — is believed to be infeasible on classical hardware. Trying every possibility would take far longer than the age of the universe.

Mining is a different job. ASICs guess nonces until a SHA-256 hash falls below the current target. That is brute-force search that scales with specialised silicon. Difficulty adjustment raises the target when more hashpower appears.

### 3.2 Quantum machines

Quantum computers use qubits. A qubit can sit in a superposition of 0 and 1, and qubits can be entangled. Two algorithms matter for Bitcoin:

- **Shor’s algorithm** solves the discrete-logarithm problem that protects elliptic-curve signatures. On a large enough fault-tolerant machine it can recover a private key from a known public key in a practical time.
- **Grover’s algorithm** gives only a square-root speedup for unstructured search. For mining and for breaking hashes that is a real but much weaker advantage.

No such cryptographically relevant machine exists today. Present public demonstrations are tens of logical qubits, not the twelve-hundred-plus needed for the published secp256k1 estimates. Document the floor. Do not announce Q-day.

---

## 4. Grover and mining — why this is not the panic

Wrong sentence: “A quantum computer hacks 256-bit entropy.”

Correct sentences:

- A 256-bit Bitcoin private key is not being brute-forced. Grover on unstructured search is a square-root speedup. Work against raw 256-bit entropy remains on the order of \(2^{128}\) — still infeasible.
- Grover on SHA-256 is real but quadratic. Bitcoin’s difficulty adjustment raises the target. Extra hashpower, quantum or classical, is absorbed.
- Building a fault-tolerant quantum hasher that beats modern ASICs at SHA-256 is a different, harder engineering problem than an ECDLP circuit. It is not treated here as an existential mining threat.

Distributed extra hashpower would, in the long run, raise total network hashrate. The secondary concern is a transition period if the first useful quantum hashers were scarce. That is a centralisation caveat, not a reason to enlarge blocks or to declare mining broken.

---

## 5. Shor and wallets — where the risk actually lives

The relevant attack is Shor’s algorithm against the elliptic-curve discrete logarithm problem on secp256k1. That recovers a private key from a **revealed** public key. It does not invert HASH160 in practical time.

### 5.1 When a key is in range

| Situation | Is the public key visible? | Shor relevance |
|---|---|---|
| Hashed address never spent (P2PKH, P2WPKH, etc.) | No — hidden behind a hash | Not the practical path. Grover on the hash remains hard. |
| First spend broadcast | Yes — key appears in the mempool | Short exposure / mempool race. |
| Address reuse or leftover change after a spend | Yes — forever | Long exposure. |
| Early P2PK (including many Satoshi-era outputs) | Yes — key is in the script | Permanently exposed. |
| Taproot key-path spend | Yes — internal key revealed | Long exposure after that spend. |

### 5.2 Long exposure versus short exposure

- **Long exposure.** Public key has been on-chain for a long time. A future CRQC can take those coins at leisure.
- **Short exposure / mempool race.** Public key appears when a spend is broadcast. An attacker must finish Shor and replace the transaction before confirmation (about ten minutes on average). This is the residual personal risk after good hygiene.

BIP-360-class containers address long exposure by removing a standing ECC key-path from the output. They do not, by themselves, stop the mempool race. Short exposure needs post-quantum *signatures*, not just a new output wrapper.

---

## 6. Conscious security: what you can do today with no fork

This is the operational heart of the note. Protocol politics can wait. Custody habits cannot.

- **New address every receive.** Never return to an address that has already spent.
- **Spend the whole UTXO where practical.** Do not leave leftovers on a key you just showed.
- **Use coin control.** Sparrow is the usual example. See which coin you are spending.
- **Know whether the spend path reveals a key.** Taproot key-path is the common one that puts the inner elliptic-curve key on-chain.
- **After confirmation, do not receive there again.** That old address is finished.
- **Keep ordinary self-custody hygiene.** Hardware isolation, verified software, and backups still matter. Quantum does not replace ordinary theft, phishing, or sloppy seeds.

Do this and you are no longer “permanently exposed once spent.” You are mainly exposed in the short window between broadcast and the next block. That is a much smaller problem. It is not zero if a minutes-scale CRQC ever exists. Do not tell people they are “quantum-proof” because they use a good wallet.

### 6.1 Residual risk that hygiene cannot erase

- Old coins that already published their key (early P2PK, reused addresses).
- Human error: change outputs, consolidations, multi-input spends.
- The short race at first spend.
- Other people’s exposed coins, which can still shock price and confidence even if your own hygiene is clean.

Systemic risk from already-exposed supply is a governance conversation (sunset, rate-limit, rescue, or do nothing). It is not solved by a larger block.

---

## 7. From the picture to the published numbers

Primary public estimate used in 2026 discussion:

**Babbush, Zalcman, Gidney, Broughton, Khattar, Neven, Bergamaschi, Drake, Boneh.**  
*Securing Elliptic Curve Cryptocurrencies against Quantum Vulnerabilities: Resource Estimates and Mitigations.*  
PRX Quantum 7, 031001 (2026); arXiv:2603.28846.

Reported operating points for secp256k1 ECDLP via Shor:

- \(\leq 1{,}200\) logical qubits and \(\leq 90\) million Toffoli gates, **or**
- \(\leq 1{,}450\) logical qubits and \(\leq 70\) million Toffoli gates.
- Superconducting assumptions, physical error rate about \(10^{-3}\), planar connectivity: runtime on the order of **minutes**, fewer than \(500{,}000\) physical qubits.

Fast-clock architectures (superconducting / some photonic sketches) can sit in the minutes window — mempool-relevant. Neutral-atom and ion-trap estimates in the same literature are often days — relevant to long exposure, not the ten-minute race.

Authorship is a fact, not a motive analysis. Google Quantum AI accounts for most authors. Dan Boneh (Stanford) and Justin Drake (Ethereum Foundation) are listed. Independently, Bitcoin-side mapping has been funded and presented via Brink (conduition presentation, August 2026). Do not collapse “EF co-author on a Google resource paper” with “Bitcoin PQ work is Ethereum FUD.” Circuit counts stand or fall on reproduction, not affiliation.

Resource estimates have dropped by more than an order of magnitude versus early-2020s constructions. That is a reason to *document* the floor, not a reason to announce Q-day. Mid-2026 hardware remains tens of logical qubits. Vendor roadmaps that reach hundreds of logical qubits cluster around late decade. A 1,000-plus logical-qubit machine with the clock and error rates needed for a minutes-scale ECDLP is more commonly placed early-to-mid 2030s, with high slippage.

---

## 8. Why a giant data centre is not Q-day

Logical qubits are an encoded resource. The physical machine is dominated by physical-qubit overhead, continuous syndrome extraction, classical decoding, magic-state factories for Toffoli gates, cryogenics or vacuum or lasers, and room-temperature electronics that close the decode loop.

A CRQC that finishes ECDLP in minutes is not “a bigger GPU” and is not interchangeable with a multi-gigawatt classical AI campus. Multi-GW facilities are a classical industrial trajectory. A 1,200-logical-qubit cryostat is a coherence, yield, interconnect, and decoding problem. Do not use “12 GW” as a proxy for “quantum is ready.”

The quantum die does not speak secp256k1 at the PCB the way an ASIC speaks SHA-256. Useful cryptographic work sits on top of a continuous error-correction tax. That tax is the present physical moat.

An LLM does not inherit Shor’s exponential. Training and inference are classical. A “structural trick” that extracted secp256k1 private keys without a CRQC would be a classical ECDLP advance, not a language-model miracle. No public evidence as of this note. Treat “unknown classical break” as a separate residual risk with unquantified probability. It is not a reason to ignore Shor, and not a reason to claim that 256-bit keys are already toast.

---

## 9. What a “quantum upgrade” actually is

One day Bitcoin can add new locks that quantum machines are not expected to pick. Those new signatures are fatter than Schnorr’s 64 bytes. Fatter signatures mean fewer payments per block, or higher fees, unless something else changes.

Then there is a choice:

- keep today’s block size and accept fewer, dearer transactions, or
- invent smaller quantum-safe signatures, or
- enlarge the block.

The third option is not “more quantum-safe.” It is more room. Room is a capacity fight. Capacity fights are how people sell a different chain. Security is the primitive. Bytes in a block are not.

Compact hash-based work such as SHRINCS (Blockstream / Nick–Kudinov; BIP published late August 2026) is explicitly option two: shrink the lock so current weight can still carry it. Hybrid Taproot designs that hold a Schnorr key now and a post-quantum key in reserve (`OP_CHECKSHRINCS`) are a new output path, not a block-size hike. They still require wallet hygiene: a Schnorr key-path spend can reveal the inner elliptic-curve key. Stateful compact signatures need a signer that does not reuse one-time slots.

---

## 10. BIP map — purpose, not activation theatre

A BIP number assigned is not “Bitcoin is quantum-proof.” A testnet experiment is not mainnet consensus. Merging a BIP into the repository is editorial, not activation.

| Item | What it does | What it does not do |
|---|---|---|
| **BIP-360 P2MR** | Taproot-like script tree without key-path. Removes long-exposure ECC key from the output. Container for later PQ signatures. | Does not stop the mempool race. Does not choose the PQ scheme. Does not migrate old coins. |
| **BIP-361 sunset draft** | Phased plan after a PQ output exists: restrict new sends to vulnerable types, then encumber or sunset legacy ECDSA/Schnorr. | Does not define the PQ signature. Phase B-style sunsets touch lost, dormant, and early P2PK coins. Governance, not physics. |
| **PQ signature BIPs** | NIST ML-DSA, FN-DSA, SLH-DSA; Bitcoin-native SHRINCS (SHA-256 assumptions). Size versus throughput is the engineering fight. | None activated. Fat NIST schemes are a block-weight / node-bulk issue if they become default spends. |
| **Hourglass-type drafts** | Rate-limit spends of exposed P2PK to avoid a sudden drain of early coins. | Not a PQ signature. Not a general wallet fix. |
| **Rescue / canaries** | Commit/reveal, seed-knowledge proofs, tripwire outputs that signal a CRQC. | Not a substitute for output types or signatures. |

**BBPP posture:** landscape and research. Do not champion coin freezes. If a future PQ spend path bloats blocks, that is a cost to measure under the three-force model, not a subsidy to hide inside “quantum preparedness.”

---

## 11. The simple map

- Hygiene now = hide the key.
- New output types later = never show the old key as a standing output.
- New signatures later = a new lock.
- Bigger blocks = extra suitcase space for a fat lock.
- A different chain = changing the suitcase until it is no longer the same trip.

Stay on the first two. Learn the third. Be highly suspicious of anyone who starts at the last two.

---

## 12. Allowed and forbidden sentences

**Allowed**

- “Only a revealed secp256k1 public key is in practical Shor range.”
- “Good hygiene moves most of the personal risk into the confirmation window; it does not zero it if a minutes-scale CRQC exists.”
- “Grover does not break mining the way ASICs did; difficulty adjusts.”
- “BIP-360 is a proposed container that removes key-path long exposure; it is not a full PQ signature system.”
- “Published 2026 resource estimates put a minutes-scale break on a superconducting CRQC at roughly 1,200–1,450 logical qubits and under half a million physical qubits. No such machine exists.”
- “EF co-authorship on the Google resource paper is a fact. Brink-funded Bitcoin mapping is also a fact.”

**Forbidden as research voice**

- “Quantum computers easily hack 256-bit entropy.”
- “Quantum FUD is just Ethereum.”
- “If you use Sparrow you are quantum-proof.”
- “BIP-360 activated Bitcoin’s quantum defence.”
- “12 GW data centres mean Q-day.”
- “An LLM will skip the physical moat any day now.”
- “Larger blocks make Bitcoin quantum-resistant.”

---

## 13. Self-custody checklist

- Seed is offline, verified, and recoverable by you alone.
- Wallet software is authentic; coin control is on.
- No address reuse. No leftover balances on spent keys.
- You can name the spend path you are using and whether it publishes a public key.
- First-spend is treated as the sensitive moment if a CRQC ever exists.
- You do not wait for a press release called Q-day before learning the output-type and signature landscape.
- You do not confuse node policy (BBPP’s home ground) with signature migration (soft-fork politics).
- You measure any future PQ scheme by weight, assumptions, and wallet operability — not by who shouts “quantum” first.

---

## 14. Sources

- Babbush et al., PRX Quantum 7, 031001 (2026); arXiv:2603.28846.
- BIP-360: https://github.com/bitcoin/bips/blob/master/bip-0360.mediawiki — https://bip360.org/
- BIP-361: https://bips.dev/361/ — https://bip361.org/
- Brink / conduition Bitcoin PQ landscape presentation (August 2026 engineering call).
- SHRINCS and `OP_CHECKSHRINCS`: Blockstream Research (Nick, Kudinov), late-August 2026 BIP publication.
- Hourglass v2 draft (Beast et al.) — P2PK spend throttle.
- BBPP internal research note, 28 August 2026: Quantum Physics Barriers and Communication Boundaries.

Update this file when resource estimates, BIP status, or activation reality change. Do not update the Charter because a BIP number was assigned.

---

## 15. Paste this into an agent for further study

Study Bitcoin quantum risk as a non-specialist. Explain: (1) why only a revealed secp256k1 public key is the practical Shor target; (2) why Grover on mining is secondary because of difficulty adjustment; (3) wallet hygiene that reduces long-range exposure (no reuse, full UTXO spends, avoid Taproot key-path, coin control); (4) the remaining mempool / on-spend race; (5) already-exposed legacy coins including P2PK; (6) post-quantum output types and compact versus NIST-fat signatures (SHRINCS-class versus SLH-DSA); (7) why larger blocks change throughput, not cryptographic hardness; (8) how bundling PQC with a block-size increase is a consensus and politics choice that can resemble a different chain; (9) the 2026 Babbush et al. resource floor and why multi-gigawatt classical campuses are not a proxy for a CRQC. Keep language plain. Separate security from capacity. List what a user can do today with no fork. Do not claim any wallet is quantum-proof.
