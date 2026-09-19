# Rubric

Occupancy gate for the seat under review. Do not invent a parallel philosophy.

## What is scored

Score **existing-solution density**, not pain. Pain is abundant. Empty seats are not.

Score **v1 as shipped**, not the Series A architecture. If v1 is a GitHub Action plus an existing indexer, score that Action.

## Bands

| Band | Score | Meaning |
|------|------:|---------|
| Saturated | 8-10 | Named products already *are* this UX. Do not found. |
| Occupied | 5-7 | Adjacent tools treat the pain. Remaining work is glue, a flag, or a plugin. |
| Sparse | 2-4 | Pieces exist. No widely adopted product sits in the proposed seat. |
| Greenfield | 0-1 | Mechanics are new. |

Pitchable **as a company** only if Sparse or Greenfield **and** no automatic reject.

Occupied leftover -> `file_on` (flag / plugin / issue on the incumbent). Do not found.

Lowest crowding is not opportunity. A sparse *product* is still a bad build if a one-line config or vendor CLI already removes the pain (`lock_timeout`, ntfy `--wait-cmd`).

Unadopted is not Greenfield. A 0-star sidecar (`tofulock`, layercache, SemaMerge-at-zero-stars) often means the seat is gist-shaped or already named.

## Split verdicts

Emit three bands, not one:

| Field | Question |
|-------|----------|
| `as_company` | Would you found this? Sparse/Greenfield + no auto-reject, or no. |
| `as_oss` | Is a bounded library/proxy worth publishing? May be yes when `as_company` is no. |
| `as_plugin` | Is the honest leftover a flag, plugin, or issue on a named host? |

An Occupied company can still be a valid OSS experiment. Do not collapse those into one 0-100.

## Automatic rejects

Any one is fatal for an `as_company` Sparse/Greenfield keep:

1. A named incumbent already ships the **headline UX**.
2. The product is a 50-line GitHub Action, curl wrapper, or editor hook.
3. The core transform is mathematically non-invertible and the pitch would have to lie.
4. The remaining wedge is reverse-mapping a security control (confused deputy; rehydrating redacted secrets).
5. The remaining wedge is "add this to incumbent X" (Veln, ntfy, silo, cachelens, Pixi, OpenTofu, Cursor, ...).
6. Silent mutation of user payloads without an advisory/linter-first v1.
7. Sidecar without **host runtime enforcement** (lockfile the platform does not consult).

## Falsification (all three must hold)

A "do not build" catalog is wrong for **this seat** only if:

1. A named process or protocol sits where **no incumbent occupies** (not "add mix to Veln," not "add a checkbox to X").
2. Runtime enforcement **cannot** be a 50-line Action, hook, or curl wrap.
3. Three incumbents can still be named, and the gap is **mechanical**, not a missing checkbox.

Do not treat "the pain is real" as falsification.

## Claim hygiene vs occupancy

Unsourced or physically implausible TAM, ROI, latency, or combinatorial claims (`sub-10ms` checksum of a whale tenant, `<60s` DPOR vs O(N!)) fail **claim hygiene**.

Claim-hygiene failure does **not** by itself prove the seat is Occupied. Kill the number. Re-score the seat from named incumbents.

Price and lock-in are **not** automatically Occupied-as-glue. An expensive hypervisor product (Antithesis) occupying a nearby reliability aisle does not mean a cheaper, narrower SKU has no company. Label those incumbents `price_packaging` (see seat-match).

Roadmap on an incumbent ("we plan to ship this") is `file_on` / wait, not Sparse, when the honest move is to file or wait.

## Gates (no overall /100)

`keep` | `hold` | `drop` | `file_on`

- `keep` -- `as_company` is Sparse or Greenfield, no auto-reject, all three falsification tests hold, >=5 named incumbents (or explicit "could not find 5" plus why the problem is still real).
- `file_on` -- Occupied leftover belongs on a named incumbent.
- `hold` -- Occupied/Saturated **as a company** but the leftover is a clean plugin, OSS experiment, or follow-up seat.
- `drop` -- Occupied/Saturated **as a company** and leftover is not even a clean plugin, or an auto-reject fired and there is no file-on target; or evidence is too thin to score (`NEED_EVIDENCE` rows dominate).

Hard blocks on a keep: Occupied `as_company`; any auto-reject; missing steelman; density scores with no supporting incumbent rows; citing unread files.
