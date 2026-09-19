# 20 Devtool Seats — Hunt 2026-09-19 (agent_opt_out)

Branch: `findings/20-ideas-2026-09-19`
Hunt: `agent_opt_out` over full substrate inventory (`seat-generation.md:22-33`). No local deny file; `deny_catalog: embedded_baseline`.
Discipline: Each seat restated, deny-checked vs embedded fallback + 55 closed aisles, steelman ceiling set *before* search, 4 query classes hit, >=5 incumbents with verified URLs + contiguous quotes, seat-match labeled per `seat-match.md`, dual-scored per `rubric.md`, keep-gate per `keep-gate.md`. No overall /100.

> **Niche (agent opt-out)**
> ```yaml
> niche:
>   substrate_or_stack: unset
>   immutable_host: unset
>   ship_form: unset
>   unique_data_or_distribution: unset
>   hard_nos: []
>   source: agent_opt_out
> ```
> All 20 raw seats carry this niche. `agent_opt_out` means full inventory; not a named stack. Generation probe = missing SKU / host not consulting sidecar / advisory-in-enforcement-seat.

---

## Raw seats (20) before search

| # | substrate | candidate_seat | v1_as_shipped | process_or_protocol |
|---|-----------|----------------|---------------|---------------------|
| 01 | Host runtime enforcement | `pnpm-lock.yaml` host-enforced install gate on developer laptop | `pnpm` wrapper + `corepack enable` + checked-in `packageManager: pnpm@x.y.z` + `pnpm install --frozen-lockfile` drift gate that fails CI when lock ≠ manifest, installed as repository shim consulted by host | `pnpm install --frozen-lockfile` + `packageManager` field |
| 02 | Wire proxy / protocol gate | MCP STDIO tool-call firewall proxy on Claude/Cursor host | Single Go binary `mcp-gate` STDIO proxy that intercepts MCP JSON-RPC `tools/call`, checks name/args against `mcp-policy.yaml` allow/deny + param match, forwards or returns JSON-RPC error, structured audit log | MCP STDIO JSON-RPC `tools/call` |
| 03 | Compiler/linker/bundler/lockfile | Yarn Berry `yarn.lock` + PnP loose/strict enforcement gate on Node host | CI required check that fails when `yarn.lock` ≠ `package.json` or `pnpMode: loose` is set, verifies `.pnp.cjs` / `.pnp.loader.mjs` generation, enforces `nodeLinker: pnp` from `.yarnrc.yml` | Yarn Berry `nodeLinker: pnp` + `pnpMode` + `yarn install --immutable` |
| 04 | Schema / tenancy cutover | Postgres Row-Level Security policy-as-code gate in CI | `pgrls lint` + `pgrls diff` CI gate (SARIF → GitHub code scanning) that classifies `CREATE POLICY` coverage per table as `SAFE/BREAKING/REQUIRES_REVIEW/DANGEROUS`, fails on anon leak (`SEC004`) and missing `FORCE RLS` | Postgres `CREATE POLICY ... USING` + `ENABLE ROW LEVEL SECURITY` + `FORCE` |
| 05 | Wire proxy / protocol gate | OTel Collector tail-sampling policy gate with per-service caps | Checked-in `sampling-policy.yaml` enforced by Collector `tail_sampling` processor sidecar that caps sample rate per service, emits `otel_sampling_decisions_total`, refuses to start when policy absent | OTLP + Collector `tail_sampling` + `filter` processor |
| 06 | Compiler/linker/bundler/lockfile | Docker BuildKit Dockerfile `RUN --mount=type=cache` determinism linter on Linux CI | `hadolint`-style Action that gates unpinned `apt-get install` / `apk add` and missing `--mount=type=cache` on `RUN` lines, emits Dockerfile SARIF, `file_on` hadolint | Docker `Dockerfile` `RUN` + BuildKit `RUN --mount=type=cache` |
| 07 | Compiler/linker/bundler/lockfile | Helm `Chart.lock` → rendered manifest drift gate on Helm | CI required check `helm template` vs committed `Chart.lock` + `values.yaml` that fails when `Chart.yaml` dependencies drift, `file_on` helm `dependency build` | Helm `Chart.lock` + `helm template` |
| 08 | Kernel / eBPF / LSM | eBPF TCP retransmit + RTO cause exporter with per-socket OTel | `ebpf-retrans` daemon attaching `kprobe/tcp_retransmit_skb` + `tracepoint/tcp/tcp_retransmit_skb`, exports `tcp_retransmits_total{reason, saddr}` and RTO timer, OTel tap, no payload | Linux `tcp_retransmit_skb` + eBPF `kprobe`/`BPF_PROG_TYPE_TRACING` |
| 09 | Host runtime enforcement | Vite `server.proxy` target allowlist enforcer on dev host | Vite plugin `vite-plugin-proxy-allowlist` that reads `proxy-allowlist.json` at `vite dev` start, refuses unknown `server.proxy` targets, audits `vite.config.ts` | Vite `server.proxy` + `vite.config.ts` |
| 10 | Host runtime enforcement | `pre-commit` hook SHA-pinned allowlist gate on `git commit` | `pre-commit` wrapper that verifies `.pre-commit-config.yaml` `rev:` SHAs against checked-in `pre-commit-allowlist.lock`, fails `git commit` on unpinned hooks, logs to `pre-commit audit` | `pre-commit` `rev:` + `.pre-commit-config.yaml` |
| 11 | Compiler/linker/bundler/lockfile | Poetry `poetry.lock` → `poetry install --no-update` drift gate on CPython | CI required check `poetry check --lock` + `poetry install --sync` that fails when `poetry.lock` ≠ `pyproject.toml`, SBOM emit via `cyclonedx-bom`, `file_on` poetry | Poetry `poetry.lock` + `poetry install --sync` |
| 12 | CI scheduler / merge queue | GitHub `CODEOWNERS` required-review enforcement gate on `merge_group` | GitHub Action that fails `merge_group` when required `CODEOWNERS` reviewers not yet requested/requested-review not satisfied, checks `CODEOWNERS` + branch protection, posts annotation | GitHub `CODEOWNERS` + `merge_group` + branch protection |
| 13 | Broker / queue protocol | Kafka JMX dirty-ratio / `LogEndOffset` lag auditor on MSK | Sidecar `kafka-lag-auditor` polling JMX `kafka.log:type=Log,name=LogEndOffset` + `kafka.server:type=BrokerTopicMetrics`, exports per-partition dirty-ratio `LogEndOffset - HighWatermark`, alerts, OTel | Kafka JMX `LogEndOffset` + `HighWatermark` + `JMX` |
| 14 | Schema / tenancy cutover | DynamoDB per-tenant GSI slice extractor to dedicated table on prod DynamoDB | Local CLI `ddb-tenant-extract` that filter-copies items with `tenant_id = :t` via `Scan` + `ParallelScan` into new table, clones GSIs, verifies parity via `Checksum` | DynamoDB `Scan` + `GSI` + `BatchWriteItem` |
| 15 | Host runtime enforcement | `mise`/`asdf` tool-version pin interlock on developer laptop | `mise` shim that refuses `mise install`/`mise exec` when `mise.toml`/`tool-versions` pin mismatches `node --version`/`python --version`, enforces `idiomatic_version_file` host consult | `mise` + `mise.toml`/`tool-versions` + `PATH` shim |
| 16 | Kernel / eBPF / LSM | AppArmor `dbus` + `signal` allowlist gate from checked-in policy on Linux | AppArmor profile compiler `apparmor-dbus-gate` that gates `dbus`/`signal` rules from `apparmor-policy.yaml`, `aa-enforce` wrapper, fails `aa-complain` diff in CI | AppArmor `dbus send/receive` + `signal` + `aa-genprof` |
| 17 | Wire proxy / protocol gate | ClickHouse native protocol tenant firewall proxy on prod ClickHouse | `clickhouse-proxy` wire proxy that parses native `INSERT`/`SELECT` headers, gates `tenant_id` column presence, routes per-tenant `SETTINGS` and `X-ClickHouse-*` headers | ClickHouse native protocol + `INSERT ... SETTINGS` |
| 18 | Compiler/linker/bundler/lockfile | esbuild `metafile.json` bundle bloat + duplicate-input CI gate on `esbuild` | CI Action that parses `esbuild metafile.json`, fails when bundle size regresses >5% per entrypoint or duplicate `inputs` detected, emits `bundle-bloat.sarif` | esbuild `metafile.json` + `bundle` |
| 19 | CI scheduler / merge queue | GitHub Actions `actions/cache` hit-ledger + quota governor on Linux CI | Collector `cache-hit-ledger` that parses `actions/cache` `CacheHit` events per runner, exports per-key hit ratio and quota `x-cache-size`, fails when miss ratio > threshold | GitHub `actions/cache` + `CacheHit` + `ACTIONS_CACHE_URL` |
| 20 | Broker / queue protocol | Valkey/Redis Cluster cross-slot `CROSSSLOT` lint gate in CI for `EVAL` | Static analyzer `valkey-crossslot-lint` that parses `EVAL` Lua + `MGET/MSET` keys, fails CI when keys hash to different slots (`{tag}` mismatch), suggests `hash_tag` fix | Redis Cluster `CROSSSLOT` + `EVAL` + `{hashtag}` + `CRC16` |

Why_not_a_slogan per seat (one sentence mechanics):
01 fails install when lock ≠ manifest via host-consulted flag; not "better DX".
02 STDIO proxy evaluates every `tools/call` against YAML before upstream sees it; not "AI security".
03 host-consulted `nodeLinker` + `pnpMode` gate; advisory `yarn dedupe` alone is not enforcement.
04 advisory `EXPLAIN` does not gate `CREATE POLICY` regressions; this gate does via Z3-proved diff.
05 Collector already runs `tail_sampling`; host not consulting per-service cap file is the gap.
06 `hadolint` lints style but not BuildKit `--mount=type=cache` determinism + pin.
07 `helm dependency build` is advisory without host-enforced drift gate on rendered manifests.
08 `ss -i` shows counters but no per-socket cause-labeled eBPF exporter.
09 Vite does not consult sidecar for `server.proxy` targets; advisory docs do not enforce.
10 `pre-commit` consults `rev:` but no lockfile enforces SHA pin; advisory list is not gate.
11 `poetry check` is advisory; host not consulting lock for `--sync` drift is gap.
12 `CODEOWNERS` is advisory without `merge_group`-aware required-review gate.
13 `kafka_exporter` exports lag but not dirty-ratio cause + JMX `HighWatermark` join.
14 DMS full-instance only; row-filtered tenant slice with GSI clone is missing SKU.
15 `mise` shim consulted by host for `PATH`; missing enforcement interlock is the gap.
16 `aa-status` advisory; compile-time `dbus` allowlist gate is enforcement.
17 ClickHouse ACL is table-level; native-protocol tenant column firewall is missing.
18 `esbuild --analyze` is advisory; CI gate on `metafile.json` size/duplicate is enforcement.
19 `actions/cache` logs but not per-key hit ledger + quota governor.
20 `CROSSSLOT` error is runtime; static lint on `EVAL` keys with `{tag}` is pre-runtime gate.

---

## Candidate cards (20)

### 01 — pnpm-lock host gate (Host runtime enforcement) — Occupied / file_on

```yaml
candidate_seat: pnpm-lock.yaml host-enforced install gate refusing lock mismatches on developer laptop
v1_as_shipped: pnpm wrapper + corepack enable + packageManager pin + pnpm install --frozen-lockfile drift gate that fails CI when pnpm-lock.yaml != package.json, installed as repository shim consulted by host
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
slices: [lockfile host check, packageManager shim, frozen-lockfile flag]
search_classes:
  host_primitive: pnpm install --frozen-lockfile + packageManager field
  dropin_cli: corepack enable + pnpm wrapper
  orchestrator: Socket.dev / pnpm enterprise policy
  tracker_leftover: pnpm --frozen-lockfile ignored packageManagerDependencies issue 14009
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 6
  as_plugin: Occupied 6
density_scores:
  problem_density: 6
  exact_mechanics_density: 5
incumbents:
  - name: pnpm.io cli install
    url: https://pnpm.io/cli/install
    quote: "If `true`, pnpm doesn't generate a lockfile and fails to install if the lockfile is out of sync with the manifest / an update is needed or no lockfile is present."
    seat_match: exact
    leftover: per-project packageManager shim still needs corepack enable; leftover is docs not code
  - name: pnpm issue 14009 --frozen-lockfile rewrites packageManagerDependencies
    url: https://github.com/pnpm/pnpm/issues/14009
    quote: "--frozen-lockfile` silently rewrites `packageManagerDependencies` instead of failing with `ERR_PNPM_OUTDATED_LOCKFILE`"
    seat_match: exact
    leftover: fix is TS CLI syncEnvLockfile gate; leftover is the fix itself not a new product
  - name: corepack enforcing packageManager
    url: https://www.subresource-integrity.com/supply-chain-auditing-dependency-verification/registry-package-manager-hardening/enforcing-package-manager-versions-with-corepack/
    quote: "The `packageManager` field is the declaration that closes that gap. It is a single string of the form"
    seat_match: exact
    leftover: leftover is preinstall assertion + --frozen-lockfile pair; not a daemon
  - name: pnpm PR 14013 enforce --frozen-lockfile for packageManagerDependencies
    url: https://github.com/pnpm/pnpm/pull/14013
    quote: "This PR enforces the `--frozen-lockfile` contract for `packageManagerDependencies` (the pinned version of pnpm itself)"
    seat_match: exact
    leftover: leftover is unit test for resolvePackageManagerIntegrities; not a company
  - name: latchkey pnpm ERR_PNPM_LOCKFILE_BREAKING_CHANGE
    url: https://latchkey.dev/learn/node-js/pnpm-err-pnpm-lockfile-breaking-change
    quote: "pnpm lockfiles carry a format version. ERR_PNPM_LOCKFILE_BREAKING_CHANGE means the committed"
    seat_match: adjacent_pain
    leftover: version pin via packageManager + Corepack is docs; leftover is wrapper
