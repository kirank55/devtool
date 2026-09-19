# Deny patterns

Short catalog of collapse modes. Not a substitute for a full killed-seats table. A previous kill is a deny-list entry, not a scoring template (prior-kill-as-rubric): do not condense another project's killed-seats tables into this file as the working catalog.

## Local deny file (optional)

If the target workspace keeps its own killed-seats file (for example `docs/adr/0001-no-pitchable-candidate.md`), its tables are authoritative (`deny_catalog: local_adr_0001`). Confirm the candidate's one-line seat against those rows before scoring; a match stops the run with a pointer to that row.

If no such file exists, use the embedded baseline below (`deny_catalog: embedded_baseline`). A hunt-local killed-seats write-up under `.docs/` or `docs/` that tables one-line seats counts as a local deny file.

`deny_catalog: incomplete` only if neither a local deny file nor this fallback is available. That is not the happy path.

Intake `hard_nos` are generation filters. They are not deny-catalog rows and do not Occupied-score a seat by themselves.

## Collapse modes

1. **File it on the incumbent.** Named product already *is* the headline UX (silo for loopback isolation; ntfy `--wait-cmd` for silent local jobs).
2. **Add the missing ecosystem to Veln** (or Pixi, OpenTofu, ntfy, cachelens, Electric, Cursor, ...). Cross-ecosystem absence is not a company.
3. **Sidecar without host runtime enforcement.** Third-party lockfile, PATH wrap, or controller the platform does not consult (`tofulock`, `pio-lock`, `red-widow`). Real engineering, not a company.

## Embedded fallback (use when no local deny file exists)

Treat as closed unless a **mechanical** gap appears that the write-up missed:

- Phone notifiers for local/CI tasks (ntfy, Pushover)
- Localhost tunnels and OAuth companions (ngrok, Cloudflare named tunnels, Dev Tunnels)
- Worktree loopback isolation (silo)
- Sidecar locks without host enforcement

Fuller aisles (same rule -- closed unless a mechanical gap appears): advisory prompt-cache inspectors, vendor API contract drift seats, universal offline SQL mutation upcast (non-invertible; reject), PTY secret reverse-map (confused deputy; reject), agent sandbox / FS / secrets / MCP wraps the host already ships, package-manager-shaped lock/integrity seats the platform absorbed, GitHub merge-queue packaging (`cancel-in-progress`, systemd job quotas, `npm ci` lock-vs-image drift Action, Trunk impacted-target parallel lanes, harden-runner job-ID egress ledger, Trunk flaky-test quarantine), npm/Node PATH enforcement packaging (lifecycle net sandbox wrapping `bwrap` + lavamoat, Volta/fnm engines interlock, lavamoat `--experimental-bins` lockfile PATH gate, npm `prefix` redirector, `NODE_OPTIONS` allowlist wrapper), Redis RESP sidecar packaging (ACL-bridging firewall, Envoy per-command fault injection, prefix dual-write/RedisShake, MONITOR/Software audit OTel tap, Envoy `ReadPolicy` lag router), rustc/cargo packaging (sccache ledger, cargo-auditable/cyclonedx SBOM, cargo-deny/bloat duplicate gate, cargo-geiger unsafe allowlist, `cargo vendor` airgap mirror), kernel/eBPF packaging that is not Landlock-loopback (cgroup freezer-budget, fapolicyd lockfile exec-allowlist, BPF-LSM/AppArmor repo interlock, io_uring `SystemCallFilter`, scx_layered latency scheduler, Tetragon/Tracee/Falco OTel provenance).

- Hunt 7: RabbitMQ/AMQP packaging (binding overlap lint, DLX shovel replay, definitions backup, message-interceptors schema, prometheus lag reaper, Toxiproxy fault proxy)

- Hunt 8: MySQL protocol packaging (ProxySQL firewall, GTID causal router, stmt pool, MaxScale TLS, Percona audit tap, runaway throttle)

