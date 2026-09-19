# Calibration

Read this before the first 0-10 score in a session. Each case is: claim -> correct labels -> disposition -> mistake to avoid.

Do not copy these dispositions onto a **new** seat. Copy the **labeling discipline**. If the restated v1 *is* a keep-gate worked false keep (tenant-slice orchestrator SKU; Landlock loopback-only test gate; Kafkatrap coordinator-injection proxy; PgLSN Gateway), apply that case's disposition; do not re-keep it as Sparse because leftover prose is strong.

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

### GitHub merge-queue packaging (cancel, quotas, lock drift, lanes, egress, flakes)

**Claim:** A company SKU on `github.com` merge queue + systemd Linux runners: cancel superseded `merge_group` jobs; per-job `CPUQuota`/`MemoryMax` with check annotations; lockfile-to-image drift required check; impacted-target parallel lanes; job-ID egress ledger; history-based flaky quarantine.

**Correct:** Occupied hosts, scored as Occupied even when leftover prose is eloquent. Actions `cancel-in-progress: true` is `exact` for redundant-run cancel. systemd `CPUQuota`/`MemoryMax` are `exact` primitives; annotations are auto-reject 5. `npm ci` already fails lock mismatch; image-label join is a 50-line Action (auto-rejects 2+5). Trunk parallel queues are `exact` for impacted-target lanes. harden-runner already maps egress to step/job/workflow and ships domain allowlists. Trunk flaky-tests quarantine plus in-queue anti-flake occupy the flake gate. Calibration's merge-stack bundle already covers syntax-aware merge + queue scheduling + conflict bots.

**Disposition:** `file_on` the named host. `as_company` Occupied. Do not spend an `agent_opt_out` hunt emitting six Occupied cards in this aisle.

**Mistake to avoid:** Treating merge_group wiring, check-annotation UX, or "Trunk is a paid SKU not a GitHub-native daemon" as vacancy. Reusing a `merge_group` webhook-dispatch quote as evidence of a different leftover.

### npm/Node PATH enforcement packaging (sandbox, engines, bins, prefix, NODE_OPTIONS)

**Claim:** Company SKUs on the developer laptop: per-package npm lifecycle net sandbox (`bwrap --unshare-net` + write allowlist); engines/Volta pin exec interlock; lockfile-pinned `.bin` PATH gate; per-project `npm i -g` prefix redirector; `NODE_OPTIONS` flag allowlist wrapper.

**Correct:** Occupied hosts. `bwrap --unshare-net` is already the loopback-up / no-egress primitive in the Landlock case. lavamoat `allow-scripts` is `exact` for lifecycle allowlists; `--experimental-bins` is `exact` for bin-confusion. Volta shims + fnm `engines.node` occupy interpreter pinning. npm `prefix` / folders docs occupy global-install layout. Node CLI `NODE_OPTIONS` precedence occupies the flag surface; an allowlist is a 50-line wrapper (auto-rejects 2+5). Hitting `bwrap` / lavamoat / Volta as class 1–2 on the first two seats **is** a substrate-switch trigger even if those names are not in the merge-queue parenthetical.

**Disposition:** `file_on` lavamoat, Volta, npm folders, or Node CLI docs. `as_company` Occupied.

**Mistake to avoid:** Staying in host-runtime enforcement because "Volta isn't listed next to Kroxylicious in SKILL.md." Citing GitHub blob READMEs with paraphrased isolation sentences. Socket.dev 403/`NEED_EVIDENCE` rows on a keep.

### Redis RESP sidecar packaging (ACL, faults, prefix migrate, audit, lag router)

**Claim:** Company SKUs in front of vanilla Redis: ACL-bridging command firewall for legacy AUTH; per-command DELAY/ERROR fault proxy for CI; key-prefix dual-write live migration; command+key audit tap with value redaction + OTel; replica-lag-aware read router.

**Correct:** Occupied hosts. Redis ACL (`+@all -@dangerous`) is `exact` for command firewall. Envoy Redis filter Delay/Error faults (including per-command `GET`) are `exact` for RESP-aware chaos. `MIGRATE` + RedisShake occupy prefix live sync; Envoy prefix routes occupy the proxy slice. `MONITOR` and Redis Software audit occupy command+key logging; value redaction already ships. Envoy `ReadPolicy` + Redis `WAIT` / `min-replicas-to-write` occupy lag-aware routing. Conjunction v1 is the same Occupied-bundle mistake as tenant-slice cutover.