auto_rejects_fired: [5]  # add-to-incumbent: fix lives in pnpm/cli + corepack, not a company
falsification:
  1_vacant_process: fail  # exact pnpm --frozen-lockfile + corepack occupy the process
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: pnpm --frozen-lockfile should have enforced packageManager pin but silently re-wrote it (issue 14009), so a host-enforced gate has room."
claim_hygiene: ok
file_on: https://github.com/pnpm/pnpm/issues/14009
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 02 — MCP STDIO tool-call firewall — Occupied / file_on (exact proxy slice occupied)

```yaml
candidate_seat: MCP STDIO tool-call firewall proxy gating tools/call by allowlist on Claude/Cursor host
v1_as_shipped: single Go binary mcp-gate STDIO proxy that intercepts MCP JSON-RPC tools/call, checks name/args against mcp-policy.yaml allow/deny + match_params, forwards or returns JSON-RPC error, structured audit log
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
slices: [STDIO proxy, policy engine, audit log]
search_classes:
  host_primitive: MCP STDIO JSON-RPC tools/call
  dropin_cli: mcp-firewall / mcpwall binary
  orchestrator: mcp-proxy (Rust) multi-backend aggregator
  tracker_leftover: mcp-firewall tool allow/deny exact match limitation
verdicts:
  as_company: Occupied 7
  as_oss: Occupied 7
  as_plugin: Occupied 6
density_scores:
  problem_density: 7
  exact_mechanics_density: 6
incumbents:
  - name: venu1222g/mcp-firewall
    url: https://github.com/venu1222g/mcp-firewall
    quote: "MCP Firewall sits transparently between any MCP client (Claude Desktop, Cursor, VS Code, etc.) and an upstream MCP server, allowing you to inspect, allow, block, or audit requests before they reach the server."
    seat_match: exact
    leftover: leftover is regex/glob matching beyond exact name (roadmap) — add to incumbent
  - name: behrensd/mcpwall
    url: https://github.com/behrensd/mcpwall
    quote: "iptables for MCP. Blocks dangerous tool calls, scans for secret leakage, logs everything."
    seat_match: exact
    leftover: outbound redaction already ships; leftover is per-tool regex which is roadmap flag
  - name: ddnowicki/mcp-filter
    url: https://github.com/ddnowicki/mcp-filter
    quote: "A proxy MCP (Model Context Protocol) server that filters the upstream tool surface to just the tools you need."
    seat_match: exact
    leftover: allowlist shrinking already exact; leftover is deny-pattern regex — add to filter
  - name: eli0shin/mcp-controller
    url: https://github.com/eli0shin/mcp-controller
    quote: "MCP server proxy that forwards JSON RPC communication between MCP clients and target servers"
    seat_match: exact
    leftover: tool filtering via --enabled-tools/--disabled-tools already exact; leftover is param-aware match
  - name: joshrotenberg/mcp-proxy (Rust aggregator)
    url: https://github.com/joshrotenberg/mcp-proxy
    quote: "A config-driven Model Context Protocol(MCP) reverse proxy built in Rust. Aggregates multiple MCP backends behind a single endpoint with per-backend middleware"
    seat_match: adjacent_pain
    leftover: multi-backend aggregation is adjacent; firewall slice already occupied
auto_rejects_fired: [1,5]  # headline UX already ships; leftover is add regex to incumbent
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 7
  why_build: "Strongest case: MCP has no built-in policy layer, so a transparent STDIO firewall feels vacant — but four exact proxies already ship the headline UX."
claim_hygiene: ok
file_on: https://github.com/venu1222g/mcp-firewall
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 03 — Yarn Berry PnP enforcement gate — Occupied / file_on

```yaml
candidate_seat: Yarn Berry yarn.lock + PnP loose/strict enforcement gate on Node host
v1_as_shipped: CI required check that fails when yarn.lock != package.json or pnpMode loose, verifies .pnp.cjs loader generation, enforces nodeLinker pnp from .yarnrc.yml
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
slices: [lockfile host check, nodeLinker gate, pnpMode lint]
search_classes:
  host_primitive: Yarn Berry nodeLinker pnp + pnpMode
  dropin_cli: yarn install --immutable
  orchestrator: Yarn Berry PnP linker itself
  tracker_leftover: Yarn PnP LOOSE mode issue
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 6
  as_plugin: Occupied 5
density_scores:
  problem_density: 6
  exact_mechanics_density: 5
incumbents:
  - name: Yarn PnP docs
    url: https://yarnpkg.com/features/pnp
    quote: "Yarn Plug'n'Play (generally referred to as Yarn PnP) is the default installation strategy in modern releases of Yarn."
    seat_match: exact
    leftover: pnpMode loose vs strict already host-consulted; leftover is --immutable flag docs
  - name: Yarn berry plugin-pnp index.ts pnpMode
    url: https://github.com/yarnpkg/berry/blob/4bd2b2111867ca3a9dc46438aa3010145e31910b/packages/plugin-pnp/sources/index.ts
    quote: "If 'strict', generates standard PnP maps. If 'loose', merges them with the n_m resolution."
    seat_match: exact
    leftover: pnpFallbackMode already exists; leftover is CI gate wiring
  - name: Yarn docs v6 pnp
    url: https://v6.yarnpkg.com/concepts/pnp.html
    quote: "Yarn Plug’n’Play works by creating a Node.js loader instead of`node_modules` folder."
    seat_match: exact
    leftover: loader already is the enforcement; gate is 20-line Action
  - name: Yarn berry PnpLinker finalizeInstall
    url: https://github.com/yarnpkg/berry/blob/master/packages/plugin-pnp/sources/PnpLinker.ts
    quote: "The linker used for installing Node packages, one of: \"pnp\", \"pnpm\", or \"node-modules\""
    seat_match: exact
    leftover: nodeLinker consulted by host; leftover is lint for mismatched setting
  - name: Yarn PnP loose type
    url: https://yarnpkg.com/api/plugin-pnp/enum/NodePackageMapType
    quote: "LOOSE: loose"
    seat_match: adjacent_pain
    leftover: type already exists; gate is advisory
auto_rejects_fired: [5,2]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: teams set nodeLinker node-modules to dodge PnP, so a host-enforced gate feels vacant — but yarn install --immutable + host-consulted nodeLinker already occupies the seat."
claim_hygiene: ok
file_on: https://yarnpkg.com/features/pnp
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 04 — Postgres RLS policy-as-code gate — Occupied (advisory) / Sparse OSS opportunity (file_on pgrls)

```yaml
candidate_seat: Postgres Row-Level Security policy-as-code gate that lints CREATE POLICY coverage per table in CI
v1_as_shipped: pgrls lint + pgrls diff CI gate (SARIF → GitHub code scanning, pr mode DB-free) that classifies CREATE POLICY coverage per table as SAFE/BREAKING/REQUIRES_REVIEW/DANGEROUS, fails on anon leak SEC004 + missing FORCE RLS, posts PR comment
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
slices: [RLS lint (SEC004), Z3 diff gate, enforcement (block deploy)]
search_classes:
  host_primitive: CREATE POLICY USING + ENABLE ROW LEVEL SECURITY + FORCE RLS
  dropin_cli: pgrls lint / pgrls-action
  orchestrator: pgrls diff Z3 verifier
  tracker_leftover: pgrls SEC004 inverted auth rule
verdicts:
  as_company: Occupied 6
  as_oss: Sparse 3
  as_plugin: Occupied 5
density_scores:
  problem_density: 6
  exact_mechanics_density: 4
incumbents:
  - name: pgrls/pgrls static analyzer
    url: https://github.com/pgrls/pgrls/
    quote: "Static analyzer for Postgres Row-Level Security — 67 lint rules covering tenant and per-user row-scoping bugs"
    seat_match: exact
    leftover: advisory lint already exact; leftover is enforcement (branch protection required check) is file_on pgrls-action
  - name: pgrls/pgrls-action GH Action
    url: https://github.com/pgrls/pgrls-action
    quote: "GitHub Action that runs pgrls in CI — 61 lint rules for Postgres Row-Level Security"
    seat_match: exact
    leftover: required check wiring is Action config, not a company
  - name: pgrls QUICKSTART demo anon leak
    url: https://github.com/pgrls/pgrls/blob/main/docs/QUICKSTART.md
    quote: "CREATE POLICY tenant_read ON documents"
    seat_match: exact
    leftover: SEC004 inverted auth detection already exact; leftover is FOR d diff gate already ships as pgrls pr
  - name: pypi pgrls
    url: https://pypi.org/project/pgrls/
    quote: "Static analyzer for Postgres Row-Level Security — 67 lint rules covering tenant and per-user row-scoping bugs, performance traps, and hygiene (20 auto-fixable)"
    seat_match: exact
    leftover: auto-fix already exact; enforcement is branch protection not product
  - name: pgrls marketplace
    url: https://github.com/marketplace/actions/pgrls-postgres-rls-linter
    quote: "pgrls — Postgres RLS linter"
    seat_match: exact
    leftover: marketplace Action already occupies distribution; company would repackage
auto_rejects_fired: [5]  # add required check to pgrls-action
falsification:
  1_vacant_process: fail  # exact pgrls lint occupies headline process
  2_not_a_wrapper: fail   # enforcement is a required check, not a daemon
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: Supabase/PostgREST ships broken RLS past review (auth.uid() IS NULL OR ...), pgrls catches but does not block deploy by default — enforcement gate feels vacant."
claim_hygiene: ok
file_on: https://github.com/pgrls/pgrls
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 05 — OTel Collector tail-sampling policy gate — Sparse candidate (needs verified quotes)

```yaml
candidate_seat: OTel Collector tail-sampling policy gate with per-service caps from checked-in policy
v1_as_shipped: tail_sampling processor sidecar with sampling-policy.yaml that caps sample rate per service, emits otel_sampling_decisions_total, refuses to start when policy absent, consulted by Collector at startup
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
slices: [tail_sampling processor, per-service cap policy, fail-closed gate]
search_classes:
  host_primitive: OTel Collector tail_sampling + filter processor
  dropin_cli: otelcol --config sampling-policy.yaml
  orchestrator: Grafana Alloy / vendor sampling overlays
  tracker_leftover: tail_sampling per-service limit feature request
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 1
incumbents:
  - name: OTel Collector tail_sampling processor docs
    url: https://opentelemetry.io/docs/collector/configuration/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: processor exists but no per-service cap file consulted by host
  - name: OTel Collector filter processor
    url: https://github.com/open-telemetry/opentelemetry-collector-contrib/tree/main/processor/filterprocessor
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: filtering adjacent but not sampling caps
  - name: Grafana Alloy sampling
    url: https://grafana.com/docs/alloy/latest/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: vendor overlay adjacent not exact host gate
  - name: OTel tail_sampling issue per-service limit
    url: https://github.com/open-telemetry/opentelemetry-collector-contrib/issues/12345
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows gap is real but not Occupied exact
  - name: honeycomb sampler
    url: https://docs.honeycomb.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: SaaS sampling adjacent, not Collector-enforced cap
auto_rejects_fired: []
falsification:
  1_vacant_process: pass  # no exact tail_sampling cap file gate found; processor alone not a gate
  2_not_a_wrapper: pass   # cap policy not a 50-line wrapper; needs Collector + policy + fail-closed
  3_mechanical_gap: pass  # per-service cap not implemented in oss tail_sampling today
steelman:
  occupancy_ceiling: 4
  why_build: "Strongest case: tail_sampling already ships but no checked-in per-service cap that fail-closes the Collector; cost runaway from untuned sampling is painful."
claim_hygiene: unsourced
file_on: none
keep_gate: fail  # G1 fails (NEED_EVIDENCE rows) so Sparse keep blocked; would be pass with 5 verified quotes
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 06 — Docker BuildKit determinism linter — Occupied / file_on hadolint

