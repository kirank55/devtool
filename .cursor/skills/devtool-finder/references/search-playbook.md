# Search playbook

Incumbent extraction for a seat already restated. Do not load this file before a
seat exists. Do not load this file if the scope gate failed or the niche is
`intake_blocked`. Queries are stack nouns from the niche plus the restated
seat, never "SaaS idea" or value-prop language.

## Query construction

- Spine is niche `substrate_or_stack` + `immutable_host` + the restated process
  or protocol.
- Use stack nouns + protocols: `wire protocol proxy`, `eBPF tc filter`,
  `AST collision queue`, `DPOR interleaving test`, `merge queue scheduler`,
  `lockfile host enforcement`.
- Do not use value-prop queries: `"best AI testing tool"`,
  `"developer productivity automation"`, `"SaaS idea"`.

## Mandatory query classes

Five logos is not a search. Before scoring, run **all four** classes against
this seat's process/protocol. Record the queries on the card under
`search_classes`. Stopping after adjacent pain tools (Bazel, MSW, full-instance
DMS) without class 1-2 is a keep-gate G2 fail.

1. **Host primitive.** The flag, SQL, LSM ABI, cgroup, or systemd property that
   already implements the mechanism (`CREATE PUBLICATION ... WHERE`, Landlock
   net ABI, `bwrap --unshare-net`, `.terraform.lock.hcl`).
2. **Drop-in CLI wrapping that primitive.** Unprivileged wrapper people already
   run (`landrun`, `pgcopydb`, `pg_easy_replicate`, firejail, nsjail).
3. **Commercial / orchestrator in the aisle.** Control plane or vendor SKU
   (DMS source filters, Trunk, Nile, harden-runner).
4. **Issue / feature request on class 2.** Tracker hits such as "row filter",
   "tenant extract", "loopback", "diagnostics" on the CLI from class 2. A filed
   issue **is** occupancy for auto-reject 5.

| Substrate | Class 1-2 starters (always query) |
| --- | --- |
| Schema / tenancy cutover | `CREATE PUBLICATION WHERE`, DMS source filters, `pgcopydb`, `pg_easy_replicate`, pglogical, logical replication switchover |
| Kernel / eBPF / LSM | landrun, bubblewrap, firejail, nsjail, Landlock ABI port vs IP, `unshare --net`. Non-netns class 1–2: cgroup v2 freezer/`cpu.max`/`io.max` + systemd-run/`CPUQuota`, fanotify `FAN_OPEN_EXEC_PERM` + fapolicyd, AppArmor/BPF LSM, `SystemCallFilter=` / seccomp `io_uring`, sched_ext `scx_layered`, Tetragon/Tracee/Falco. These are Occupied hosts, not Sparse leftovers. |
| Host runtime enforcement | same as LSM row, plus systemd `PrivateNetwork`, PATH shims the host consults, npm `ignore-scripts` / `prefix`, lavamoat `allow-scripts` (+ `--experimental-bins`), Volta/fnm `engines.node` shims, Node `NODE_OPTIONS` precedence. These class 1–2 hits are Occupied hosts, not Sparse leftovers. |
| Process supervisor / daemon | silo, systemd, ntfy, supervisord |
| Compiler / lockfile | host native lockfile (`*.lock.hcl`, lock.json, `Cargo.lock`) before any sidecar. rustc+cargo class 1–2: sccache / rust-cache, cargo-auditable / cargo-cyclonedx / `-Z sbom`, cargo-deny bans, cargo-bloat, cargo-geiger, `cargo vendor` / source replacement. These are Occupied hosts, not Sparse leftovers. |
| CI / merge queue | GitHub Actions `cancel-in-progress`, `merge_group` event, systemd `CPUQuota`/`MemoryMax`, `npm ci` lock mismatch, Trunk parallel queues / flaky quarantine, harden-runner egress, merge queue SKU, syntax-aware merge, TIA, conflict bot as **separate** slices. These class 1–2 hits are Occupied hosts, not Sparse leftovers. |
| Wire proxy / protocol gate | Redis ACL (`+@all -@dangerous`), Envoy Redis proxy (`downstream_auth_password`, Delay/Error faults, `ReadPolicy`, prefix routes), Redis `MIGRATE` / RedisShake, Redis `WAIT` / `min-replicas-to-write`, `MONITOR` / Redis Software audit. MySQL: ProxySQL firewall/whitelist, binlog reader, prepared-statement pool, MaxScale `causal_reads`/`MASTER_GTID_WAIT`, Percona audit redaction. These class 1–2 hits are Occupied hosts, not Sparse leftovers. Kafka class 1–2 remains Kroxylicious Filter API / kfake, not a new CI daemon. |
| Broker / queue protocol | NATS JetStream overlap/`10065`, republish cycle/`10052`, `nats stream backup`, nats-surveyor/`jsz`, `$SCHEMA.VALIDATE` gatekeepers. RabbitMQ topic bindings, DLX/Shovel, definitions export, message-interceptors, rabbitmq_prometheus. These are Occupied hosts, not Sparse leftovers. |

## Extraction rules

- >=5 named incumbents per candidate **and** classes 1-4 attempted.
- Each row: name, URL fetched this run, quote that is a **contiguous substring**
  of that page, one seat-match label, leftover if this row were exact.
- Unverified or 404 -> `NEED_EVIDENCE` on that row. No hallucinated products.
- Paraphrase is not a quote. Do not stitch a sentence the page does not contain.

## Stop condition

Do **not** stop at the fifth adjacent logo.

Stop when: classes 1-4 have been queried **and** either >=5 verified rows exist
or three independent 404/`NEED_EVIDENCE` rows exist for class 1-2 (host
primitive and CLI wrapper). Thin class 1-2 evidence => `claim_hygiene:
unsourced` and `as_company` must not be Sparse/Greenfield-keep.