- Hunt 9: Go toolchain packaging (Athens airgap, setup-go cache, cyclonedx-gomod, toolchain pin, gosec unsafe, go-size-analyzer bloat). as_oss Sparse on gobloat is not a company keep.

- Hunt 10: CPython/pip/uv packaging (auditwheel, uv sync lock drift, free-threading docs, cibuildwheel repro, pipdeptree bloat)

- Hunt 11: JVM Maven/Gradle packaging (shade transformers, jdeps internals, config cache, jlink, APT isolation, dependency verification)

- Hunt 12: Envoy HTTP/gRPC filters (fault, proto scrubber, jwt_authn, router retry, rate limit)

- Hunt 13: SQLite tenancy packaging (Atlas per-tenant, sqldiff, Litestream PITR, sqlite-utils extract/merge)

- Hunt 14: MQTT broker packaging (mosquitto ACL/retained, HiveMQ bridge, EMQX rate-limit/LWT/inflight)

- Hunt 15: Elasticsearch tenancy packaging (aliases, CCR, ILM, templates, snapshots, reindex)

- Hunt 16: MongoDB wire packaging (RBAC firewall, maxTimeMS/killOp, Envoy mongo fault, maxStaleness, audit redaction, requireTLS)

- Hunt 17: flake.lock-to-store drift gate as CI required check on Nix flakes lockfile; flake.lock SBOM/SLSA attestor emitting signed CycloneDX at `nix build`; Nix closure bloat plus duplicate-input CI gate over flake.lock closure; Shared Nix store artifact-cache orchestrator with per-derivation hit ledger on Linux CI; Offline airgap flake input mirror daemon serving locked inputs on isolated nets; Flake input follows and duplicate-nixpkgs pin lint gate in CI

- Hunt 18: Wasmtime WASI preopen dir allowlist enforcer from checked-in policy (wasmtime --dir gate); Wasmtime wasi-http outgoing-host egress allowlist gate for wasmtime run-serve components; Wasmtime fuel plus epoch execution-budget enforcer per command from checked-in budgets; Wasmtime component WIT import capability CI gate denying wasi-sockets-http-env per policy; Wasmtime component OCI digest pin interlock refusing mutable tags without wkg-lock digest; Wasmtime WASI env inheritance allowlist gate blocking inherit-env secret passthrough

- Hunt 19: Pulsar bundle-ownership rebalance planner (split + unload dry-run) on prod Pulsar; Pulsar geo-replication backlog and replicated-subscription drift governor on prod Pulsar; Pulsar tiered-storage offload plus ledger-orphan auditor on prod Pulsar; Pulsar broker-deduplication gap plus transaction pending-ack reaper on prod Pulsar; Pulsar Key_Shared hash-range skew balancer on prod Pulsar; Pulsar namespace backlog-quota plus retention policy-as-code gate on prod Pulsar

- Hunt 20: Partition-key tenant slice extractor to dedicated keyspace on prod Cassandra CQL; Live per-tenant keyspace cutover daemon on prod Cassandra CQL with dual-write plus CDC catchup; Per-tenant keyspace schema parity CI gate across Cassandra keyspaces; Per-tenant tombstone plus gc_grace retention governor on prod Cassandra; Per-tenant snapshot PITR restore daemon on prod Cassandra keyspaces

- Hunt 21: Laptop-suspend-aware systemd timer catch-up coalescer (Persistent backlog merge); Per-timer journald retention cap governor for user timers; Procfile dev-task to systemd user timer unit generator with calendar lint; Ephemeral dev-loop fleet manager over systemd-run transient timers; Laptop AC-power and failure-gated timer guard (ConditionACPower plus OnFailure plus Restart backoff); OnCalendar thundering-herd spread linter (RandomizedDelaySec plus AccuracySec)