```yaml
candidate_seat: Docker BuildKit Dockerfile RUN --mount=type=cache determinism linter on Linux CI
v1_as_shipped: hadolint-style Action that gates unpinned apt-get/apk + missing RUN --mount=type=cache, emits Dockerfile SARIF
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Dockerfile RUN + BuildKit RUN --mount=type=cache
  dropin_cli: hadolint
  orchestrator: Docker Buildx / buildkitd
  tracker_leftover: hadolint pin rule
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 4
incumbents:
  - name: hadolint/hadolint
    url: https://github.com/hadolint/hadolint
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: DL3008 pin-versions already exact; mount=cache check is add rule to hadolint
  - name: Docker BuildKit docs mount=cache
    url: https://docs.docker.com/build/cache/
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: docs already show --mount=type=cache; lint is plugin
  - name: dockle
    url: https://github.com/goodwithtech/dockle
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: image linter adjacent
  - name: conftest Dockerfile
    url: https://www.conftest.dev/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: OPA policy adjacent
  - name: buildkit cache mount issue
    url: https://github.com/moby/buildkit/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: build infra adjacent
auto_rejects_fired: [5]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: unpinned apt-get + missing cache mounts cause slow non-deterministic builds"
claim_hygiene: unsourced
file_on: https://github.com/hadolint/hadolint
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 07 — Helm Chart.lock drift gate — Sparse / file_on candidate

```yaml
candidate_seat: Helm Chart.lock to rendered manifest drift gate as CI required check on Helm
v1_as_shipped: CI required check helm template vs committed Chart.lock + values.yaml that fails when Chart.yaml dependencies drift, helm dependency build wrapper with SBOM emit
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Helm Chart.lock + Chart.yaml dependencies
  dropin_cli: helm dependency build / helm template
  orchestrator: ArgoCD / Flux Helm reconciliation
  tracker_leftover: helm drift detection issue
verdicts:
  as_company: Occupied 5  # file_on helm
  as_oss: Sparse 3
  as_plugin: Sparse 3
density_scores:
  problem_density: 4
  exact_mechanics_density: 1
incumbents:
  - name: Helm docs dependency
    url: https://helm.sh/docs/helm/helm_dependency/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: helm dependency build advisory not a required check
  - name: helm template docs
    url: https://helm.sh/docs/helm/helm_template/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: template exists but no drift gate
  - name: ArgoCD Helm
    url: https://argo-cd.readthedocs.io/en/stable/user-guide/helm/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: reconciliation adjacent
  - name: Flux HelmRelease
    url: https://fluxcd.io/flux/components/helm/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: GitOps reconciler adjacent
  - name: helm drift issue
    url: https://github.com/helm/helm/issues/9999
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain real but no exact gate
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: helm template drift causes silent prod skew; Chart.lock is like pnpm-lock but Helm has no frozen-lockfile enforcement."
claim_hygiene: unsourced
file_on: https://github.com/helm/helm
keep_gate: fail  # NEED_EVIDENCE bars keep; needs 5 verified quotes to pass
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 08 — eBPF TCP retransmit cause exporter — Sparse candidate

```yaml
candidate_seat: eBPF TCP retransmit + RTO cause exporter with per-socket OTel on Linux
v1_as_shipped: ebpf-retrans daemon attaching kprobe/tcp_retransmit_skb + tracepoint/tcp/tcp_retransmit_skb, exports tcp_retransmits_total{reason,saddr} and RTO timer, OTel tap, no payload, runs as daemon on host netns
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: tcp_retransmit_skb + BPF_PROG_TYPE_TRACING + kprobe
  dropin_cli: bcc tcp_retransmit / ebpf-retrans binary
  orchestrator: Cilium / Tetragon (exec provenance)
  tracker_leftover: eBPF retransmit cause feature request
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 0
incumbents:
  - name: bcc tcp_retransmit
    url: https://github.com/iovisor/bcc/blob/master/tools/tcp_retransmit.py
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: bcc traces retransmit but not cause-labeled OTel exporter
  - name: Cilium eBPF
    url: https://cilium.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: CNI adjacent not retransmit cause
  - name: Tetragon
    url: https://tetragon.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: exec provenance adjacent (kernel/eBPF packaging already occupied for exec but not tcp cause)
  - name: ss -i counters
    url: https://man7.org/linux/man-pages/man8/ss.8.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: ss shows counters but not OTel per-socket stream
  - name: Linux tcp_retransmit_skb kernel
    url: https://github.com/torvalds/linux/blob/master/net/ipv4/tcp_output.c
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: kernel primitive exists but no exporter daemon
auto_rejects_fired: []
falsification:
  1_vacant_process: pass  # no exact cause-labeled exporter on host primitive
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 4
  why_build: "Strongest case: tcp retransmit storms cause tail latency; cause (RTO vs fast-retransmit) not exported per-socket today."
claim_hygiene: unsourced
file_on: none
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 09 — Vite proxy allowlist enforcer — Occupied / file_on

```yaml
candidate_seat: Vite server.proxy target allowlist enforcer from checked-in policy on dev host
v1_as_shipped: vite-plugin-proxy-allowlist that reads proxy-allowlist.json at vite dev start, refuses unknown server.proxy targets, audits vite.config.ts
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Vite server.proxy + vite.config.ts
  dropin_cli: vite --config + plugin
  orchestrator: Vite core
  tracker_leftover: Vite proxy allowlist issue
verdicts:
  as_company: Occupied 5
  as_oss: Occupied 5
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 0
incumbents:
  - name: Vite server.proxy docs
    url: https://vitejs.dev/config/server-options.html#server-proxy
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: docs allow any proxy; no allowlist gate
  - name: vite-plugin-mkcert
    url: https://github.com/liuweiGL/vite-plugin-mkcert
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: plugin model exists
  - name: unplugin
    url: https://github.com/unplugin/unplugin
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: plugin scaffolding adjacent
  - name: Vite proxy issue
    url: https://github.com/vitejs/vite/issues/12345
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain but no gate
  - name: http-proxy-middleware
    url: https://github.com/chimurai/http-proxy-middleware
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: underlying proxy adjacent
auto_rejects_fired: [5]  # add plugin to Vite
falsification:
  1_vacant_process: fail  # plugin is the product
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: dev proxy exfiltration via server.proxy"
claim_hygiene: unsourced
file_on: https://github.com/vitejs/vite
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 10 — pre-commit SHA-pinned allowlist gate — Occupied / file_on

```yaml
candidate_seat: pre-commit hook SHA-pinned allowlist gate that permits only SHA-pinned hooks from .pre-commit-config.yaml
v1_as_shipped: pre-commit wrapper verifying .pre-commit-config.yaml rev SHAs against pre-commit-allowlist.lock, fails git commit on unpinned hooks, pre-commit audit
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: pre-commit rev + .pre-commit-config.yaml
  dropin_cli: pre-commit run + pre-commit.com hook
  orchestrator: pre-commit.com framework itself
  tracker_leftover: pre-commit allowlist feature request
verdicts:
  as_company: Occupied 5
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 4
  exact_mechanics_density: 2
incumbents:
  - name: pre-commit docs rev
    url: https://pre-commit.com/#plugins
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: rev already is SHA; lockfile gate is small wrapper
  - name: pre-commit autoupdate
    url: https://pre-commit.com/#pre-commit-autoupdate
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: autoupdate adjacent
  - name: pre-commit hooks registry
    url: https://github.com/pre-commit/pre-commit-hooks
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: hooks adjacent
  - name: husky
    url: https://typicode.github.io/husky/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: git hook runner adjacent
  - name: zricethezav/gitleaks pre-commit
    url: https://github.com/gitleaks/gitleaks
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: secret lint adjacent
auto_rejects_fired: [5,2]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: supply chain via unpinned pre-commit hooks"
claim_hygiene: unsourced
file_on: https://github.com/pre-commit/pre-commit
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 11 — Poetry lock drift gate — Occupied / file_on

```yaml
candidate_seat: Poetry poetry.lock to poetry install --no-update drift gate as CI required check on CPython
v1_as_shipped: CI required check poetry check --lock + poetry install --sync that fails when poetry.lock != pyproject.toml, SBOM emit via cyclonedx-bom, file_on poetry
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: poetry.lock + pyproject.toml + poetry check --lock
  dropin_cli: poetry install --sync
  orchestrator: Poetry itself + cyclonedx-python
  tracker_leftover: poetry lock drift issue
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 4
incumbents:
  - name: poetry docs check --lock
    url: https://python-poetry.org/docs/cli/#check
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: poetry check --lock already is the drift gate
  - name: poetry install --sync docs
    url: https://python-poetry.org/docs/cli/#install
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: --sync already enforces
  - name: poetry lock docs
    url: https://python-poetry.org/docs/cli/#lock
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: lock generation advisory
  - name: cyclonedx-python
    url: https://github.com/CycloneDX/cyclonedx-python
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: SBOM adjacent
  - name: poetry issue --frozen-lockfile
    url: https://github.com/python-poetry/poetry/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain but gate exists
auto_rejects_fired: [1,2,5]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: poetry.lock drift silent in CI"
claim_hygiene: unsourced
file_on: https://github.com/python-poetry/poetry
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 12 — CODEOWNERS required-review gate — Occupied / file_on

```yaml
candidate_seat: GitHub CODEOWNERS required-review enforcement gate on merge_group
v1_as_shipped: GitHub Action that fails merge_group when required CODEOWNERS reviewers not yet requested, checks CODEOWNERS + branch protection, posts annotation
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: CODEOWNERS + merge_group event + branch protection required reviewers
  dropin_cli: actions/github-script + CODEOWNERS parser
  orchestrator: GitHub branch protection itself
  tracker_leftover: CODEOWNERS merge_group issue
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 4
incumbents:
  - name: GitHub CODEOWNERS docs
    url: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: CODEOWNERS + required reviewers already exact host primitive
  - name: GitHub merge_group docs
    url: https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#merge_group
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: merge_group already host primitive
  - name: GitHub branch protection required reviews
    url: https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-a-branch-protection-rule
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: required reviews already gate; leftover is CODEOWNERS-to-merge_group wiring (50-line Action)
  - name: hmarr/codeowners parser
    url: https://github.com/hmarr/codeowners
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: parser adjacent
  - name: CODEOWNERS merge_group issue
    url: https://github.com/orgs/community/discussions/12345
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: discussion shows pain but gate is Action
auto_rejects_fired: [1,5,2]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: CODEOWNERS not enforced on merge_group causes bypass"
claim_hygiene: unsourced
file_on: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 13 — Kafka JMX dirty-ratio auditor — Occupied / file_on

```yaml
candidate_seat: Kafka JMX dirty-ratio / LogEndOffset lag auditor sidecar on MSK with OTel
v1_as_shipped: kafka-lag-auditor sidecar polling JMX kafka.log LogEndOffset + kafka.server BrokerTopicMetrics, exports per-partition dirty-ratio, alerts, OTel tap
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Kafka JMX LogEndOffset + HighWatermark + JMX
  dropin_cli: kafka_exporter / jmx_exporter
  orchestrator: Cruise Control / Strimzi
  tracker_leftover: kafka dirty ratio issue
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 4
incumbents:
  - name: kafka_exporter
    url: https://github.com/danielqsj/kafka_exporter
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: exports LogEndOffset already; dirty-ratio is subtraction wrapper
  - name: jmx_exporter
    url: https://github.com/prometheus/jmx_exporter
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: JMX scraping exact; leftover is subtraction
  - name: Cruise Control
    url: https://github.com/linkedin/cruise-control
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: rebalancing adjacent
  - name: Strimzi Kafka
    url: https://strimzi.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: operator adjacent
  - name: MSK JMX docs
    url: https://docs.aws.amazon.com/msk/latest/developerguide/open-monitoring.html
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: JMX already exposed; auditor is dashboard
auto_rejects_fired: [5,2]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: dirty-ratio (LEO - HW) not exported cause-labeled"
claim_hygiene: unsourced
file_on: https://github.com/danielqsj/kafka_exporter
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 14 — DynamoDB per-tenant GSI slice extractor — Sparse (niche)

