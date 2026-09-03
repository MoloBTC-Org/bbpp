# Roadmap

Living list. Not a promise of dates. Not a consensus roadmap.  
Updated: 2026-09-04

## Done (foundation)

- Public README with working `docs/BBPP-*` paths.
- Tree: `docs/` normative, `research/` adjacent, `src/` reserved empty.
- Research notes landed: quantum self-custody; template generation / DMTG.
- Governance page, CONTRIBUTING, issue templates, PR template, GitHub topics list.
- Landscape through Bit-Block V2 + LND guides, OCEAN/DATUM 30 Aug, Monetary Node strip, Bitcoin Purity boundary.

## Now (keep current)

- Refresh Landscape when a client, pool interface, or measured default actually changes.
- Refresh the quantum note only when resource estimates or BIP *status* change — not when a BIP number is assigned.
- Keep README / About / topics accurate. Do not let the front door drift behind the files.

## Next (documentation, still no code)

- Default-value table: policy knobs only (datacarrier, mempool, relay), each with the operator opt-out.
- One-page “which node for which job” card pulled from Landscape §1.2 (home / miner-template / enterprise / compact-state).
- Optional: Lessons Learned line on BitcoinPR + DATUM client-agnostic claim (ask recorded, not a guarantee).

## Later (only after Next)

- Measurement helpers under `scripts/`.
- First code in `src/` — defaults / configuration layer, not a clean-room node.

## Explicitly not on this roadmap

- Hard fork of the primary line.
- 32 MB blocks as “quantum readiness.”
- Shipping a binary because `src/` exists.
- Championing coin freezes or BIP-361-style sunsets.