- Hunt 22: Memcached ASCII/binary translation plus multiget fan-out proxy for legacy clients on prod Memcached; Memcached large-value chunk plus manifest split proxy over 1MB item limit on prod Memcached; Memcached hot-key singleflight plus meta herd-guard proxy with W-Z lease semantics on prod Memcached; Memcached TTL-cap plus never-expire slab-evict auditor proxy on prod Memcached; Memcached gets-cas read-modify-write serializer proxy with bounded retry on prod Memcached

- Hunt 23: Gemfile.lock-to-installed-gems drift gate as CI required check on Bundler+RubyGems; Gemfile.lock SBOM/SLSA attestor emitting signed CycloneDX at bundle install on Bundler+RubyGems; Native-extension closure bloat plus duplicate-gem CI gate over Gemfile.lock closure on Bundler+RubyGems; Shared Bundler gem artifact-cache orchestrator with per-gem hit ledger on Linux CI; Offline airgap RubyGems mirror daemon serving compact index plus gem files on isolated nets

- Hunt 24: composer.lock-to-vendor drift gate as CI required check on PHP Composer; composer.lock SBOM/SLSA attestor emitting signed CycloneDX at composer install on PHP Composer; PHP ext-platform closure bloat plus duplicate-package CI gate over composer.lock; Shared Composer dist artifact-cache orchestrator with per-package hit ledger on Linux CI; Offline airgap Packagist mirror daemon serving composer metadata plus dist zips on isolated nets; Composer platform php-version plus ext enforcement interlock refusing wrong interpreter on PHP Composer

- Hunt 25: Deno anti-allow-all production interlock refusing `deno run -A` on prod entrypoints; Deno remote-import allowlist enforcer from checked-in policy at `deno run`; Deno `npm:` hermetic gate enforcing JSR-only prod entrypoints via `--no-npm`; Deno `--allow-net` egress host allowlist enforcer per entrypoint with deny carve-outs; Deno `--allow-run` subprocess allowlist interlock per `deno task` forbidding deno and shell spawn; Deno `deno.json` permission-sets scope gate confining prod server to data dir plus named env

- Hunt 26: bun.lock-to-node_modules drift gate as CI required check on Bun (`bun ci` / `--frozen-lockfile`); Bun trustedDependencies postinstall allowlist gate on Bun installs; Bun isolated-linker phantom-dependency enforcement gate on Bun workspaces; bunx ephemeral-run pin interlock refusing unpinned auto-install on Bun prod; bunfig.toml preload plugin allowlist gate on Bun prod entrypoints

- Hunt 27: build.zig.zon-to-cache drift gate as CI required check on Zig + build.zig; build.zig.zon SBOM/SLSA attestor emitting signed CycloneDX at `zig build`; Shared Zig global-cache orchestrator with per-package hit ledger on Linux CI; Offline airgap zon fetch mirror daemon serving tarballs plus hashes on isolated nets; Zig toolchain pin exec interlock refusing wrong `zig version` on minimum_zig_version plus zon; translate-c plus @cImport header-upgrade drift gate on Zig C interop

- Hunt 28: packages.lock.json-to-restore drift gate as CI required check on .NET NuGet; NuGet lock SBOM attestor emitting signed CycloneDX at dotnet publish; NativeAOT ILLink trim plus single-file bundle bloat and duplicate-package CI gate on .NET; Shared NuGet global-packages plus Roslyn build artifact-cache orchestrator with hit ledger on Linux CI; Offline airgap NuGet feed mirror daemon serving nupkgs on isolated nets; global.json SDK pin exec interlock refusing wrong dotnet on rollForward disable

- Hunt 29: Package.resolved-to-checkout drift gate as CI required check on SwiftPM (`--only-use-versions-from-resolved-file`); Package.resolved SBOM/SLSA attestor emitting signed CycloneDX at swift build on SwiftPM; SwiftPM closure bloat plus duplicate-package CI gate over Package.resolved; Shared SwiftPM build-cache orchestrator with per-package hit ledger on Linux CI; Offline airgap SwiftPM mirror daemon serving locked deps on isolated nets; Swift tools-version pin exec interlock refusing wrong swift toolchain on SwiftPM