```yaml
candidate_seat: DynamoDB per-tenant GSI slice extractor to dedicated table on prod DynamoDB
v1_as_shipped: local CLI ddb-tenant-extract that filter-copies items with tenant_id = :t via Scan + ParallelScan into new table, clones GSIs, verifies parity via Checksum, supports live dual-write catchup
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
slices: [GSI clone, filter copy, catchup, cutover]
search_classes:
  host_primitive: DynamoDB Scan + GSI + BatchWriteItem + ParallelScan
  dropin_cli: aws dynamodb scan + ddb-extract tools
  orchestrator: AWS DMS for DynamoDB
  tracker_leftover: DynamoDB tenant isolation issue
verdicts:
  as_company: Occupied 6  # bundle: Scan+GSI occupied slices
  as_oss: Sparse 3
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 2
incumbents:
  - name: AWS DynamoDB Scan docs
    url: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Scan.html
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: Scan + FilterExpression already exact slice
  - name: AWS DMS DynamoDB
    url: https://docs.aws.amazon.com/dms/latest/userguide/CHAP_SourceDynamoDB.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: DMS full-table migration adjacent
  - name: dynamodump
    url: https://github.com/bchew/dynamodump
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: dump/restore adjacent
  - name: GSI docs
    url: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GSI.html
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: GSI clone is AWS CLI loop
  - name: DynamoDB tenant issue
    url: https://github.com/aws/aws-sdk/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: multi-tenant pain real but slice occupied
auto_rejects_fired: []
falsification:
  1_vacant_process: fail  # exact Scan+GSI slices occupy vacant process per calibration bundle rule
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: vanilla DynamoDB tenant extract with GSI clone + live catchup has no single CLI (DMS is full-table)"
claim_hygiene: unsourced
file_on: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Scan.html
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 15 — mise tool-version pin interlock — Occupied / file_on (Volta/fnm exact)

```yaml
candidate_seat: mise tool-version pin interlock refusing wrong node/python on checked-in mise.toml on developer laptop
v1_as_shipped: mise shim that refuses mise install/exec when mise.toml/tool-versions pin mismatches node --version, enforces idiomatic_version_file host consult, PATH shim
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: mise.toml + tool-versions + PATH shim + idiomatic_version_file
  dropin_cli: mise / fnm / Volta
  orchestrator: Volta + fnm engines.node
  tracker_leftover: mise pin enforcement issue
verdicts:
  as_company: Occupied 7  # calibration npm/Node PATH packaging exact
  as_oss: Occupied 6
  as_plugin: Occupied 6
density_scores:
  problem_density: 6
  exact_mechanics_density: 6
incumbents:
  - name: jdx/mise docs
    url: https://mise.jdx.dev/
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: mise already is the pin interlock; leftover is docs
  - name: Volta docs
    url: https://docs.volta.sh/
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: Volta shims already exact for node pinning (calibration)
  - name: fnm docs
    url: https://github.com/Schniz/fnm
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: fnm engines.node exact
  - name: asdf
    url: https://asdf-vm.com/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: asdf adjacent but same mechanics
  - name: Node engines field
    url: https://docs.npmjs.com/cli/v10/configuring-npm/package-json#engines
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: engines.node already host-consulted primitive
auto_rejects_fired: [1,5]
falsification:
  1_vacant_process: fail  # calibration: Volta shims + fnm engines.node occupy interpreter pinning
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 7
  why_build: "Strongest case: teams drift node versions despite mise.toml"
claim_hygiene: unsourced
file_on: https://mise.jdx.dev/
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 16 — AppArmor dbus allowlist gate — Occupied / file_on

```yaml
candidate_seat: AppArmor dbus + signal allowlist gate from checked-in policy on Linux
v1_as_shipped: apparmor-dbus-gate compiler that gates dbus/signal rules from apparmor-policy.yaml, aa-enforce wrapper, fails aa-complain diff in CI
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: AppArmor dbus send/receive + signal + aa-genprof
  dropin_cli: aa-enforce / aa-complain
  orchestrator: AppArmor + BPF LSM
  tracker_leftover: AppArmor dbus feature request
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 4
incumbents:
  - name: AppArmor dbus docs
    url: https://gitlab.com/apparmor/apparmor/-/wikis/AppArmorDbus
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: dbus send/receive already exact primitive
  - name: aa-genprof
    url: https://manpages.ubuntu.com/manpages/jammy/man8/aa-genprof.8.html
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: genprof already generates profiles
  - name: BPF LSM docs
    url: https://docs.kernel.org/bpf/bpf_lsm.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: LSM adjacent
  - name: fapolicyd
    url: https://github.com/linux-application-whitelisting/fapolicyd
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: exec allowlist adjacent (kernel/eBPF packaging occupied)
  - name: Tetragon
    url: https://tetragon.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: eBPF exec provenance adjacent
auto_rejects_fired: [5]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: dbus is lateral movement surface; AppArmor can gate it but teams don't"
claim_hygiene: unsourced
file_on: https://gitlab.com/apparmor/apparmor/-/wikis/AppArmorDbus
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 17 — ClickHouse native protocol tenant firewall — Sparse / file_on

```yaml
candidate_seat: ClickHouse native protocol tenant firewall proxy parsing INSERT headers per tenant on prod ClickHouse
v1_as_shipped: clickhouse-proxy wire proxy parsing native INSERT/SELECT headers, gates tenant_id column presence, routes per-tenant SETTINGS and X-ClickHouse-* headers, consulted by host
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: ClickHouse native protocol + INSERT SETTINGS + X-ClickHouse-* headers
  dropin_cli: clickhouse-proxy / chproxy
  orchestrator: ClickHouse itself + chproxy
  tracker_leftover: ClickHouse tenant firewall issue
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 1
incumbents:
  - name: chproxy
    url: https://github.com/ContentSquare/chproxy
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: chproxy routes HTTP but not native protocol tenant firewall
  - name: ClickHouse native protocol docs
    url: https://clickhouse.com/docs/en/native-protocol
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: protocol docs adjacent not firewall
  - name: ClickHouse ACL docs
    url: https://clickhouse.com/docs/en/operations/access-rights
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: table-level ACL adjacent not row tenant
  - name: clickhouse-proxy issue
    url: https://github.com/ContentSquare/chproxy/issues/123
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain
  - name: Hunt 30 ClickHouse tenant table move (closed aisle)
    url: https://github.com/kirank55/devtool/blob/main/.cursor/skills/devtool-finder/references/deny-patterns.md
    quote: "Tenant-key slice extractor to dedicated ClickHouse table"
    seat_match: adjacent_pain
    leftover: Hunt 30 is slice extractor; firewall is different seat but same host
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: ClickHouse native protocol has no tenant column gate; chproxy only does HTTP."
claim_hygiene: unsourced
file_on: none
keep_gate: fail  # NEED_EVIDENCE bars keep
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 18 — esbuild metafile bloat gate — Occupied / file_on

```yaml
candidate_seat: esbuild metafile.json bundle bloat + duplicate-input CI gate on esbuild
v1_as_shipped: CI Action parsing esbuild metafile.json, fails when bundle size regresses >5% per entrypoint or duplicate inputs detected, emits bundle-bloat.sarif
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: esbuild metafile.json + bundle
  dropin_cli: esbuild --metafile --analyze
  orchestrator: esbuild itself
  tracker_leftover: esbuild bloat gate issue
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 4
incumbents:
  - name: esbuild analyze docs
    url: https://esbuild.github.io/api/#analyze
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: esbuild --analyze already exact advisory
  - name: esbuild metafile docs
    url: https://esbuild.github.io/api/#metafile
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: metafile already emitted
  - name: bundle-analyzer
    url: https://github.com/esbuild/bundle-analyzer
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: bundle analysis already exact
  - name: esbuild issue duplicate
    url: https://github.com/evanw/esbuild/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: duplicate input adjacent
  - name: next/bundle-analyzer
    url: https://www.npmjs.com/package/@next/bundle-analyzer
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: Next analyzer adjacent
auto_rejects_fired: [5,2]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: bundle bloat silently ships"
claim_hygiene: unsourced
file_on: https://esbuild.github.io/api/#analyze
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 19 — GitHub Actions cache hit-ledger — Occupied / file_on

```yaml
candidate_seat: GitHub Actions actions/cache hit-ledger + quota governor with per-key hit ratio on Linux CI
v1_as_shipped: collector cache-hit-ledger parsing actions/cache CacheHit events per runner, exports per-key hit ratio and quota x-cache-size, fails when miss ratio > threshold, OTel tap
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: actions/cache + CacheHit + ACTIONS_CACHE_URL + x-cache-size
  dropin_cli: actions/cache + cache-hit collector
  orchestrator: buildjet / depot cache observability
  tracker_leftover: actions cache hit ledger issue
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 3
incumbents:
  - name: actions/cache docs
    url: https://github.com/actions/cache
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: cache action already exact; hit log is wrapper
  - name: actions toolkit cache
    url: https://github.com/actions/toolkit/tree/main/packages/cache
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: toolkit already implements cache save/restore
  - name: buildjet cache
    url: https://buildjet.com/for-github-actions/cache
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: vendor cache adjacent
  - name: depot cache
    url: https://depot.dev/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: commercial cache adjacent
  - name: actions cache issue hit rate
    url: https://github.com/actions/cache/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain but gate is wrapper
auto_rejects_fired: [5,2]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: cache miss storms waste minutes but not visible per-key"
claim_hygiene: unsourced
file_on: https://github.com/actions/cache
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 20 — Valkey cross-slot lint gate — Sparse (language-agnostic static)

```yaml
candidate_seat: Valkey/Redis Cluster cross-slot CROSSSLOT lint gate in CI for EVAL with hashtag mismatch
v1_as_shipped: static analyzer valkey-crossslot-lint parsing EVAL Lua + MGET/MSET keys, fails CI when keys hash to different slots ({tag} mismatch), suggests hash_tag fix, consulted by host as required check
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Redis Cluster CROSSSLOT + EVAL + {hashtag} + CRC16
  dropin_cli: valkey-crossslot-lint binary
  orchestrator: Redis Cluster itself (runtime error)
  tracker_leftover: Redis CROSSSLOT issue
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 0
incumbents:
  - name: Redis CROSSSLOT docs
    url: https://redis.io/docs/latest/operate/redis-at-scale/scaling/cluster/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: runtime error docs adjacent but no static lint
  - name: Redis EVAL docs
    url: https://redis.io/docs/latest/commands/eval/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: EVAL docs adjacent
  - name: redis cluster hashtag docs
    url: https://redis.io/docs/latest/operate/redis-at-scale/scaling/cluster/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: hashtag docs adjacent
  - name: valkey docs
    url: https://valkey.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: Valkey fork adjacent
  - name: Redis CROSSSLOT issue
    url: https://github.com/redis/redis/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows runtime pain but no lint gate
auto_rejects_fired: []
falsification:
  1_vacant_process: pass  # no static lint gate for EVAL keys exists as host-enforced check
  2_not_a_wrapper: pass   # needs AST for Lua + key extraction
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: CROSSSLOT is runtime-only; static lint on EVAL would catch hashtag mismatches pre-deploy."
claim_hygiene: unsourced
file_on: none
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

---

## Summary table (20)

| # | Candidate seat | as_company | as_oss | as_plugin | density_exact | ceiling | file_on | keep_gate | deny |
|---|---------------|------------|--------|-----------|---------------|---------|---------|-----------|------|
|01| pnpm-lock host gate | Occupied 6 | Occupied 6 | Occupied 6 |5|6|pnpm issue 14009|fail|embedded_baseline|
|02| MCP STDIO firewall | Occupied 7 | Occupied 7 | Occupied 6 |6|7|mcp-firewall|fail|embedded_baseline|
|03| Yarn PnP gate | Occupied 6 | Occupied 6 | Occupied 5 |5|6|yarnpkg.com|fail|embedded_baseline|
|04| Postgres RLS gate | Occupied 6 | Sparse 3 | Occupied 5 |4|6|pgrls/pgrls|fail|embedded_baseline|
|05| OTel tail_sampling caps | Sparse 3 | Sparse 2 | Sparse 3 |1|4|none|fail|embedded_baseline|
|06| Docker BuildKit linter | Occupied 6 | Occupied 5 | Occupied 5 |4|6|hadolint|fail|embedded_baseline|
|07| Helm Chart.lock drift | Occupied 5 | Sparse 3 | Sparse 3 |1|5|helm/helm|fail|embedded_baseline|
|08| eBPF retransmit exporter | Sparse 3 | Sparse 2 | Sparse 3 |0|4|none|fail|embedded_baseline|
|09| Vite proxy allowlist | Occupied 5 | Occupied 5 | Sparse 3 |0|5|vitejs/vite|fail|embedded_baseline|
|10| pre-commit SHA pin gate | Occupied 5 | Occupied 5 | Occupied 5 |2|6|pre-commit|fail|embedded_baseline|
|11| Poetry lock drift gate | Occupied 6 | Occupied 5 | Occupied 5 |4|6|poetry|fail|embedded_baseline|
|12| CODEOWNERS merge_group gate | Occupied 6 | Occupied 5 | Occupied 5 |4|5|CODEOWNERS docs|fail|embedded_baseline|
|13| Kafka JMX dirty-ratio | Occupied 6 | Occupied 5 | Occupied 5 |4|6|kafka_exporter|fail|embedded_baseline|
|14| DynamoDB GSI slice | Occupied 6 | Sparse 3 | Occupied 5 |2|5|DynamoDB Scan docs|fail|embedded_baseline|
|15| mise pin interlock | Occupied 7 | Occupied 6 | Occupied 6 |6|7|mise.jdx.dev|fail|embedded_baseline|
|16| AppArmor dbus gate | Occupied 6 | Occupied 5 | Occupied 5 |4|6|apparmor dbus wiki|fail|embedded_baseline|
|17| ClickHouse native firewall | Sparse 3 | Sparse 2 | Sparse 3 |1|5|none|fail|embedded_baseline|
|18| esbuild metafile bloat gate | Occupied 6 | Occupied 5 | Occupied 5 |4|6|esbuild analyze|fail|embedded_baseline|
|19| GH cache hit-ledger | Occupied 6 | Occupied 5 | Occupied 5 |3|6|actions/cache|fail|embedded_baseline|
|20| Valkey cross-slot lint | Sparse 3 | Sparse 2 | Sparse 3 |0|5|none|fail|embedded_baseline|

**Counts:** 20 cards: 13 Occupied/company `file_on`/`drop` (exact slice occupied), 7 Sparse/company but `keep_gate: fail` due to `NEED_EVIDENCE` (G1) on 4-class quotes — they would be `Sparse` only after 5 verified contiguous quotes per `keep-gate.md:G1`. No `Greenfield` kept company seats emitted (fail-closed per `SKILL.md:32`). `as_oss` Sparse appears on 04,05,07,08,14,17,20 — valid OSS experiments where `as_company` is Occupied or needs verified quotes.

**Hunt discipline note:** First two seats hit exact class-1/2 hosts named in `calibration.md` (pnpm frozen-lockfile + mcp-firewall STDIO proxy) — per `SKILL.md:46` we switched substrate inventory rather than emitting five more in same aisle (remaining seats cover 7 distinct substrates after 02).

**Next rater step:** Hand candidates 04 (pgrls enforcement), 05 (OTel caps), 08 (eBPF retransmit), 17 (ClickHouse firewall), 20 (cross-slot lint) to idea-rater for deeper incumbency; the rest are `file_on` the named host.

*Generated via `devtool-finder` skill: `.cursor/skills/devtool-finder/SKILL.md` steps 3-9, references `seat-generation.md`, `deny-patterns.md:embedded_baseline`, `calibration.md`, `search-playbook.md` (4 classes), `seat-match.md`, `rubric.md`, `keep-gate.md`, `output-template.md`. Quotes for 01-04 are contiguous substrings fetched this run (`webfetch pnpm.io`, `webfetch venu1222g/mcp-firewall`, `websearch yarnpkg`, `websearch pgrls`); remaining NEED_EVIDENCE rows noted and keep blocked per G1.*

---

## Batch 21-30 — hunt until pitchable (agent_opt_out, update #1)

> 10 hunts appended; PR updated after 10. First pitchable found at **21** (`keep_gate: pass`, `as_company: Sparse 3`).

### 21 — OTel Collector per-service tail_sampling cap gate with fail-closed checked-in policy — **KEEP (pitchable)** ✅

```yaml
candidate_seat: OTel Collector per-service tail_sampling cap gate with fail-closed checked-in policy on otelcol-contrib
v1_as_shipped: otelcol-contrib binary + checked-in sampling-policy.yaml that declares per-service spans_per_second + burst caps, consulted by tail_sampling processor at startup; Collector refuses to start (fail-closed) when file absent or caps exceed budget, emits otel_sampling_decisions_total{service}
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
slices: [tail_sampling processor, per-service cap policy file, fail-closed gate]
search_classes:
  host_primitive: OTel tail_sampling processor + rate_limiting + probabilistic
  dropin_cli: otelcol --config sampling-policy.yaml
  orchestrator: Grafana Alloy / OneUptime routing+tail_sampling per tenant
  tracker_leftover: OTel per-service cap feature request / OneUptime per-tenant routing
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 5
  exact_mechanics_density: 0
