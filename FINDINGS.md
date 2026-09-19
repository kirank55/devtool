# Devtool research findings — 2026-09-19

Target: solo / indie devs. Model: any best opportunity. Constraint: none.

## Signals (fetched this run)

- Agent bill shock: unattended `/loop` ~$6k (r/ClaudeAI, Apr 2026); Uber maxed 2026 AI budget in 4 months; some engineers $2k/mo; Claude Code Review $15–25/PR.
- Review trust gap: green CI can lie when the PR edits its own checks. "Proof beats diffs" — ProofShot (HN), AgentProof min-score gate, Stage chapters, Spotlight session reports, Flux replay.
- Token waste: Paritok claims ~85% cut in saturated sessions, 447M tokens compressed over 2 weeks.
- Payments pain (repeat): 2–3 weeks on auth + Stripe; full setup = products/prices, webhooks, portal, entitlements, failed payments, test vs live (r/webdev Mar 2026).
- Stack cost: ~$744/mo before product code — Clerk ~$25 + Stigg ~$249 + Knock ~$250 + LaunchDarkly ~$120 + Customer.io ~$100 + 5-dashboard glue (r/SideProject Jun 2026).
- AI credits billing is precision work: midpoint failure refunds, double-fire, concurrent drain, downgrade leftovers — AI-written handlers lose real money (r/SideProject May 2026).
- Indie monitoring: DeepTracer $19/mo guardian pitch vs Pingoni 0 customers after 6 months building a Datadog-alt. Lesson: sell "sleep through the night", not "cheap Datadog".

## Longlist (11)

1. Agent runaway cap + estimate
2. Proof bundle for agent UI/PR (video + logs + console in viewer.html)
3. AI review cost / re-review multiplier saver
4. AI credits ledger (refund-safe)
5. Stripe completeness auditor/fixer (not another starter)
6. Indie $744-stack killer (auth + billing + notify + flags in one)
7. Solo guardian monitoring (errors + uptime + LLM cost, Slack plain-English)
8. Prod-bug replayer for Next.js
9. Refactor equivalence checker (`equiv` in CI)
10. Local agent memory with conflict UI
11. Token compressor local

## Shortlist (pain / pay / gap / build-fit, 0-10)

1. Solo Agent Cost Guard — 9 / 9 / 8 / 9. Pre-run estimate + hard per-task cap in request path, kill retry storms.
2. Proof Bundle for PRs — 9 / 7 / 8 / 9. Agent records browser + console + server logs to single `proof.html` on PR. No pass/fail, just evidence.
3. AI Credits Ledger — 8 / 9 / 9 / 7. Deduct/refund/idempotency/concurrency-correct credits lib + Stripe handlers.
4. Stripe Completeness Fixer — 8 / 8 / 7 / 8. `npx stripe-audit`: missing webhook cases, portal, entitlements sync, test/live drift, generates patches.
5. Solo Guardian — 7 / 8 / 6 / 8. 5-line middleware: error grouping + uptime + LLM spend + throttled Slack with fix. Must be $19 all-in-one.

## Top picks

### #1 Solo Agent Cost Guard
- MVP: CLI proxy + `max_iterations` + budget file + HTTP 429 on cap + Slack alert.
- Pricing: free local, $19/mo pro with history + team caps.
- First 10 users: Claude Code / Cursor solo devs on X, r/ClaudeAI, HN.
- Why: invoice pain acute, monthly repeat, enforcement > dashboard still missing for solo.

### #2 Credits Ledger + Stripe Fixer combo
- MVP: Postgres ledger with `deduct/refund` idempotency keys + downgrade proration + tests; `stripe-audit` scanner.
- Pricing: OSS lib + $29–69 paid audit/patches.
- First 10 users: r/SideProject AI builders hitting refund bugs.
- Why: same buyer as #1, direct money-loss pain starters skip.

## Next
- Draft MVP specs for #1 and #2.
- Validate with 5 solo-dev interviews before code.
