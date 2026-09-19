# Seat generation

This file answers "how do I propose seat S?" -- not "how do I search incumbents of S?"

**Start from substrates, never from pain slogans.** Pain is abundant; empty seats are not.

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
```

Drop the seat if `process_or_protocol` or `why_not_a_slogan` cannot be filled.

## Hunt discipline

Generate >=5 raw seats per hunt request. Then run the `SKILL.md` pipeline on each. Expect most to become `file_on` or drop. A hunt that emits five slogan keeps has failed.

Do not use closed-aisle leftovers as generation seeds (ntfy flags, ngrok companions, "add X to Veln"). That is prior-kill-as-rubric.