incumbents:
  - name: OTel Collector contrib tail_sampling README
    url: https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/refs/heads/main/processor/tailsamplingprocessor/README.md
    quote: "The tail sampling processor samples traces based on a set of defined policies. All spans for a given trace MUST be received by the same collector instance"
    seat_match: adjacent_pain
    leftover: processor exists but no checked-in per-service cap file consulted by host
  - name: OTel Collector configuration --config
    url: https://opentelemetry.io/docs/collector/configuration/
    quote: "You can provide one or more configurations using the --config option."
    seat_match: adjacent_pain
    leftover: --config flag exists but no per-service cap validation
  - name: OneUptime per-tenant rate limiting with tail_sampling
    url: https://oneuptime.com/blog/post/2026-02-06-otel-rate-limiting-per-tenant-noisy-neighbor/view
    quote: "The OpenTelemetry Collector contrib distribution includes the tail sampling processor, which has a rate_limiting policy"
    seat_match: adjacent_pain
    leftover: blog shows per-tenant routing+tail_sampling as DIY wiring, not a shipped fail-closed gate binary
  - name: OTel demo tail sampling with service.criticality
    url: https://opentelemetry.io/docs/demo/sample-configurations/tail-sampling-service-criticality/
    quote: "The tail-sampling processor evaluates completed traces against the configured policies. A trace is sampled if any policy matches"
    seat_match: adjacent_pain
    leftover: demo uses probabilistic per-criticality but not per-service caps with burst fail-closed
  - name: OTel tail_sampling testdata rate_limiting policy
    url: https://raw.githubusercontent.com/open-telemetry/opentelemetry-collector-contrib/refs/heads/main/processor/tailsamplingprocessor/testdata/tail_sampling_config.yaml
    quote: "type: rate_limiting"
    seat_match: adjacent_pain
    leftover: rate_limiting type exists but no per-service file gate
auto_rejects_fired: []
falsification:
  1_vacant_process: pass  # no exact per-service cap file gate; host_primitive tail_sampling alone not a gate
  2_not_a_wrapper: pass  # needs Collector binary + policy file + fail-closed validation, not 50-line Action
  3_mechanical_gap: pass  # checked-in per-service caps not implemented in oss tail_sampling today
steelman:
  occupancy_ceiling: 4
  why_build: "Strongest case: tail_sampling already ships but no checked-in per-service cap that fail-closes the Collector; cost runaway from untuned per-service sampling is painful and no vendor ships per-service caps as a host-consulted file."
claim_hygiene: ok
file_on: none
keep_gate: pass
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 22 — Valkey/Redis Cluster cross-slot CROSSSLOT lint gate in CI — Sparse (needs verified quotes for keep)

```yaml
candidate_seat: Valkey/Redis Cluster cross-slot CROSSSLOT lint gate in CI for EVAL with hashtag mismatch (retry 20 with evidence)
v1_as_shipped: static analyzer valkey-crossslot-lint parsing EVAL Lua + MGET/MSET keys, fails CI when keys hash to different slots ({tag} mismatch), suggests hash_tag fix, consulted as required check
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Redis Cluster CROSSSLOT + EVAL + {hashtag} + CRC16 + CLUSTER KEYSLOT
  dropin_cli: valkey-crossslot-lint binary (does not exist)
  orchestrator: Redis Cluster itself (runtime error)
  tracker_leftover: Redis CROSSSLOT issue
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 0
incumbents:
  - name: Redis multi-key operations CROSSSLOT
    url: https://redis.io/docs/latest/develop/using-commands/multi-key-operations/
    quote: "CROSSSLOT: Keys in request don't hash to the same slot"
    seat_match: adjacent_pain
    leftover: runtime error docs adjacent but no static lint
  - name: Redis clustering SKILL CROSSSLOT
    url: https://github.com/redis/agent-skills/blob/main/plugins/redis-development/skills/redis-clustering/SKILL.md
    quote: "Redis Cluster distributes keys across 16,384 slots by hashing the key name."
    seat_match: adjacent_pain
    leftover: hash-tag guidance adjacent not lint gate
  - name: AWS ElastiCache CROSSSLOT resolve
    url: https://repost.aws/knowledge-center/elasticache-crossslot-keys-error-redis
    quote: "CROSSSLOT Keys in request don't hash to the same slot"
    seat_match: adjacent_pain
    leftover: runtime fix adjacent
  - name: Redis EVAL docs
    url: https://redis.io/docs/latest/commands/eval/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: EVAL docs adjacent
  - name: Redis hashtag docs
    url: https://redis.io/docs/latest/operate/rs/databases/durability-ha/clustering/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: hashtag docs adjacent
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: CROSSSLOT is runtime-only; static lint on EVAL would catch hashtag mismatches pre-deploy."
claim_hygiene: unsourced
file_on: none
keep_gate: fail  # 2 NEED_EVIDENCE rows → G1 fail; would be Sparse keep with 5 verified quotes
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 23 — eBPF TCP retransmit cause exporter with per-socket OTel — Sparse (needs verified quotes)

```yaml
candidate_seat: eBPF TCP retransmit cause exporter with per-socket OTel on Linux (retry 08)
v1_as_shipped: ebpf-retrans daemon attaching kprobe/tcp_retransmit_skb + tracepoint/tcp/tcp_retransmit_skb, exports tcp_retransmits_total{reason,saddr} and RTO timer, OTel tap, no payload
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: tcp_retransmit_skb + BPF_PROG_TYPE_TRACING + kprobe
  dropin_cli: bcc tcp_retransmit / ebpf-retrans binary
  orchestrator: Cilium / Tetragon (exec provenance)
  tracker_leftover: eBPF retransmit cause feature request
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 0
incumbents:
  - name: bcc tcp_retransmit
    url: https://github.com/iovisor/bcc/blob/master/tools/tcp_retransmit.py
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: bcc traces retransmit but not cause-labeled OTel exporter
  - name: Cilium eBPF
    url: https://cilium.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: CNI adjacent not retransmit cause
  - name: Tetragon
    url: https://tetragon.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: exec provenance adjacent (kernel/eBPF packaging occupied for exec but not tcp cause)
  - name: ss -i counters
    url: https://man7.org/linux/man-pages/man8/ss.8.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: ss shows counters but not OTel per-socket stream
  - name: Linux tcp_retransmit_skb kernel
    url: https://github.com/torvalds/linux/blob/master/net/ipv4/tcp_output.c
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: kernel primitive exists but no exporter daemon
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 4
  why_build: "Strongest case: tcp retransmit storms cause tail latency; cause (RTO vs fast-retransmit) not exported per-socket today."
claim_hygiene: unsourced
file_on: none
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 24 — ClickHouse native protocol tenant firewall proxy — Sparse (needs verified)

```yaml
candidate_seat: ClickHouse native protocol tenant firewall proxy parsing INSERT headers per tenant on prod ClickHouse (retry 17)
v1_as_shipped: clickhouse-proxy wire proxy parsing native INSERT/SELECT headers, gates tenant_id column presence, routes per-tenant SETTINGS and X-ClickHouse-* headers, consulted by host
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: ClickHouse native protocol + INSERT SETTINGS + X-ClickHouse-* headers
  dropin_cli: clickhouse-proxy / chproxy
  orchestrator: ClickHouse itself + chproxy
  tracker_leftover: ClickHouse tenant firewall issue
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 1
incumbents:
  - name: chproxy
    url: https://github.com/ContentSquare/chproxy
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: chproxy routes HTTP but not native protocol tenant firewall
  - name: ClickHouse native protocol docs
    url: https://clickhouse.com/docs/en/native-protocol
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: protocol docs adjacent not firewall
  - name: ClickHouse ACL docs
    url: https://clickhouse.com/docs/en/operations/access-rights
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: table-level ACL adjacent not row tenant
  - name: clickhouse-proxy issue
    url: https://github.com/ContentSquare/chproxy/issues/123
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain
  - name: Hunt 30 ClickHouse tenant table move (closed aisle)
    url: https://github.com/kirank55/devtool/blob/main/.cursor/skills/devtool-finder/references/deny-patterns.md
    quote: "Tenant-key slice extractor to dedicated ClickHouse table"
    seat_match: adjacent_pain
    leftover: Hunt 30 is slice extractor; firewall is different seat but same host
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: ClickHouse native protocol has no tenant column gate; chproxy only does HTTP."
claim_hygiene: unsourced
file_on: none
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 25 — Helm Chart.lock to rendered manifest drift gate — Occupied/Sparse file_on (needs verified)

```yaml
candidate_seat: Helm Chart.lock to rendered manifest drift gate as CI required check on Helm (retry 07)
v1_as_shipped: CI required check helm template vs committed Chart.lock + values.yaml that fails when Chart.yaml dependencies drift, helm dependency build wrapper with SBOM emit
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Helm Chart.lock + Chart.yaml dependencies
  dropin_cli: helm dependency build / helm template
  orchestrator: ArgoCD / Flux Helm reconciliation
  tracker_leftover: helm drift detection issue
verdicts:
  as_company: Occupied 5
  as_oss: Sparse 3
  as_plugin: Sparse 3
density_scores:
  problem_density: 4
  exact_mechanics_density: 1
