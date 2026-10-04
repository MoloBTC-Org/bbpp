# Examples

Pasteable policy files. Not consensus. Confirm every key with `bitcoind -help` on the binary you run.

| File | Job | Binary |
|------|-----|--------|
| [job1-bit-block.conf](job1-bit-block.conf) | Home validator | Bit-Block V3 |
| [job1-knots.conf](job1-knots.conf) | Home validator | Knots Legacy `V29.3.0.20260920` (DATUM + BIP-110 keys match V3) |

V3 stock that these files keep: `datacarrier=1` + `datacarriersize=0`, `rejectparasites=1`, `rejecttokens=1`, seven `antispam*` = on, `datum=0` (job-1 is not mining).

BBPP additions on top of stock: `prune=550`, indexes off, `acceptnonstd*=0`, local RPC bind.

Job-2 is `datum=1` on this same file, not a second personality. That addendum is not in this folder yet.
