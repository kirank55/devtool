# Seat match

Every incumbent gets **exactly one** label. This is the check that stops category collapse (Coyote counted as a Kafka wire proxy, Temporal counted as a CI interleaving tester).

## Labels

| Label | Meaning | Counts toward problem density? | Counts toward exact-mechanics density? |
|-------|---------|--------------------------------|----------------------------------------|
| `exact` | Same stack placement and SKU as the proposed v1 | yes | **yes** |
| `adjacent_pain` | Treats the same pain with different mechanics | yes | no |
| `language_scoped` | Same idea, wrong runtime (in-process .NET rewrite, Rust scheduler) | weakly | no |
| `wrong_substrate` | Same slogan, different data plane (MySQL/Vitess vs vanilla RDS Postgres) | weakly | no |
| `obsolete` | Abandoned or legacy; does not occupy the current year by default | no | no |
| `price_packaging` | A product exists in a nearby aisle; access, price, or lock-in may still be a gap | yes as adjacent | no unless it *is* the SKU |

If two labels could apply, pick the **strictest mismatch** (prefer `wrong_substrate` / `language_scoped` / `obsolete` over `exact`). Do not upgrade to `exact` to make a kill easier.

## Dual scores

**Problem density** -- how many ways already stop the *pain*, including `adjacent_pain`.

**Exact-mechanics density** -- how many products already *are* this daemon / proxy / compiler / CI check / library. Count `exact` only.

A bundle of three `exact` occupied slices sold as one SKU is **Occupied**, not Sparse. Packaging three occupied tools is not a new seat.

Architecture alternatives are not `exact`. Durable orchestration that *avoids* choreographed sagas (Temporal, Restate, DBOS) is `adjacent_pain` relative to a Kafka wire-protocol DPOR proxy in CI. It treats the pain. It is not the SKU.

## Examples (do not generalize beyond the label)

| Cited as occupant | Proposed seat | Correct label |
|-------------------|---------------|---------------|
| Coyote (.NET binary rewrite, mocked HTTP/Cosmos) | Kafka wire-protocol DPOR in CI | `language_scoped` |
| Filibuster (HTTP/gRPC fault injection) | Kafka message-interleaving scheduler | `adjacent_pain` |
| Shuttle / Loom (in-process Rust) | Drop-in broker proxy | `language_scoped` |
| Temporal / Restate / DBOS | CI tester for existing Kafka sagas | `adjacent_pain` |
| Vitess `MoveTables --tenant-id`, Ghostferry | Vanilla RDS **Postgres** tenant extract | `wrong_substrate` |
| PG15 `CREATE PUBLICATION ... WHERE (tenant_id = ...)` | Tenant-filtered logical replication on Postgres | `exact` (for that *slice*) |
| Citus `isolate_tenant_to_new_shard` | Extract a tenant **out of** vanilla RDS | `adjacent_pain` or `wrong_substrate` (Citus cluster, not vanilla RDS) |
| Azure Split-Merge (classic, ~2015) | 2026 tenant cutover | `obsolete` |
| Antithesis (expensive hypervisor) | Cheap CI DPOR proxy | `price_packaging` |
| Kroxylicious fetch-delay filter | Kafka wire proxy | `exact` for the proxy slice; leftover may still be OSS |

## How to write a row

Required fields per incumbent: name, URL, one quote from **that** page, `seat_match`, leftover (what is still missing if this row is `exact`).

A row without a URL is not an incumbent. Put it in `NEED_EVIDENCE` or drop it.