**Disposition:** `file_on` Redis ACL, Envoy redis_proxy, or RedisShake. `as_company` Occupied.

**Mistake to avoid:** Treating "legacy-client mapping" or "OTel export" as vacancy on an `exact` primitive. Scoring `Occupied 6.5` as if half-points were a keep-shaped leftover.

### rustc/cargo packaging (sccache, SBOM, bloat, geiger, vendor)

**Claim:** Company SKUs on rustc+cargo: shared rustc cache with per-crate hit ledger; signed CycloneDX at `cargo build`; linker bloat + duplicate-crate CI gate; unsafe-surface allowlist gate; offline airgap registry mirror.

**Correct:** Occupied hosts. sccache (S3/GHA/multilevel) and `Swatinem/rust-cache` are `exact` for shared compile cache; a ledger is auto-reject 5. cargo-auditable, cargo-cyclonedx, native `-Z sbom`, auditable2cdx occupy SBOM emit; signing is auto-reject 5. `cargo tree -d`, cargo-deny bans, cargo-bloat occupy duplicate/bloat; a CI Action is auto-rejects 2+5. cargo-geiger counts `unsafe`; `--check`+whitelist is a filed leftover (auto-reject 5). `cargo vendor`, source replacement, JFrog Cargo remote, frostmirror occupy airgap mirrors.

**Disposition:** `file_on` sccache, cargo-auditable, cargo-deny, cargo-geiger, or `cargo vendor`. `as_company` Occupied. Hitting sccache/cargo-auditable on the first two seats **is** a substrate-switch trigger.

**Mistake to avoid:** Staying in rustc+cargo because those CLIs are not in the merge-queue parenthetical.

### Kernel/eBPF packaging (cgroup budget, fapolicyd, io_uring, scx, Tetragon)

**Claim:** Company SKUs on Linux kernel + cgroup v2 (not netns isolation): freeze-on-PSI budget gate; fanotify exec-allowlist keyed on lockfile hashes; BPF-LSM repo-scoped exec interlock; io_uring allow-deny profile fragments; sched_ext interactive-vs-build latency daemon; eBPF exec provenance with OTel.

**Correct:** Occupied hosts. systemd-run + `CPUQuota`/`MemoryMax` + cgroup freezer/`cgroup.freeze` occupy the budget/freeze slice (hunt 1 already Occupied systemd quotas). fanotify `FAN_OPEN_EXEC_PERM` + fapolicyd trust/whitelist occupy exec allowlisting; lockfile join is auto-reject 5. AppArmor + BPF LSM + fapolicyd occupy MAC/exec interlock. seccomp-BPF, `SystemCallFilter=`, `io_uring_disabled`, Docker default profile occupy io_uring deny. sched_ext + `scx_layered` occupy cgroup-aware scheduling. Tetragon, Tracee, Falco occupy eBPF exec/file events; OTel export is auto-reject 5.

**Disposition:** `file_on` systemd, fapolicyd, `SystemCallFilter`, scx_layered, or Tetragon. `as_company` Occupied.

**Mistake to avoid:** Treating lockfile-hash policy source or OTel export as vacancy on an `exact` primitive. Regenerating hunt-1 systemd quotas under a "dev laptop not merge queue" host rename.

### Tenant-slice cutover orchestrator (filter + FK walk + switchover as one SaaS)

**Claim:** Sparse 3.0. Vanilla RDS/Aurora tenant extract: row-filtered `pgoutput` slots, foreign-key traversal, WAL catchup, sub-second pool drain.

**Correct:** Occupied **bundle**. PG15 `CREATE PUBLICATION ... WHERE` is `exact` for the filter slice. AWS DMS **source filters** already take column predicates (including tenant id). Logical-replication switchover CLIs (`pg_easy_replicate`, sbshift) occupy lag-watch + read-only cutover + sequence refresh. Leftover "infer tenant closure and emit WHERE" is auto-reject 5 / `file_on` pgcopydb (see issue 161). `1_vacant_process` may not pass while an `exact` slice sits on the card. `as_plugin` is not Greenfield.

**Disposition:** `file_on` / `drop` as a company. `as_oss` may still be Sparse for the closure-inference leftover.

**Mistake to avoid:** Keeping the bundle Sparse because no single logo sells filter + FK walk + cutover. Calling DMS "full-instance only" without fetching the source-filter page. Passing vacant-process by renaming the seat to "the orchestrator."

### Landlock "loopback-only" test gate

