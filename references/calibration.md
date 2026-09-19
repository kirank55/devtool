# Calibration

Read this before the first 0-10 score in a session. Each case is: claim -> correct labels -> disposition -> mistake to avoid.

Do not copy these dispositions onto a new seat. Copy the **labeling discipline**.

## Occupied bundle sold as one SKU

### Merge-stack bundle (syntax-aware merge + queue scheduling + conflict bots)

**Claim:** Sparse 3.0. AST collision graph + impacted-target scheduling + agent conflict synthesizer as one SKU.

**Correct:** Occupied ~6.5 as a **bundle of exact occupied slices**. Syntax-aware merge tools (SemaMerge / Mergiraf), interference-graph merge queues (Trunk parallel queues), TIA systems (Datadog / Nx / Launchable), conflict bots (Copilot / CodeRabbit / GitButler). v1 languages (TS/Python) are where `merge` + `tsc`/`pyright` already catch semantic breaks.

**Disposition:** `file_on` / `drop` as a company.

**Mistake to avoid:** Scoring the *bundle* Sparse because no single logo sells all three slices. Straw-man table (Git line merge, desktop diff GUI) while omitting the products that *are* the UX.

### ntfy `--wait-cmd` / silo / build-hook jail for a new ecosystem

**Claim:** Phone notifier for silent local builds; worktree loopback isolation; build-hook jail for Mix/Zig/Conan.

**Correct:** Saturated/Occupied exact SKUs (ntfy, silo, version-manager wrap). Leftover is add-ecosystem or a gist.

**Disposition:** `file_on`.

**Mistake to avoid:** Combination novelty (daemon + phone + wait) as a new category.

## Claim-kill, seat not auto-Occupied

### Tenant cutover with an implausible checksum bound

**Claim:** PgWire proxy + tenant-filtered CDC + atomic cutover, including a sub-10ms cryptographic checksum of a whale tenant. Sparse 2.2.

**Correct:** Kill the **number**. Checksumming the tenant you isolated *because it is huge* does not fit in 10ms; Vitess treats VDiff as async. That is claim hygiene.

PG15 `CREATE PUBLICATION ... WHERE (tenant_id = ...)` is `exact` for the **filtered-replication slice**. Vitess/Ghostferry are `wrong_substrate` for vanilla RDS Postgres. Citus isolate is not "extract tenant out of vanilla RDS."

**Disposition:** Do not use the checksum fail as proof the whole cutover **seat** is Occupied. Re-score slices. Likely `file_on` on native logical replication / DMS for the CDC slice; company verdict follows remaining exact rows, not the physics tell.

**Mistake to avoid:** "Implausible latency => Occupied 7.0."

### Wire-protocol DPOR proxy with an implausible exploration bound

**Claim:** Kafka/Redis wire-protocol proxy, DPOR in CI under 60s, SQL invariants, delta-debug replay. Sparse 2.8.

**Correct:** Kill the **physics** if the seat also claims O(N!) interleavings *and* sub-minute full exploration of real Kafka + real DBs. Kroxylicious is `exact` for a Kafka proxy slice. Coyote/Shuttle/Loom are `language_scoped`. Temporal is `adjacent_pain`. Antithesis is `price_packaging`.

**Disposition:** `as_company` likely Occupied or `file_on` if leftover is a Kroxylicious filter plus SQL assertions. `as_oss` may still be a bounded experiment. Do not publish Occupied 8-9 after a steelman of 5-6.

**Mistake to avoid:** Architecture alternatives filling the exact-mechanics column; discarding a steelman.

## False `exact`

These rows were once labeled `exact` and were wrong. Do not repeat them.

| Cited | Proposed seat | Wrong | Right |
|-------|---------------|-------|-------|
| Coyote, Filibuster, Shuttle/Loom | Kafka wire DPOR in CI | `exact` | `language_scoped` or `adjacent_pain` |
| Temporal / Restate / DBOS | CI interleaving tester for existing brokers | `exact` | `adjacent_pain` |
| Vitess / Ghostferry | Vanilla Postgres tenant extract | `exact` | `wrong_substrate` |
| Azure Split-Merge | Live 2026 cutover product | `exact` | `obsolete` |

## Wrong object

**User:** "rate the PR in a table out of 100." **Follow-up:** "i mean rate the ideas."

**Correct:** The seat under review is the *idea*, not the PR. Drop PR title, commit list, and writing quality from the scoring. Those belong to process review, not occupancy.

**Mistake to avoid:** A blended score that is mostly hygiene, then keeping density as a hidden overall after the user corrects the object.

## Steelman discipline

If thinking says occupancy is 5-6 and OSS is plausible, the published exact-mechanics score may not jump to 8-9 with the same evidence. Publish the steelman. If you discard it, say which **new named row** changed the ceiling.