- Hunt 30: Tenant-key slice extractor to dedicated ClickHouse table (tenant_id filter + schema clone); Live per-tenant table cutover daemon on ClickHouse (dual-write plus catchup plus EXCHANGE flip); Per-tenant ClickHouse DDL and schema parity CI gate across tenant tables; Per-tenant TTL retention governor attaching per-tenant lifecycle policies on ClickHouse tables; Per-tenant snapshot PITR restore daemon restoring single-tenant ClickHouse tables from shared backup; Cross-cluster per-tenant table move on ClickHouse via filtered copy plus alias flip

- Hunt 31: Per-service key-prefix allowlist firewall proxy in front of prod etcd gRPC; Deterministic etcd gRPC fault-injection proxy for CI (error at revision offsets); etcd watch fan-out coalescing gateway for prod etcd gRPC; etcd lease TTL-ceiling plus keepalive-audit governor proxy on prod etcd; etcd revision-staleness read router (linearizable versus serializable gate) on prod etcd

- Hunt 32: launchd KeepAlive crash-loop circuit breaker daemon (ThrottleInterval backoff + auto-disable + alert) on macOS developer laptops; launchd StandardOutPath log rotation governor (size caps + rotation + reload) for user agents on macOS developer laptops; launchd plist correctness linter plus fixer for deprecated keys on macOS developer laptops; launchd Sockets-activation migration helper (port spec to Sockets dict + launchctl verify) on macOS developer laptops; launchd LimitLoadToSessionType Aqua-versus-Background misplacement guard on macOS developer laptops; launchd per-agent resource-policy enforcer (ProcessType + Nice + LowPriorityIO from checked-in policy) on macOS developer laptops

- Hunt 33: Consul KV CAS check-and-set serializer proxy with bounded retry on prod Consul KV; Consul DNS SRV blocking-query fan-out coalescing gateway on prod Consul; Consul prepared-query name-allowlist plus datacenter-failover firewall proxy on prod Consul; Consul session lock-delay plus TTL-ceiling audit governor proxy on prod Consul; Consul Connect intentions handshake plus match-order audit gateway on prod Consul; Consul blocking-query consistency router with stale-consistent gate on prod Consul

- Hunt 34: JVM version pin exec interlock refusing wrong `java` on checked-in `.java-version` / `.sdkmanrc` / toolchain file; JAVA_TOOL_OPTIONS / JDK_JAVA_OPTIONS flag allowlist gate stripping debug/agent smuggling at `java` launch; -javaagent allowlist interlock per `java` launch from sha256-pinned policy; JPMS --add-opens / --add-exports encapsulation-break allowlist gate at `java` launch; JNI native-library path allowlist gate on `java.library.path` plus loadLibrary targets

- Hunt 35: mix.lock-to-deps drift gate as CI required check on Elixir mix+Hex; mix.lock SBOM/SLSA attestor emitting signed CycloneDX at mix compile on Elixir mix+Hex; Hex closure bloat plus duplicate-package CI gate over mix.lock on Elixir mix+Hex; Shared Mix/Hex build artifact-cache orchestrator with per-package hit ledger on Linux CI; Offline airgap Hex mirror daemon serving registry plus tarballs on isolated nets; Elixir plus Erlang toolchain pin exec interlock refusing wrong runtime on .tool-versions plus mix

- Hunt 36: Celery canvas chord stall detector (chord_unlock lag plus header-failure attribution) on Celery plus RabbitMQ; Celery beat double-fire guard (distributed lock plus due-task dedup) on Celery beat plus Redis; RQ DeferredJobRegistry dependency-orphan auditor (stuck-deferred TTL plus requeue) on RQ plus Redis; SQS visibility-heartbeat extender for Celery-SQS long tasks (ChangeMessageVisibility daemon thread) on Celery plus SQS; Celery worker prefetch head-of-line inspector (prefetch multiplier plus acks-late audit) on Celery plus RabbitMQ; RQ pause-drain cutover gate (rq suspend with duration plus burst drain plus resume) on RQ plus Redis

