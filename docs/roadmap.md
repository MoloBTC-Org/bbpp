# Roadmap

Living list. Not a promise of dates. Not a consensus roadmap.  
Updated: 2026-10-01

## Done (on GitHub — early Sep shape)

- Charter 00–04, Landscape through 30 Aug, governance, issue templates.
- Research: quantum self-custody; DMTG.
- `src/` reserved empty. No BBPP binary.

## Done in workdir (upload this wave)

- `docs/BBPP-07-Which-Node-For-Which-Job.md`
- `docs/BBPP-06-Default-Value-Table.md` — V3 / Knots Legacy flags from Dimitri 29 Sep–1 Oct
- `examples/job1-bit-block.conf` + `examples/job1-knots.conf`
- `research/ultimate-client-scope.md` + `research/live-vs-deadweight-classifier.md`
- Landscape + README + BBPP-04 pointed at Bit-Block **V3**, Monetary Node store, Libbitcoin as job 3 only

## Now

- Copy the first wave onto GitHub.
- Optional: which three of the seven `antispam*` flags were already in-tree (Dimitri: “some (3) lived passively”). Does not block upload.

## Next (after the wave is live)

- Job-2 addendum: `datum=1` + `zmqpubtemplatehint*` on the same datadir as §2 filters.
- One measured GBT / mempool snapshot on a named V3 binary.
- Folder `README.md` under `src/`, `scripts/`, `measurements/`, `references/` (hygiene).

## Hold (`_push/2026-09-06/`)

BBPP-08–11 narratives, dummy profile, operator sheet, unrun scripts.

## Later

- `scripts/` after they have been run.
- First `src/` payload = defaults layer, not a clean-room node. Skip `src/` entirely if Bit-Block + this table already serve jobs 1–2.

## Not on this roadmap

- Hard fork of the primary line.
- 32 MB as “quantum readiness.”
- Shipping a binary because a folder exists.
- Charter tense rewrite.
- Libbitcoin as a job-1 starting point.
