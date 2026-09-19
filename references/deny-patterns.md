# Deny patterns

Short catalog of collapse modes. Not a substitute for a full killed-seats table. A previous kill is a deny-list entry, not a scoring template (prior-kill-as-rubric): do not condense another project's killed-seats tables into this file as the working catalog.

## Local deny file (optional)

If the target workspace keeps its own killed-seats file (for example `docs/adr/0001-no-pitchable-candidate.md`), its tables are authoritative (`deny_catalog: local_adr_0001`). Confirm the candidate's one-line seat against those rows before scoring; a match stops the run with a pointer to that row.

If no such file exists, use the embedded baseline below (`deny_catalog: embedded_baseline`).

`deny_catalog: incomplete` only if neither a local deny file nor this fallback is available. That is not the happy path.

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

Fuller aisles (same rule -- closed unless a mechanical gap appears): advisory prompt-cache inspectors, vendor API contract drift seats, universal offline SQL mutation upcast (non-invertible; reject), PTY secret reverse-map (confused deputy; reject), agent sandbox / FS / secrets / MCP wraps the host already ships, package-manager-shaped lock/integrity seats the platform absorbed.

## Priors are not a rubric

A previous kill is a deny-list entry, not a scoring template. Do not use closed-aisle leftovers as generation seeds. Re-search **this** seat. Name **this** seat's incumbents. Seat-match those rows.