- Hunt 37: Per-service CONNECT destination allowlist firewall (dstdomain plus port allowlist plus user scope plus block) on Squid forward proxy; CONNECT-aware deterministic fault-injection proxy for CI (407 plus 502 plus tunnel-delay at CONNECT offsets) on Squid egress; CONNECT-tunnel redacted audit OTel tap (CONNECT host plus port plus bytes, no payload) on Squid; Parent-proxy latency-aware egress router (peer RTT plus dead-peer plus selection) on Squid cache_peer mesh; CONNECT plus upstream-TLS enforcement gate (frontend require plus backend verify plus cert audit) on Squid

- Hunt 38: MODULE.bazel.lock-to-fetch drift gate as CI required check on Bazel Bzlmod; MODULE.bazel.lock SBOM/SLSA attestor emitting signed CycloneDX at bazel build; Shared Bazel action-cache orchestrator with per-target hit ledger on Linux CI; Offline airgap Bazel registry mirror daemon serving locked Bzlmod modules on isolated nets; Bazel toolchain pin exec interlock refusing wrong bazel version on .bazelversion plus MODULE.bazel.lock; Bazel module closure bloat plus duplicate-module CI gate over MODULE.bazel.lock

- Hunt 39: Per-service DNS QNAME allowlist firewall proxy in front of prod CoreDNS/unbound; Deterministic DNS fault-injection proxy for CI on prod CoreDNS/unbound protocol; DNS query redacted audit OTel tap on prod CoreDNS/unbound; Upstream RTT-aware forwarder router on prod CoreDNS/unbound mesh; Response TTL-ceiling plus stale-serve governor proxy on prod DNS; DNSSEC sign-plus-validate enforcement gate on prod CoreDNS/unbound

- Hunt 40: Per-service envelope-sender allowlist firewall proxy in front of prod SMTP MTA; Deterministic SMTP fault-injection proxy for CI on prod SMTP MTA protocol; Envelope redacted audit OTel tap on prod SMTP MTA; Deferred-queue lag exporter plus stuck-queue reaper daemon on prod SMTP MTA; STARTTLS plus upstream-TLS enforcement gate on prod SMTP MTA; Per-domain outbound rate-limit throttle proxy on prod SMTP MTA

- Hunt 41: OpenResty lua_code_cache prod interlock refusing lua_code_cache off in prod; OpenResty lua_package_path plus lua_package_cpath allowlist gate from checked-in policy; LuaRocks plus OPM lock-to-installed drift gate as CI required check on OpenResty; OpenResty privileged-phase allowlist gate over init_by_lua plus set_by_lua from checked-in policy; LuaJIT FFI cdef plus ffi.load allowlist gate per OpenResty service from sha-pinned policy; OpenResty plus LuaJIT version pin exec interlock refusing wrong openresty -V on checked-in pin

- Hunt 42: buf.lock-to-generated drift gate as CI required check on buf/Protobuf; buf breaking plus lint enforcement gate as CI required check on buf/Protobuf; Protobuf descriptor closure bloat plus duplicate-package CI gate over buf.lock closure on buf/Protobuf; Shared buf generate artifact-cache orchestrator with per-module hit ledger on Linux CI; Offline airgap buf registry mirror daemon serving locked modules on isolated nets

- Hunt 43: Tenant-label slice extractor to dedicated Neo4j database on prod Bolt DBMS; Live per-tenant Neo4j cutover daemon with dual-write Bolt plus CDC catchup plus driver DB switch; Per-tenant Neo4j constraint and schema parity CI gate across tenant DBs; Per-tenant Neo4j point-in-time restore daemon from shared full plus differential backup chain; Cross-cluster per-tenant Neo4j move via filtered copy plus seed URI plus alias flip; Per-tenant Neo4j composite-alias router for Bolt cutover with zero driver change

