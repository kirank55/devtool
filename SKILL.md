---
name: profinder
description: >
  Find sparse developer-tool and infrastructure seats by generating stack
  positions, naming incumbents with URL plus quote, and scoring occupancy
  density. Use when asked to find, hunt, or propose product seats. Abort
  if the request is people-search (GitHub profiles, freelancers, professors).
  Do not use this skill to rate an already-chosen idea when an idea-rater
  is the requested job.
---

# Profinder

Propose and document vacant developer-tool / infrastructure seats. Score
**occupancy**, not pain. Pain is abundant. Empty seats are not.

## Constraints (every run)

- No repo writes by default.
- Do not score from memory. Load the cited reference file or emit `NEED_EVIDENCE`.
- No overall `/100`.
- Never inline rubric tables into `SKILL.md`.
- Load references **on demand by step**, not as a mandatory full stack. Do not load [search-playbook.md](references/search-playbook.md) before a seat exists. Do not load [calibration.md](references/calibration.md) unless a label is on a boundary (bundle vs slice, claim-kill vs seat-kill, false exact).
- Object is a **stack seat**, never PR hygiene. If the user pastes a PR process question, abort that object.

## Procedure

1. **Abort checks.** People-finder (GitHub profiles, freelancers, professors) -> stop; wrong skill, do not reuse these references. Request is "rate this idea / ADR" -> that is a rater job: hand off to an idea-rating skill or workflow; optionally continue only as restatement of a seat into a candidate card, never as a rater verdict.

2. **Choose entry.**
   - User named a seat or pasted an ADR/idea as a seat -> go to step 4 (restate).
   - User asked to find / hunt / propose seats -> load [seat-generation.md](references/seat-generation.md), produce >=5 raw seats, then map steps 3-8 over each.

3. **Deny check.** Load [deny-patterns.md](references/deny-patterns.md). If the target workspace keeps a local deny file, that file wins (`deny_catalog: local_adr_0001`). Else use the embedded fallback (`deny_catalog: embedded_baseline`). If both missing, `deny_catalog: incomplete` and do not emit an `as_company` keep.

4. **Restate.** One-line `candidate_seat`, concrete `v1_as_shipped`, named process or protocol, stack substrate. If this cannot be stated without slogans ("AI developer productivity"), drop the seat.

5. **Steelman ceiling.** Strongest case a skeptical founder would still build this. Occupancy ceiling 0-10 **before** search. Published `exact_mechanics_density` must not exceed this ceiling unless new named incumbent rows appear.

6. **Search incumbents.** Load [search-playbook.md](references/search-playbook.md). Collect >=5 incumbents, each with name, verified URL, exact quote, seat-match label, leftover. 404 or unverified fetch -> that row is `NEED_EVIDENCE`; do not invent.

7. **Seat-match + dual-score.** Load [seat-match.md](references/seat-match.md) then [rubric.md](references/rubric.md). One label per incumbent; strictest mismatch wins. `problem_density` counts `adjacent_pain`; `exact_mechanics_density` counts `exact` only and must be <= steelman ceiling.

8. **Gates.** Apply auto-rejects and falsification from [rubric.md](references/rubric.md). Load [calibration.md](references/calibration.md) only if needed to break a tie on a boundary case.

9. **Emit** the candidate card from [output-template.md](references/output-template.md). Split `as_company` / `as_oss` / `as_plugin`. Set `file_on` when the honest leftover is a flag, PR, or plugin. Do not emit a headline rater decision (that belongs to a rater, not the finder). Finder disposition is the split verdicts plus `file_on` plus `claim_hygiene`.