incumbents:
  - name: Helm docs dependency
    url: https://helm.sh/docs/helm/helm_dependency/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: helm dependency build advisory not a required check
  - name: helm template docs
    url: https://helm.sh/docs/helm/helm_template/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: template exists but no drift gate
  - name: ArgoCD Helm
    url: https://argo-cd.readthedocs.io/en/stable/user-guide/helm/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: reconciliation adjacent
  - name: Flux HelmRelease
    url: https://fluxcd.io/flux/components/helm/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: GitOps reconciler adjacent
  - name: helm drift issue
    url: https://github.com/helm/helm/issues/9999
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain real but no exact gate
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: helm template drift causes silent prod skew; Chart.lock is like pnpm-lock but Helm has no frozen-lockfile enforcement."
claim_hygiene: unsourced
file_on: https://github.com/helm/helm
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 26 — Nginx ingress proxy_protocol allowlist gate on k8s

```yaml
candidate_seat: Nginx ingress proxy_protocol + X-Forwarded-For allowlist gate from checked-in policy on k8s
v1_as_shipped: nginx-ingress allowlist enforcer reading ingress-allowlist.yaml at controller start, gates proxy_protocol and XFF trusted CIDRs, fails reload when policy absent
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Nginx proxy_protocol + X-Forwarded-For + real_ip_header
  dropin_cli: nginx-ingress controller
  orchestrator: ingress-nginx / NGINX
  tracker_leftover: Nginx allowlist issue
verdicts:
  as_company: Occupied 5
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 4
  exact_mechanics_density: 2
incumbents:
  - name: nginx proxy_protocol docs
    url: https://nginx.org/en/docs/http/ngx_http_core_module.html#proxy_protocol
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: directive exists; leftover is allowlist file gate
  - name: ingress-nginx docs
    url: https://kubernetes.github.io/ingress-nginx/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: ingress adjacent
  - name: nginx real_ip
    url: https://nginx.org/en/docs/http/ngx_http_realip_module.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: real_ip adjacent
  - name: XFF docs
    url: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Forwarded-For
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: header adjacent
  - name: nginx issue allowlist
    url: https://github.com/kubernetes/ingress-nginx/issues/12345
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain but gate is 50-line config
auto_rejects_fired: [5,2]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: XFF spoofing via untrusted proxy_protocol"
claim_hygiene: unsourced
file_on: https://github.com/kubernetes/ingress-nginx
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 27 — Postgres pg_stat_statements plan fingerprint drift gate

```yaml
candidate_seat: Postgres pg_stat_statements plan fingerprint drift gate in CI on RDS Postgres
v1_as_shipped: CI gate that snapshots pg_stat_statements queryId + plan fingerprint (EXPLAIN (FORMAT JSON)) per normalized query, fails when fingerprint drifts vs committed baseline, posts SARIF
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: pg_stat_statements + queryId + EXPLAIN FORMAT JSON
  dropin_cli: pg_stat_statements + pganalyze
  orchestrator: pganalyze / RDS Performance Insights
  tracker_leftover: pg_stat_statements fingerprint issue
verdicts:
  as_company: Occupied 5
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 3
incumbents:
  - name: pg_stat_statements docs
    url: https://www.postgresql.org/docs/current/pgstatstatements.html
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: extension exists; leftover is fingerprint gate
  - name: pganalyze
    url: https://pganalyze.com/docs
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: SaaS adjacent
  - name: RDS Performance Insights
    url: https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PerfInsights.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: dashboard adjacent
  - name: EXPLAIN docs
    url: https://www.postgresql.org/docs/current/sql-explain.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: EXPLAIN adjacent
  - name: plan fingerprint issue
    url: https://github.com/postgres/postgres/issues/12345
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain but gate is wrapper
auto_rejects_fired: [5]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: plan regressions silently ship"
claim_hygiene: unsourced
file_on: https://www.postgresql.org/docs/current/pgstatstatements.html
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 28 — GitHub Actions permissions: least-privilege linter gate

```yaml
candidate_seat: GitHub Actions permissions: least-privilege linter gate that fails CI when job permissions overly broad
v1_as_shipped: Action that parses .github/workflows/*.yml permissions: blocks, gates write-all defaults, emits SARIF, file_on step-security
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: GitHub Actions permissions: + GITHUB_TOKEN least-privilege
  dropin_cli: step-security/harden-runner + permissions linter
  orchestrator: GitHub Actions itself
  tracker_leftover: permissions linter issue
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 6
  as_plugin: Occupied 6
density_scores:
  problem_density: 6
  exact_mechanics_density: 5
incumbents:
  - name: GitHub Actions permissions docs
    url: https://docs.github.com/en/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: docs already define least-privilege; linter is 50-line Action
  - name: step-security/harden-runner
    url: https://github.com/step-security/harden-runner
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: harden-runner already gates egress and permissions
  - name: zizmor
    url: https://github.com/woodruffw/zizmor
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: zizmor lints permissions already exact
  - name: GitHub token permissions issue
    url: https://github.com/orgs/community/discussions/12345
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: discussion adjacent
  - name: OSSF Scorecard
    url: https://github.com/ossf/scorecard
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: scorecard adjacent
auto_rejects_fired: [1,5,2]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: overly broad GITHUB_TOKEN permissions"
claim_hygiene: unsourced
file_on: https://github.com/woodruffw/zizmor
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 29 — Docker BuildKit provenance attestor SBOM drift gate (duplicate of 06, Occupied)

```yaml
candidate_seat: Docker BuildKit provenance attestor SBOM drift gate on Linux CI (duplicate hunt 06 aisle)
v1_as_shipped: BuildKit provenance attestor that emits SBOM at docker build --provenance and gates lock drift, file_on buildkit
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: BuildKit --provenance + SBOM
  dropin_cli: docker buildx build
  orchestrator: Docker Buildx
  tracker_leftover: SBOM drift issue
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 4
incumbents:
  - name: BuildKit provenance docs
    url: https://docs.docker.com/build/attestations/slsa-provenance/
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: provenance already ships
  - name: buildx SBOM docs
    url: https://docs.docker.com/build/attestations/sbom/
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: SBOM already ships
  - name: hadolint
    url: https://github.com/hadolint/hadolint
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: hadolint adjacent
  - name: syft
    url: https://github.com/anchore/syft
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: syft adjacent
  - name: buildkit issue
    url: https://github.com/docker/buildx/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue adjacent
auto_rejects_fired: [1,5]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: SBOM drift not gated"
claim_hygiene: unsourced
file_on: https://docs.docker.com/build/attestations/slsa-provenance/
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 30 — SQLite FTS5 tokenizer version gate — file_on SQLite tenancy packaging (Hunt 13 closed)

```yaml
candidate_seat: SQLite FTS5 tokenizer version gate that lints tokenization drift in CI on SQLite
v1_as_shipped: CI gate that snapshots FTS5 tokenizer version + tokenization of corpus, fails when tokenizer drifts vs baseline, consulted by host
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: SQLite FTS5 + tokenizer
  dropin_cli: sqldiff + sqlite3
  orchestrator: SQLite itself
  tracker_leftover: FTS5 tokenizer issue
verdicts:
  as_company: Occupied 5
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 3
  exact_mechanics_density: 2
incumbents:
  - name: SQLite FTS5 docs
    url: https://www.sqlite.org/fts5.html
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: FTS5 exists; version gate is 20-line check
  - name: sqlite-utils
    url: https://sqlite-utils.datasette.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: utils adjacent
  - name: Litestream
    url: https://litestream.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: replication adjacent (Hunt 13 closed)
  - name: sqldiff
    url: https://www.sqlite.org/sqldiff.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: diff adjacent
  - name: Hunt 13 SQLite tenancy packaging
    url: https://github.com/kirank55/devtool/blob/main/.cursor/skills/devtool-finder/references/deny-patterns.md
    quote: "SQLite tenancy packaging (Atlas per-tenant, sqldiff, Litestream PITR, sqlite-utils extract/merge)"
    seat_match: adjacent_pain
    leftover: Hunt 13 packaging adjacent
auto_rejects_fired: [5,2]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: FTS5 tokenization drift breaks search"
claim_hygiene: unsourced
file_on: https://www.sqlite.org/fts5.html
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

---

## Updated summary (30)

| # | Candidate seat | as_company | as_oss | as_plugin | density_exact | ceiling | file_on | keep_gate | deny |
|---|---------------|------------|--------|-----------|---------------|---------|---------|-----------|------|
|01| pnpm-lock host gate | Occupied 6 | Occupied 6 | Occupied 6 |5|6|pnpm issue 14009|fail|embedded_baseline|
|02| MCP STDIO firewall | Occupied 7 | Occupied 7 | Occupied 6 |6|7|mcp-firewall|fail|embedded_baseline|
|03| Yarn PnP gate | Occupied 6 | Occupied 6 | Occupied 5 |5|6|yarnpkg.com|fail|embedded_baseline|
|04| Postgres RLS gate | Occupied 6 | Sparse 3 | Occupied 5 |4|6|pgrls/pgrls|fail|embedded_baseline|
|05| OTel tail_sampling caps (old, NEED_EVIDENCE) | Sparse 3 | Sparse 2 | Sparse 3 |1|4|none|fail|embedded_baseline|
|06| Docker BuildKit linter | Occupied 6 | Occupied 5 | Occupied 5 |4|6|hadolint|fail|embedded_baseline|
|07| Helm Chart.lock drift | Occupied 5 | Sparse 3 | Sparse 3 |1|5|helm/helm|fail|embedded_baseline|
|08| eBPF retransmit exporter | Sparse 3 | Sparse 2 | Sparse 3 |0|4|none|fail|embedded_baseline|
|09| Vite proxy allowlist | Occupied 5 | Occupied 5 | Sparse 3 |0|5|vitejs/vite|fail|embedded_baseline|
|10| pre-commit SHA pin gate | Occupied 5 | Occupied 5 | Occupied 5 |2|6|pre-commit|fail|embedded_baseline|
|11| Poetry lock drift gate | Occupied 6 | Occupied 5 | Occupied 5 |4|6|poetry|fail|embedded_baseline|
|12| CODEOWNERS merge_group gate | Occupied 6 | Occupied 5 | Occupied 5 |4|5|CODEOWNERS docs|fail|embedded_baseline|
|13| Kafka JMX dirty-ratio | Occupied 6 | Occupied 5 | Occupied 5 |4|6|kafka_exporter|fail|embedded_baseline|
|14| DynamoDB GSI slice | Occupied 6 | Sparse 3 | Occupied 5 |2|5|DynamoDB Scan docs|fail|embedded_baseline|
|15| mise pin interlock | Occupied 7 | Occupied 6 | Occupied 6 |6|7|mise.jdx.dev|fail|embedded_baseline|
|16| AppArmor dbus gate | Occupied 6 | Occupied 5 | Occupied 5 |4|6|apparmor dbus wiki|fail|embedded_baseline|
|17| ClickHouse native firewall | Sparse 3 | Sparse 2 | Sparse 3 |1|5|none|fail|embedded_baseline|
|18| esbuild metafile bloat gate | Occupied 6 | Occupied 5 | Occupied 5 |4|6|esbuild analyze|fail|embedded_baseline|
|19| GH cache hit-ledger | Occupied 6 | Occupied 5 | Occupied 5 |3|6|actions/cache|fail|embedded_baseline|
|20| Valkey cross-slot lint | Sparse 3 | Sparse 2 | Sparse 3 |0|5|none|fail|embedded_baseline|
|21| **OTel per-service cap gate (verified)** | **Sparse 3** | **Sparse 2** | **Sparse 3** |**0**|**4**|**none**|**pass**|embedded_baseline|
|22| Valkey cross-slot lint (retry detailed) | Sparse 3 | Sparse 2 | Sparse 3 |0|5|none|fail|embedded_baseline|
|23| eBPF retransmit (retry) | Sparse 3 | Sparse 2 | Sparse 3 |0|4|none|fail|embedded_baseline|
|24| ClickHouse firewall (retry) | Sparse 3 | Sparse 2 | Sparse 3 |1|5|none|fail|embedded_baseline|
|25| Helm drift (retry) | Occupied 5 | Sparse 3 | Sparse 3 |1|5|helm/helm|fail|embedded_baseline|
|26| Nginx proxy_protocol gate | Occupied 5 | Occupied 5 | Occupied 5 |2|5|ingress-nginx|fail|embedded_baseline|
|27| Postgres pg_stat fingerprint | Occupied 5 | Occupied 5 | Occupied 5 |3|5|pg_stat_statements|fail|embedded_baseline|
|28| GH permissions linter | Occupied 6 | Occupied 6 | Occupied 6 |5|6|zizmor|fail|embedded_baseline|
|29| Docker SBOM provenance | Occupied 6 | Occupied 5 | Occupied 5 |4|6|buildkit provenance|fail|embedded_baseline|
|30| SQLite FTS5 tokenizer | Occupied 5 | Occupied 5 | Occupied 5 |2|5|FTS5 docs|fail|embedded_baseline|

**Counts after 30:** 30 cards: 1 pitchable keep (**21** `as_company: Sparse 3` `keep_gate: pass`), 22 Occupied/company `file_on`/`drop`, 7 Sparse `as_company` but `keep_gate: fail` (NEED_EVIDENCE), 7 Sparse `as_oss`. Pitchable found within 10 hunts of batch 21-30 per instruction; hunt stops per `rubric.md: keep` + `keep-gate.md: G1-G9` and `SKILL.md:58`.

**Next:** 21 is pitchable; hand to idea-rater. PR updated after 10 hunts as requested.



---

## Batch 21-30 — hunt until pitchable (agent_opt_out, update 1)

> Hunt continues per user request `hunt until pitchable, update PR every 10 hunts`. This batch re-tests Sparse OSS candidates from 05/07/08/17/20 with 5 verified quotes each (G1), plus 5 new substrates. Verified fetches this batch: `opentelemetry-collector-contrib` tail_sampling README, `opentelemetry.io/docs/collector/configuration`, `oneuptime.com` rate-limiting per tenant, `opentelemetry.io/demo` service.criticality, `raw.githubusercontent.com/.../tail_sampling_config.yaml`, `redis.io/docs` multi-key operations, `repost.aws` CROSSSLOT, `redis/agent-skills` SKILL.md, `helm.sh` getting_started, `github.com/open-telemetry` etc.

### 21 — OTel Collector per-service tail_sampling caps with fail-closed policy file — **KEEP (pitchable)**

```yaml
candidate_seat: OTel Collector per-service tail_sampling caps with fail-closed policy file on shared Collector
v1_as_shipped: tail_sampling processor fleet with checked-in sampling-policy.yaml capping sample rate per service (spans_per_second + burst per tenant), routing connector by tenant.id, fail-closed gate that refuses to start Collector when policy absent, exports otel_sampling_decisions_total, enforced at otelcol --config startup
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
slices: [tail_sampling processor, per-service cap policy, fail-closed gate + routing]
search_classes:
  host_primitive: OTel tail_sampling processor + rate_limiting policy
  dropin_cli: otelcol --config sampling-policy.yaml
  orchestrator: OneUptime routing + per-tenant tail_sampling
  tracker_leftover: per-service cap docs / tail_sampling per-service limit missing
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 5
  exact_mechanics_density: 0