- Hunt 44: Per-service TURN allocation allowlist firewall proxy (realm plus peer-IP plus quota) on WebRTC TURN; Deterministic RTP/RTCP fault-injection proxy for CI (PLI/NACK drop plus SSRC-tagged delay at offsets) on WebRTC; SDP offer-answer codec plus m-line scrub gateway per ingress on WebRTC; DataChannel SCTP PPID plus message-size firewall proxy on WebRTC data path; WHIP-WHEP bearer-token ingress gate plus upstream-TLS enforcement proxy on WebRTC ingest; ICE STUN binding storm throttle plus consent-audit proxy on WebRTC edge

- Hunt 45: Per-service XDP destination allowlist firewall daemon from checked-in policy on Linux; XDP/TC deterministic packet fault-injection harness for CI with per-5-tuple scenario file on Linux; XDP per-source token-bucket rate-limit plus SYN-flood throttle daemon on Linux; TC egress bandwidth-cap plus latency-injection daemon per destination port for dev/CI perf budgets on Linux; XDP redacted flow audit OTel tap exporting 5-tuple plus bytes and verdict without payload on Linux; XDP DNS QNAME denylist filter daemon dropping disallowed domains at driver layer on Linux

- Hunt 46: supervisord exitcode plus autorestart unexpected-policy gate across [program:x] on supervisord box; supervisord graceful-shutdown verifier over stopsignal plus stopwaitsecs plus stopasgroup on supervisord box; supervisord PROCESS_STATE event-listener OTel exporter on supervisord box; supervisord inet plus unix HTTP XML-RPC exposure plus auth audit gate on supervisord box; supervisord conf.d-to-running drift gate over reread plus update on supervisord box; supervisord priority ordered-start plus readiness wait orchestrator across [program:x] on supervisord box

- Hunt 47: Prefix tenant slice extractor to dedicated MinIO bucket (prefix filter plus versioned copy as local CLI); Live per-tenant prefix cutover daemon on MinIO with dual-write plus catchup plus endpoint flip; Per-tenant bucket-policy and versioning parity CI gate across MinIO tenant buckets; Per-tenant ILM retention governor attaching per-tenant lifecycle rules on MinIO tenant buckets; Per-tenant versioned PITR restore daemon restoring single-tenant MinIO prefix from shared versioned bucket; Cross-cluster per-tenant bucket move on MinIO via batch copy plus alias flip

- Hunt 48: Per-service LDAP search-filter firewall proxy (base-DN scope + filter allowlist + attribute allowlist + block) in front of prod LDAP; LDAP StartTLS/LDAPS enforcement gateway (frontend require-TLS + backend verify + cert audit) on prod LDAP; LDAP nested-group memberOf expansion cache proxy (memberof + nestgroup fan-out coalescing) in front of prod LDAP; LDAP search/bind audit-redaction OTel tap (DN + filter + attrs, redact password values) on prod LDAP; LDAP syncrepl/persistent-search fan-out coalescing gateway for prod LDAP consumers; LDAP bind-storm throttle plus password-policy lockout governor proxy (per-client bind rate + failed-bind lockout) on prod LDAP

- Hunt 49: cabal.project.freeze-to-store drift gate as CI required check on Haskell Cabal/Stack prod; cabal freeze plus stack lock SBOM attestor emitting signed CycloneDX at build on Haskell Cabal/Stack; GHC closure bloat plus duplicate-package CI gate over freeze closure on Haskell Cabal/Stack; Shared Cabal store plus Stack work artifact-cache orchestrator with per-package hit ledger on Linux CI; Offline airgap Hackage mirror daemon serving locked inputs on isolated nets for Haskell Cabal/Stack; GHC toolchain pin exec interlock refusing wrong ghc on checked-in pin for Haskell Cabal/Stack