**Claim:** Sparse 2.5. Unprivileged `hermetic-test <cmd>` using Landlock v3/v4 + seccomp-bpf to allow `127.0.0.1` and block egress, with CI diagnostics.

**Correct:** Occupied, plus a claim-hygiene kill on the mechanism. Landlock ABI v4 matches TCP **ports**, not IP addresses. The loopback-up / no-egress primitive is a new netns with `lo` up (`bwrap --unshare-net`, firejail `--net=none`, systemd `PrivateNetwork`). landrun already wraps Landlock (filesystem + `--connect-tcp` / `--bind-tcp`). Leftover diagnostics is auto-reject 5.

**Disposition:** `file_on` landrun or bubblewrap. `as_company` Occupied. Do not keep Sparse by labeling landrun `adjacent_pain` for missing error-message UX.

**Mistake to avoid:** Treating `unshare -n` as "loopback is impossible." Omitting bubblewrap/firejail from the table. Using Landlock as the network isolation story without fetching the ABI page.

### Kafkatrap (coordinator-frame injection proxy in CI)

**Claim:** Sparse 2.5. Deterministic Kafka wire-protocol proxy that injects `JoinGroup` / `SyncGroup` / `Heartbeat` / `OffsetCommit` frames at record offsets in CI. Toxiproxy is frame-blind; Testcontainers is container lifecycle; Antithesis is a hypervisor.

**Correct:** Occupied leftover. Kroxylicious is `exact` for a Kafka protocol proxy (calibration already says this). Filter interfaces exist per API key (`JoinGroupRequestFilter`, `HeartbeatRequestFilter`). `shortCircuitResponse` / `errorResponse(ApiException)` returns a protocol-valid coordinator error without forwarding. Kroxylicious also rewrites advertised broker addresses in `Metadata` / `FindCoordinator`. kfake `ControlKey` injects API-key-specific responses in-process for CI. grepplabs/kafka-proxy rewrites Metadata / FindCoordinator. The only named leftover (offset-triggered rules + local HTTP control API) is test-runner UX: auto-reject 5. `1_vacant_process` may not pass while an `exact` Kroxylicious row sits on the card. `as_plugin` Occupied plus `file_on: none` is a card fail (G3/G8).

**Disposition:** `file_on` Kroxylicious Filter API (or kfake `ControlKey`). `as_company` Occupied. `as_oss` may still be Sparse for a bounded filter/harness.

**Mistake to avoid:** Keeping Sparse because Kroxylicious is "an enterprise gateway, not a lightweight CI daemon." That is packaging, not a vacant process. Citing the GitHub README while omitting the Filter API. Stitching quotes. Scoring `as_oss` Greenfield (illegal band 1.5) *below* `as_company` Sparse.

### PgLSN Gateway (session LSN read-your-writes PgWire SaaS)

**Claim:** Sparse 2.5. Managed PgWire proxy that captures `pg_current_wal_lsn()` on commit and routes later reads to replicas whose `pg_last_wal_replay_lsn()` is caught up, else primary, on AWS RDS / Aurora Postgres. RDS Proxy does not split reads/writes; Pgpool only has `delay_threshold`.

**Correct:** Occupied **bundle**. Slices: PgWire pooler (PgCat, Pgpool-II, PgDog, ProxySQL PostgreSQL, RDS Proxy) · session stickiness after a write (Pgpool-II `disable_load_balance_on_write` = `always` / `transaction` **on the load-balancing page the hunt already cites**) · host-native read-your-writes on Aurora (`apg_write_forward.consistency_mode=SESSION`) · commercial no-stale-read R/W-split SaaS (Heimdall table timestamps + replica lag) · cluster LSN lag (PgDog `ban_replica_lag`). The per-session LSN cookie leftover is go-pgrouter `pg_min_lsn` (`language_scoped`) and auto-reject 5 / `file_on` the pooler. ProxySQL is not MySQL-only. `as_plugin` Occupied plus `file_on: none` is a card fail.

**Disposition:** `file_on` / `drop` as a company. `as_oss` may still be Sparse for an LSN cookie on an existing pooler.

**Mistake to avoid:** Keeping the bundle Sparse because no single logo sells "LSN cookie + managed SaaS." Citing Pgpool load-balancing docs without `disable_load_balance_on_write`. Naming Aurora in a comment and omitting `SESSION` write-forwarding as a row. Invented quotes on RDS Proxy / PgCat / Prisma.

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