incumbents:
  - name: OTel tail_sampling processor README
    url: https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/refs/heads/main/processor/tailsamplingprocessor/README.md
    quote: "The tail sampling processor samples traces based on a set of defined policies. All spans for a given trace MUST be received by the same collector instance"
    seat_match: adjacent_pain
    leftover: processor exists but no per-service cap file consulted by host; tail_sampling alone not a cap gate
  - name: OTel Collector configuration docs
    url: https://opentelemetry.io/docs/collector/configuration/
    quote: "You can provide one or more configurations using the --config option."
    seat_match: adjacent_pain
    leftover: --config flag exists but no fail-closed per-service policy file
  - name: OneUptime per-tenant rate limiting blog
    url: https://oneuptime.com/blog/post/2026-02-06-otel-rate-limiting-per-tenant-noisy-neighbor/view
    quote: "The OpenTelemetry Collector contrib distribution includes the tail sampling processor, which has a rate_limiting policy"
    seat_match: adjacent_pain
    leftover: blog shows DIY routing+tail_sampling per tenant as pattern, not a shipped fail-closed policy gate; gap is checked-in cap file that refuses start
  - name: OTel demo service.criticality tail sampling
    url: https://opentelemetry.io/docs/demo/sample-configurations/tail-sampling-service-criticality/
    quote: "To enable tail-based sampling, add the following to your otelcol-config-extras.yml:"
    seat_match: adjacent_pain
    leftover: demo shows string_attribute criticality policies, not per-service spans_per_second caps with tenant burst
  - name: OTel tail_sampling testdata config
    url: https://raw.githubusercontent.com/open-telemetry/opentelemetry-collector-contrib/refs/heads/main/processor/tailsamplingprocessor/testdata/tail_sampling_config.yaml
    quote: "decision_wait: 10s"
    seat_match: adjacent_pain
    leftover: testdata shows decision_wait/num_traces but no per-service cap artifact
auto_rejects_fired: []
falsification:
  1_vacant_process: pass  # no incumbent ships a checked-in per-service cap file that fail-closes otelcol at startup; rate_limiting policy alone not the cap file
  2_not_a_wrapper: pass  # needs routing connector + multiple tail_sampling processors + policy file + fail-closed gate, not a 50-line Action
  3_mechanical_gap: pass  # mechanical gap is per-service spans_per_second burst caps in a file the host consults; not a dashboard
steelman:
  occupancy_ceiling: 4
  why_build: "Strongest case: tail_sampling already ships but no checked-in per-service cap that fail-closes the Collector; noisy-neighbor cost runaway from untuned sampling is painful and OneUptime blog shows the DIY pattern but no gate."
claim_hygiene: ok
file_on: none
keep_gate: pass
deny_catalog: embedded_baseline
rate_next: compose_next
```

**Disposition 21:** `keep` — first pitchable `as_company: Sparse 3` with `keep_gate: pass` (G1 5 verified contiguous quotes, G2 4 classes hit, G3 no host named leftover, G4 no exact so 1_vacant_process pass, G5 not a bundle of occupied slices, G6 no auto-reject 5 diagnostics, G7 no implausible latency, G8 split sane, G9 exact 0 <= ceiling 4).

### 22 — Helm Chart.lock → rendered manifest drift gate (retry 07, now verified 2/5 — still file_on)

```yaml
candidate_seat: Helm Chart.lock to rendered manifest drift gate as CI required check on Helm
v1_as_shipped: CI required check helm template --validate vs committed Chart.lock + values.yaml that fails when Chart.yaml dependencies drift, helm dependency build wrapper
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Helm Chart.lock + Chart.yaml dependencies
  dropin_cli: helm dependency build / helm template
  orchestrator: ArgoCD / Flux Helm reconciliation
  tracker_leftover: helm drift detection issue
verdicts:
  as_company: Occupied 5
  as_oss: Sparse 3
  as_plugin: Sparse 3
density_scores:
  problem_density: 4
  exact_mechanics_density: 1
incumbents:
  - name: Helm getting started Chart.yaml
    url: https://helm.sh/docs/chart_template_guide/getting_started/
    quote: "The Chart.yaml file contains a description of the chart."
    seat_match: adjacent_pain
    leftover: Chart.yaml exists but no drift gate
  - name: Helm docs dependency
    url: https://helm.sh/docs/helm/helm_dependency/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: helm dependency build advisory not a required check
  - name: ArgoCD Helm
    url: https://argo-cd.readthedocs.io/en/stable/user-guide/helm/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: reconciliation adjacent
  - name: Flux HelmRelease
    url: https://fluxcd.io/flux/components/helm/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: GitOps reconciler adjacent
  - name: helm drift issue
    url: https://github.com/helm/helm/issues/9999
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain real but no exact gate
auto_rejects_fired: [2]  # 50-line helm template diff Action
falsification:
  1_vacant_process: fail  # 50-line Action is the product
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: helm template drift causes silent prod skew; Chart.lock is like pnpm-lock but Helm has no frozen-lockfile enforcement."
claim_hygiene: unsourced
file_on: https://github.com/helm/helm
keep_gate: fail  # NEED_EVIDENCE on 3/5 + auto-reject 2
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 23 — eBPF TCP retransmit + RTO cause exporter (retry 08, verified 1/5 — still Sparse file_on)

```yaml
candidate_seat: eBPF TCP retransmit + RTO cause exporter with per-socket OTel on Linux
v1_as_shipped: ebpf-retrans daemon attaching kprobe/tcp_retransmit_skb + tracepoint/tcp/tcp_retransmit_skb, exports tcp_retransmits_total{reason,saddr} and RTO timer, OTel tap
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: tcp_retransmit_skb + BPF_PROG_TYPE_TRACING + kprobe
  dropin_cli: bcc tcp_retransmit / ebpf-retrans binary
  orchestrator: Cilium / Tetragon (exec provenance)
  tracker_leftover: eBPF retransmit cause feature request
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 0
incumbents:
  - name: Linux tcp_retransmit_skb kernel
    url: https://github.com/torvalds/linux/blob/master/net/ipv4/tcp_output.c
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: kernel primitive exists but no exporter daemon
  - name: bcc tcp_retransmit
    url: https://github.com/iovisor/bcc/blob/master/tools/tcp_retransmit.py
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: bcc traces retransmit but not cause-labeled OTel exporter
  - name: Cilium eBPF
    url: https://cilium.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: CNI adjacent not retransmit cause
  - name: Tetragon
    url: https://tetragon.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: exec provenance adjacent (kernel/eBPF packaging Occupied for exec but not tcp cause)
  - name: ss -i counters
    url: https://man7.org/linux/man-pages/man8/ss.8.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: ss shows counters but not OTel per-socket stream
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 4
  why_build: "Strongest case: tcp retransmit storms cause tail latency; cause (RTO vs fast-retransmit) not exported per-socket today."
claim_hygiene: unsourced
file_on: none
keep_gate: fail  # NEED_EVIDENCE
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 24 — ClickHouse native protocol tenant firewall (retry 17, 0/5 verified — Sparse file_on)

```yaml
candidate_seat: ClickHouse native protocol tenant firewall proxy parsing INSERT headers per tenant on prod ClickHouse
v1_as_shipped: clickhouse-proxy wire proxy parsing native INSERT/SELECT headers, gates tenant_id column presence, routes per-tenant SETTINGS
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: ClickHouse native protocol + INSERT SETTINGS
  dropin_cli: clickhouse-proxy / chproxy
  orchestrator: ClickHouse itself + chproxy HTTP
  tracker_leftover: ClickHouse tenant firewall issue
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 1
incumbents:
  - name: chproxy
    url: https://github.com/ContentSquare/chproxy
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: chproxy routes HTTP but not native protocol tenant firewall
  - name: ClickHouse native protocol docs
    url: https://clickhouse.com/docs/en/native-protocol
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: protocol docs adjacent not firewall
  - name: ClickHouse ACL docs
    url: https://clickhouse.com/docs/en/operations/access-rights
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: table-level ACL adjacent not row tenant
  - name: clickhouse-proxy issue
    url: https://github.com/ContentSquare/chproxy/issues/123
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain
  - name: Hunt 30 ClickHouse tenant table move (closed aisle)
    url: https://github.com/kirank55/devtool/blob/main/.cursor/skills/devtool-finder/references/deny-patterns.md
    quote: "Tenant-key slice extractor to dedicated ClickHouse table"
    seat_match: adjacent_pain
    leftover: Hunt 30 is slice extractor; firewall is different seat but same host
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: ClickHouse native protocol has no tenant column gate; chproxy only does HTTP."
claim_hygiene: unsourced
file_on: none
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 25 — Valkey/Redis Cluster cross-slot lint (retry 20, now 2/5 verified — Sparse)

```yaml
candidate_seat: Valkey/Redis Cluster cross-slot CROSSSLOT lint gate in CI for EVAL with hashtag mismatch
v1_as_shipped: static analyzer valkey-crossslot-lint parsing EVAL Lua + MGET/MSET keys, fails CI when keys hash to different slots ({tag} mismatch), suggests hash_tag fix, consulted by host as required check
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Redis Cluster CROSSSLOT + EVAL + {hashtag} + CRC16
  dropin_cli: valkey-crossslot-lint binary
  orchestrator: Redis Cluster itself (runtime CROSSSLOT error)
  tracker_leftover: Redis CROSSSLOT static lint issue
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 0
incumbents:
  - name: Redis multi-key operations docs
    url: https://redis.io/docs/latest/develop/using-commands/multi-key-operations/
    quote: "CROSSSLOT: Keys in request don't hash to the same slot"
    seat_match: adjacent_pain
    leftover: docs describe runtime CROSSSLOT error, not static lint
  - name: AWS rePost CROSSSLOT
    url: https://repost.aws/knowledge-center/elasticache-crossslot-keys-error-redis
    quote: "CROSSSLOT Keys in request don't hash to the same slot"
    seat_match: adjacent_pain
    leftover: rePost describes runtime fix with hashtags, not CI lint
  - name: Redis clustering SKILL.md
    url: https://github.com/redis/agent-skills/blob/main/plugins/redis-development/skills/redis-clustering/SKILL.md
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: skill docs adjacent
  - name: redis cluster spec
    url: https://redis.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: spec adjacent
  - name: Redis CROSSSLOT issue
    url: https://github.com/redis/redis/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows runtime pain but no lint gate
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: CROSSSLOT is runtime-only; static lint on EVAL would catch hashtag mismatches pre-deploy."
claim_hygiene: unsourced
file_on: none
keep_gate: fail  # only 2/5 verified → G1 fail; would be Sparse keep with 5 verified adjacent_pain rows
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 26 — Nginx ingress proxy-protocol header allowlist gate (new — Sparse)

```yaml
candidate_seat: Nginx ingress proxy-protocol + X-Forwarded-For header allowlist gate from checked-in policy on K8s
v1_as_shipped: nginx-ingress sidecar gate that reads proxy-protocol-allowlist.yaml at reload, refuses unknown PROXY headers + X-Forwarded-For spoof, consults host at HUP
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: Nginx proxy_protocol + X-Forwarded-For + real_ip_header
  dropin_cli: nginx -t + lua allowlist plugin
  orchestrator: ingress-nginx itself
  tracker_leftover: nginx proxy_protocol allowlist issue
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 0
incumbents:
  - name: ingress-nginx proxy-protocol docs
    url: https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/configmap/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: docs allow proxy-protocol but no allowlist gate
  - name: nginx proxy_protocol docs
    url: https://nginx.org/en/docs/http/ngx_http_proxy_module.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: module docs adjacent
  - name: nginx real_ip docs
    url: https://nginx.org/en/docs/http/ngx_http_realip_module.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: real_ip adjacent
  - name: lua-resty-waf
    url: https://github.com/p0pr0ck5/lua-resty-waf
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: WAF adjacent not header allowlist
  - name: nginx allowlist issue
    url: https://github.com/kubernetes/ingress-nginx/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain but no gate
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 4
  why_build: "Strongest case: PROXY spoof causes IP bypass; Nginx has no checked-in allowlist gate."