- Hunt 50: site-packages `.pth` executable-line allowlist gate on CPython venv; PYTHONPATH plus PYTHONHOME env-inheritance allowlist gate at `python` launch on venv; Python interpreter-version pin exec interlock on `.python-version` plus venv pyvenv.cfg; sitecustomize plus usercustomize startup-hook allowlist interlock on CPython venv; CPython isolated plus safe-path enforcement gate for prod venv entrypoints

- Hunt 51: CURVE/ZAP certificate enrollment plus domain allowlist gate daemon on ZeroMQ fleet; REQ/REP strict-FSM deadlock plus Lazy-Pirate retry tracer sidecar on ZeroMQ; ROUTER mandatory plus identity allowlist envelope firewall proxy on ZeroMQ; XPUB/XSUB topic-prefix parity plus subscription-storm audit gate on ZeroMQ; Socket-monitor HWM-drop plus heartbeat OTel exporter with stuck-peer reaper on ZeroMQ; ZMTP deterministic fault-injection proxy for CI on ZeroMQ

- Hunt 52: QUIC 0-RTT anti-replay idempotency gate proxy in front of terminated QUIC/HTTP3; QUIC connection-ID migration-sticky edge router proxy on terminated QUIC/HTTP3; HTTP/3 QPACK redacted access-log plus QLOG OTel tap on terminated QUIC/HTTP3; QUIC Retry address-validation storm throttle proxy on terminated QUIC/HTTP3; Deterministic QUIC packet fault-injection proxy for CI on terminated QUIC/HTTP3

- Hunt 53: Tenant-subspace slice extractor to dedicated FoundationDB tenant (prefix filter + versioned copy as local CLI); Live per-tenant subspace cutover daemon on FoundationDB with dual-write plus versionstamp catchup plus tenant switch; Per-tenant Tenant Management plus schema-template parity CI gate across FoundationDB tenants; Per-tenant backup PITR restore daemon restoring single-tenant FoundationDB tenant from shared fdbbackup; Cross-cluster per-tenant tenant move on FoundationDB via fdbbackup plus fdbdr plus tenant flip; Per-tenant Record Layer record-store clone governor (template-pinned tenant clone as local CLI)

- Hunt 54: dune.lock-to-switch drift gate as CI required check on OCaml Dune; dune.lock plus opam SBOM attestor emitting signed CycloneDX at dune build; Dune closure bloat plus duplicate-package CI gate over dune.lock; Shared Dune build artifact-cache orchestrator with per-package hit ledger on Linux CI; Offline airgap opam plus Dune lock mirror daemon serving locked inputs on isolated nets; OCaml toolchain pin exec interlock refusing wrong compiler on checked-in Dune pin

- Hunt 55: OpenRC supervise-daemon crash-loop circuit breaker (respawn backoff + auto-disable + alert) on OpenRC box; OpenRC runscript need/use/after dependency correctness linter plus CI gate on OpenRC box; s6-rc compiled service DB drift gate (source defs vs live compiled) on s6 box; s6 supervision ordered-start readiness orchestrator (s6-svwait -U) on s6 box; OpenRC supervise-daemon stdout/stderr log rotation governor on OpenRC box; s6 readiness-notification coverage linter (notification-fd plus s6-svstat ready audit) on s6 box

## Priors are not a rubric

A previous kill is a deny-list entry, not a scoring template. Do not use closed-aisle leftovers as generation seeds. Re-search **this** seat. Name **this** seat's incumbents. Seat-match those rows.

Closed Occupied aisles from this hunt loop (see `.docs/killed-seats.md` for one-line seats):
- Hunt 6: NATS JetStream packaging (overlap lint, DLQ replay, S3 backup, schema gateway, surveyor lag reaper)
