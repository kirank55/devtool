# Keep gate

Load this file at `SKILL.md` step 8 **before** any `as_company: Sparse` or
`as_company: Greenfield`. Do not skip it on a "clear keep." Balanced models
emit Sparse to be helpful. This file is the fail-closed latch.

Default: `as_company` is Occupied or `file_on`. A Sparse/Greenfield **company
keep** is allowed only if every check below passes. Failure does not prove the
*pain* is fake. It blocks the keep.

This is not a rater verdict. It only forbids a finder company-keep.

## Checks (all required for a company keep)

**G1. Quotes are literals.** Each incumbent `quote` is a contiguous substring
of a page **fetched this run** at `url`. Ellipsis may join two substrings only
if both appear on that page. 404, JS-empty, or paraphrase -> that row is
`NEED_EVIDENCE`. A keep may not include `NEED_EVIDENCE` rows.

**G2. Query classes, not five logos.** Search hit the mandatory classes in
[search-playbook.md](search-playbook.md) for this substrate. A table of five
adjacent or straw-man rows (desktop GUI, wrong language, full-instance
migrator) does not satisfy G2.

**G3. Leftover names a host -> `file_on` that host.** If any leftover sentence
names a product, repo, flag, or issue, `file_on` is that URL (not `none`).
`as_plugin` may not be Greenfield in that case.

**G4. Exact slice occupies vacant-process.** If any row is `exact`,
`1_vacant_process` is `fail` unless `file_on` is set on that slice **and**
`as_company` scores only the remaining named process. You may not pass vacant
process by redefining the seat as "the orchestrator around the exact primitive."

**G5. Conjunction v1 is a bundle.** If `v1_as_shipped` joins two or more
mechanisms with "and" (filter + cutover, jail + diagnostics, proxy + scheduler),
split into slices before scoring. If each slice has an `exact` or adjacent
host, the SKU is Occupied. No single logo selling the bundle is not vacancy.
Load [calibration.md](calibration.md) Occupied-bundle cases.

**G6. Auto-reject #5 default.** Leftover that is diagnostics, a checkbox,
row-filter flags, test-runner UX, or "orchestration around X" is "add this to
incumbent X." Fire auto-reject 5. Do not talk it into a company in prose.

**G7. Mechanism claims.** Latency bounds, IP-vs-port filters, complexity
(`O(N!)`), checksum windows, and "sub-second cutover" must be stated on a
fetched kernel, protocol, or vendor page. Else `claim_hygiene: implausible`,
delete the claim from `v1_as_shipped`, and re-score. Hygiene fail is not
Occupied-by-itself (see [rubric.md](rubric.md)); inventing a kernel property
**is** a keep block until v1 is restated without it.

**G8. Split-verdict sanity.** `as_plugin` Greenfield plus an `exact` incumbent
row is a card fail. `as_oss` occupancy **lower** than `as_company` needs a
one-line reason or it is a card fail.

**G9. Steelman.** Published `exact_mechanics_density` may exceed the pre-search
ceiling only if G2 added **named** rows. Missed-search is not a low ceiling.

## Emit

`keep_gate: pass` only if G1-G9 hold.

`keep_gate: fail` -> `as_company` is Occupied, Saturated, `file_on`, or `drop`.
Never Sparse/Greenfield keep. `as_oss` / `as_plugin` may still be Sparse.

## Worked false keeps (labeling, not generation seeds)

Do not generate from these. If a restated seat **is** one of them, copy the
labeling: company Occupied / `file_on`, not Sparse keep.

| Claimed keep | Correct |
| --- | --- |
| PG15 row-filter + FK walk + WAL catchup + pool drain as one SaaS SKU | Bundle. `exact` on `CREATE PUBLICATION ... WHERE`; DMS source filters and logical-replication switchover tools occupy cutover. `file_on` the orchestrator. Auto-reject 5. |
| Landlock v3/v4 CLI that "enforces loopback-only IPs" for `npm test` | Physics fail (Landlock net is TCP **ports**). landrun is the Landlock wrapper. `bwrap --unshare-net` is loopback-up / no-egress. `file_on` landrun or bubblewrap. Auto-rejects 1 and 5. |
| Kafkatrap: Kafka wire proxy that injects coordinator frames (`JoinGroup` / `Heartbeat` / `OffsetCommit`) at record offsets in CI | Occupied leftover. Kroxylicious is `exact` for the proxy slice (`JoinGroupRequestFilter`, `HeartbeatRequestFilter`, `shortCircuitResponse` / `errorResponse`). kfake `ControlKey` is the CI drop-in. Offset-triggered rules are auto-reject 5. `file_on` Kroxylicious. `as_plugin` Occupied forbids `file_on: none`. |
| PgLSN Gateway: PgWire proxy + commit-LSN capture + replica matrix + managed SaaS as one SKU on RDS/Aurora | Occupied bundle. Pgpool-II `disable_load_balance_on_write` is `exact` for session stickiness (on the load-balancing page). Aurora `apg_write_forward.consistency_mode=SESSION` is `exact` on the named Aurora host. Heimdall sells R/W-split-with-consistency. LSN cookie leftover is auto-reject 5 / `file_on` the pooler. |
