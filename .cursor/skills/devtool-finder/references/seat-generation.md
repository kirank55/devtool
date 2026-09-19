# Seat generation

This file answers "how do I propose seat S?" -- not "how do I search incumbents of S?"

**Start from substrates, never from pain slogans.** Pain is abundant; empty seats are not.

## Niche first

Do not open this file on a slogan hunt. If the scope gate has not passed,
return to [intake.md](intake.md).

Generate **inside the niche**. `substrate_or_stack` and `immutable_host`
constrain the inventory: drop substrates that are not that stack family
unless `niche.source` is `agent_opt_out`.

`hard_nos` are generation filters, not occupancy scores. Drop a raw seat
that matches a hard no **before** deny.

When `source: agent_opt_out`, use the full substrate inventory and set
`niche.source: agent_opt_out` on every raw seat.

## Substrate inventory

Generate from these nouns:

- Process supervisor / daemon
- Wire proxy / protocol gate
- Compiler, linker, bundler, lockfile
- Kernel / eBPF / LSM
- CI scheduler / merge queue
- Broker / queue protocol
- Schema / tenancy cutover
- Host runtime enforcement (PATH, interpreter, package manager)

## Vacancy probes

Queries for missing SKUs, not "best tools for X":

- Named protocol or RFC with no shipping daemon in that seat
- Host that does not consult a sidecar (policy file, third-party lockfile, PATH shim)
- Advisory-only tool sitting in an enforcement seat
- Language-scoped exact (in-process runtime) with a claimed language-agnostic v1 -- label later; do not auto-pitch

## Raw seat shape

Each raw seat must include, before search:

```yaml
candidate_seat: <stack position, one line>
v1_as_shipped: <concrete deliverable and where it sits>
substrate: <one item from the inventory>
process_or_protocol: <named process; not a vibe>
why_not_a_slogan: <the mechanic, in one sentence>
niche:
  substrate_or_stack: <from intake>
  immutable_host: <from intake>
  ship_form: company | oss | plugin | unset
  unique_data_or_distribution: <from intake or unset>
  hard_nos: []
  source: user | agent_opt_out
```

Drop the seat if `process_or_protocol` or `why_not_a_slogan` cannot be filled.
Drop the seat if it ignores `immutable_host` or a `hard_nos` entry.

## Hunt discipline

Generate >=5 raw seats per hunt request **inside the niche**. Then run the `SKILL.md` pipeline on each. Expect most to become `file_on` or drop. A hunt that emits five slogan keeps has failed. A hunt that emits seats outside the niche has failed. A hunt that emits Sparse company keeps without `keep_gate: pass` has failed. A hunt that emits five Occupied merge-queue packaging leftovers (`cancel-in-progress`, Trunk lanes, harden-runner, `npm ci`, systemd quotas, Trunk flakes) has finished that aisle: switch substrate; do not found the packaging. A hunt that emits five Occupied npm/Node PATH leftovers (`bwrap` lifecycle sandbox, Volta/fnm engines, lavamoat bins, npm `prefix`, `NODE_OPTIONS` wrapper) has finished that aisle too. A hunt that emits five Occupied Redis RESP sidecars (ACL firewall, Envoy faults, RedisShake prefix migrate, MONITOR audit tap, Envoy `ReadPolicy` lag router) has finished that aisle too. A hunt that emits five Occupied rustc/cargo leftovers (sccache, cargo-auditable, cargo-deny/bloat, cargo-geiger, `cargo vendor`) has finished that aisle too. A hunt that emits five Occupied kernel/eBPF leftovers (cgroup freezer-budget, fapolicyd exec-allowlist, BPF-LSM/AppArmor, io_uring `SystemCallFilter`, scx_layered, Tetragon/Tracee/Falco) has finished that aisle too. If `v1_as_shipped` is a conjunction, list slices on the raw seat before search.

Do not use closed-aisle leftovers as generation seeds (ntfy flags, ngrok companions, "add X to Veln"). That is prior-kill-as-rubric. Do not port the previous hunt's one-line seats onto a new host (JetStream overlap-lint → RabbitMQ overlap-lint; Redis Envoy faults → AMQP Toxiproxy). Re-search **this** substrate.