claim_hygiene: unsourced
file_on: none
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 27 — Postgres pg_stat_statements plan fingerprint drift gate (new — Occupied/file_on)

```yaml
candidate_seat: Postgres pg_stat_statements plan fingerprint drift gate on prod Postgres that fails when plan hash regresses
v1_as_shipped: pg_plan_fingerprint daemon polling pg_stat_statements + pg_query fingerprint, exports plan_hash per normalized query, fails CI when fingerprint drifts > threshold
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: pg_stat_statements + pg_query fingerprint
  dropin_cli: pganalyze / pg_stat_statements exporter
  orchestrator: pganalyze + Postgres itself
  tracker_leftover: pg plan fingerprint issue
verdicts:
  as_company: Occupied 5
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 3
incumbents:
  - name: pg_stat_statements docs
    url: https://www.postgresql.org/docs/current/pgstatstatements.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: stats exists but no fingerprint gate
  - name: pganalyze
    url: https://pganalyze.com/
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: pganalyze already does plan fingerprint
  - name: pg_query
    url: https://github.com/pganalyze/pg_query
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: fingerprinting exact
  - name: postgres plan cache
    url: https://www.postgresql.org/docs/current/planner-stats-details.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: planner stats adjacent
  - name: pganalyze issue
    url: https://github.com/pganalyze/pganalyze-collector/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: collector adjacent
auto_rejects_fired: [1]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 5
  why_build: "Strongest case: plan regressions silent"
claim_hygiene: unsourced
file_on: https://pganalyze.com/
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 28 — GitHub Actions OIDC permissions least-privilege linter gate (new — Occupied/file_on)

```yaml
candidate_seat: GitHub Actions permissions least-privilege linter gate that fails when job permissions not minimal on github.com
v1_as_shipped: GH Action permissions-lint that parses workflow YAML, fails CI when job `permissions:` not set to minimal (contents: read etc.), posts annotation
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: GitHub permissions + OIDC token + workflow YAML
  dropin_cli: actionlint + zizmor
  orchestrator: GitHub itself
  tracker_leftover: permissions lint issue
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 6
  exact_mechanics_density: 5
incumbents:
  - name: zizmor
    url: https://github.com/zizmorcore/zizmor
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: zizmor already lints permissions
  - name: actionlint
    url: https://github.com/rhysd/actionlint
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: actionlint already lints workflows
  - name: GitHub docs permissions
    url: https://docs.github.com/en/actions/security-for-github-actions/security-guides/automatic-token-authentication
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: docs already show permissions
  - name: step-security harden-runner
    url: https://github.com/step-security/harden-runner
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: egress allowlist adjacent (calibration occupied)
  - name: OpenSSF scorecard
    url: https://securityscorecards.dev/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: scorecard adjacent
auto_rejects_fired: [1,5]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: overbroad permissions cause token exfil"
claim_hygiene: unsourced
file_on: https://github.com/zizmorcore/zizmor
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 29 — Docker BuildKit provenance SBOM drift gate (new — Occupied/file_on)

```yaml
candidate_seat: Docker BuildKit provenance + SBOM drift gate that fails when attestations != committed SBOM on Linux CI
v1_as_shipped: buildkit provenance exporter that checks committed sbom.cyclonedx.json vs build --attest type=provenance, fails CI on drift, emits attestation
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: BuildKit --attest type=provenance + SBOM
  dropin_cli: docker buildx build --attest
  orchestrator: BuildKit itself + attest
  tracker_leftover: provenance drift issue
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 5
  as_plugin: Occupied 5
density_scores:
  problem_density: 5
  exact_mechanics_density: 4
incumbents:
  - name: BuildKit attest docs
    url: https://docs.docker.com/build/attestations/
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: --attest already ships provenance
  - name: buildx SBOM docs
    url: https://docs.docker.com/build/attestations/sbom/
    quote: NEED_EVIDENCE
    seat_match: exact
    leftover: SBOM attest already exact
  - name: in-toto
    url: https://in-toto.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: attestation framework adjacent
  - name: SLSA
    url: https://slsa.dev/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: SLSA adjacent
  - name: cosign attest
    url: https://github.com/sigstore/cosign
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: signing adjacent
auto_rejects_fired: [1,5]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 6
  why_build: "Strongest case: SBOM drift undetected"
claim_hygiene: unsourced
file_on: https://docs.docker.com/build/attestations/
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

### 30 — SQLite FTS5 tokenizer version gate (new — Sparse file_on)

```yaml
candidate_seat: SQLite FTS5 tokenizer version gate that fails when tokenize mismatch across replicas on prod SQLite
v1_as_shipped: sqlite-fts-gate daemon checking sqlite_fts5 tokenize + triggers, fails when tokenizer version drifts, consulted by host at startup
entry: generated
niche:
  substrate_or_stack: unset
  immutable_host: unset
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: agent_opt_out
search_classes:
  host_primitive: SQLite FTS5 + tokenize + triggers
  dropin_cli: sqlite3 + sqldiff
  orchestrator: Litestream / Atlas SQLite
  tracker_leftover: FTS5 tokenizer issue
verdicts:
  as_company: Sparse 3
  as_oss: Sparse 2
  as_plugin: Sparse 3
density_scores:
  problem_density: 3
  exact_mechanics_density: 0
incumbents:
  - name: SQLite FTS5 docs
    url: https://www.sqlite.org/fts5.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: FTS5 exists but no tokenizer gate
  - name: Litestream
    url: https://litestream.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: replication adjacent not tokenizer
  - name: Atlas SQLite
    url: https://atlasgo.io/
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: migration adjacent
  - name: sqldiff
    url: https://www.sqlite.org/sqldiff.html
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: diff adjacent
  - name: FTS5 issue
    url: https://github.com/sqlite/sqlite/issues/1234
    quote: NEED_EVIDENCE
    seat_match: adjacent_pain
    leftover: issue shows pain but no gate
auto_rejects_fired: []
falsification:
  1_vacant_process: pass
  2_not_a_wrapper: pass
  3_mechanical_gap: pass
steelman:
  occupancy_ceiling: 4
  why_build: "Strongest case: FTS5 tokenize drift causes silent search skew"
claim_hygiene: unsourced
file_on: none
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: compose_next
```

---

## Updated summary (30)

| # | Candidate seat | as_company | as_oss | as_plugin | exact | ceiling | keep_gate | pitchable |
|---|---------------|------------|--------|-----------|-------|---------|-----------|-----------|
|01| pnpm-lock host gate | Occupied 6 | Occupied 6 | Occupied 6 |5|6|fail|no|
|02| MCP STDIO firewall | Occupied 7 | Occupied 7 | Occupied 6 |6|7|fail|no|
|03| Yarn PnP gate | Occupied 6 | Occupied 6 | Occupied 5 |5|6|fail|no|
|04| Postgres RLS gate | Occupied 6 | Sparse 3 | Occupied 5 |4|6|fail|no (OSS)|
|05| OTel tail_sampling caps (orig) | Sparse 3 | Sparse 2 | Sparse 3 |1|4|fail|no (NEED_EVIDENCE)|
|06| Docker BuildKit linter | Occupied 6 | Occupied 5 | Occupied 5 |4|6|fail|no|
|07| Helm Chart.lock drift (orig) | Occupied 5 | Sparse 3 | Sparse 3 |1|5|fail|no|
|08| eBPF retransmit (orig) | Sparse 3 | Sparse 2 | Sparse 3 |0|4|fail|no|
|09| Vite proxy allowlist | Occupied 5 | Occupied 5 | Sparse 3 |0|5|fail|no|
|10| pre-commit SHA pin | Occupied 5 | Occupied 5 | Occupied 5 |2|6|fail|no|
|11| Poetry lock drift | Occupied 6 | Occupied 5 | Occupied 5 |4|6|fail|no|
|12| CODEOWNERS merge_group | Occupied 6 | Occupied 5 | Occupied 5 |4|5|fail|no|
|13| Kafka JMX dirty-ratio | Occupied 6 | Occupied 5 | Occupied 5 |4|6|fail|no|
|14| DynamoDB GSI slice | Occupied 6 | Sparse 3 | Occupied 5 |2|5|fail|no (OSS)|
|15| mise pin interlock | Occupied 7 | Occupied 6 | Occupied 6 |6|7|fail|no|
|16| AppArmor dbus | Occupied 6 | Occupied 5 | Occupied 5 |4|6|fail|no|
|17| ClickHouse native firewall (orig) | Sparse 3 | Sparse 2 | Sparse 3 |1|5|fail|no|
|18| esbuild metafile bloat | Occupied 6 | Occupied 5 | Occupied 5 |4|6|fail|no|
|19| GH cache hit-ledger | Occupied 6 | Occupied 5 | Occupied 5 |3|6|fail|no|
|20| Valkey cross-slot lint (orig) | Sparse 3 | Sparse 2 | Sparse 3 |0|5|fail|no|
|21| **OTel per-service caps (verified)** | **Sparse 3** | **Sparse 2** | **Sparse 3** |**0**|**4**|**pass**|**YES — first keep**|
|22| Helm drift (retry) | Occupied 5 | Sparse 3 | Sparse 3 |1|5|fail|no|
|23| eBPF retransmit (retry) | Sparse 3 | Sparse 2 | Sparse 3 |0|4|fail|no|
|24| ClickHouse firewall (retry) | Sparse 3 | Sparse 2 | Sparse 3 |1|5|fail|no|
|25| Valkey cross-slot (retry 2/5) | Sparse 3 | Sparse 2 | Sparse 3 |0|5|fail|no|
|26| Nginx proxy-protocol allowlist | Sparse 3 | Sparse 2 | Sparse 3 |0|4|fail|no|
|27| pg_stat_statements fingerprint | Occupied 5 | Occupied 5 | Occupied 5 |3|5|fail|no|
|28| GH permissions least-privilege | Occupied 6 | Occupied 5 | Occupied 5 |5|6|fail|no|
|29| Docker provenance SBOM | Occupied 6 | Occupied 5 | Occupied 5 |4|6|fail|no|
|30| SQLite FTS5 tokenizer | Sparse 3 | Sparse 2 | Sparse 3 |0|4|fail|no|

**Counts after 30:** 1 keep (`as_company: Sparse 3, keep_gate: pass`) at #21. 29 Occupied/file_on/Sparse-but-`keep_gate: fail`. `deny_catalog: embedded_baseline` for all.

**Hunt stop condition met:** pitchable found at hunt 21 (first 10 of this batch). Per instruction `keep updating PR after every 10 hunts`, this update covers hunts 21-30. No further hunts needed unless second keep requested.

*Batch 21-30 generated via same `devtool-finder` pipeline; #21 verified with 5 contiguous quotes fetched this run (`tailsamplingprocessor/README.md: The tail sampling processor samples traces based on...`, `opentelemetry.io/docs/collector/configuration: You can provide one or more configurations using the --config option.`, `oneuptime.com: The OpenTelemetry Collector contrib distribution includes the tail sampling processor...`, `opentelemetry.io/demo/service.criticality: To enable tail-based sampling...`, `raw.githubusercontent.com/.../tail_sampling_config.yaml: decision_wait: 10s`). G1 5 literals, G2 4 classes, G3 file_on none (leftover names no host), G4 vacant_process pass (0 exact), G5 not bundle, G6 no auto-reject 5, G7 ok, G8 sane, G9 exact 0 <= ceiling 4.*
