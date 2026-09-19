---
name: devtool-finder
description: >
  Find sparse developer-tool and infrastructure seats by niching the stack
  first, then generating positions, naming incumbents with URL plus quote,
  and scoring occupancy density. Fail closed: as_company defaults to Occupied
  or file_on; Sparse/Greenfield company keeps must pass keep-gate (literal
  quotes, mandatory search classes, no occupied bundle). Use when asked to
  find, hunt, or propose product seats, including broad "SaaS idea" or
  "something to build" prompts -- those must be grilled into a named stack
  and host before generation or search; do not invent a niche. Do not use
  for vertical-workflow SaaS seats on a named system of record (that is a
  SaaS-finder job). Abort if the request is people-search (GitHub profiles,
  freelancers, professors). Do not use this skill to rate an already-chosen
  idea when an idea-rater is the requested job.
---

# Devtool finder

Propose and document vacant developer-tool / infrastructure seats. Score
**occupancy**, not pain. Pain is abundant. Empty seats are not.

## Constraints (every run)

- No repo writes by default.
- Do not score from memory. Load the cited reference file or emit `NEED_EVIDENCE`.
- No overall `/100`.
- Never inline rubric tables into `SKILL.md`.
- Load references **on demand by step**, not as a mandatory full stack. Do not load [intake.md](references/intake.md) unless step 2 needs the scope gate. Do not load [seat-generation.md](references/seat-generation.md) or [search-playbook.md](references/search-playbook.md) before that gate passes. Do not load [search-playbook.md](references/search-playbook.md) before a seat exists.
- Scoring files are not optional. Load [calibration.md](references/calibration.md) before the first 0-10 score. Load [keep-gate.md](references/keep-gate.md) before any `as_company` Sparse/Greenfield. Do not skip either because the keep "looks clear."
- Quotes are contiguous substrings of a page fetched this run. Paraphrase is `NEED_EVIDENCE`.
- `as_company` **defaults to Occupied or `file_on`**. A Sparse/Greenfield company keep is fail-closed and requires `keep_gate: pass`.
- Object is a **stack seat**, never PR hygiene. If the user pastes a PR process question, abort that object.
- This skill is self-contained under `.cursor/skills/devtool-finder/`. Load only files in this tree. Do not load sibling skill trees (e.g. niche-saas-finder / SaaS-finder playbooks).
- User-supplied niche, unique data, and "nobody does this" scope generation. They are not occupancy evidence and do not replace incumbent URLs.

## Procedure

1. **Abort checks.** People-finder (GitHub profiles, freelancers, professors) -> stop; wrong skill, do not reuse these references. Vertical-workflow SaaS hunt on a named system of record (Clio, Eaglesoft, Toast, ServiceTitan) -> stop; wrong skill, do not reuse these references. Request is "rate this idea / ADR" -> that is a rater job: hand off to an idea-rating skill or workflow; optionally continue only as restatement of a seat into a candidate card, never as a rater verdict.

2. **Choose entry / scope gate.** A slogan is not a seat. Do not generate or search until the object is a named stack position.
   - User named a seat or pasted an ADR/idea that already restates without slogans -> go to step 4 (restate). Do not load intake.
   - User named a seat that cannot be restated without slogans ("AI developer productivity") -> treat as an incomplete hunt. Load [intake.md](references/intake.md). Do not drop at restatement to skip grilling.
   - User named a restatable seat but `v1_as_shipped` or host is missing -> load [intake.md](references/intake.md) (named-seat branch), ask only those blanks, then step 4. Do not search until restatable.
   - User asked to find / hunt / propose seats -> load [intake.md](references/intake.md). If the niche card is incomplete and the user did not opt out, emit the intake card and **stop**. Do not load seat-generation or search-playbook. Do not invent a niche.
   - Hunt with a filled niche, or explicit "pick a stack" opt-out -> load [seat-generation.md](references/seat-generation.md), produce >=5 raw seats **inside that niche**, then map steps 3-9 over each. On `agent_opt_out`, if the first two restated seats hit `exact` class-1/2 hosts **named in** [calibration.md](references/calibration.md) or `.docs/killed-seats.md` (any row; the table is the working closed-aisle list, not a parenthetical sample), **switch substrate** from the inventory rather than emitting five more Occupied cards in that aisle.

3. **Deny check.** Load [deny-patterns.md](references/deny-patterns.md). If the target workspace keeps a local deny file, that file wins (`deny_catalog: local_adr_0001`). Else use the embedded fallback (`deny_catalog: embedded_baseline`). If both missing, `deny_catalog: incomplete` and do not emit an `as_company` keep.

4. **Restate.** One-line `candidate_seat`, concrete `v1_as_shipped`, named process or protocol, stack substrate. Copy `niche` from intake (named-seat path may derive it from the restatement; `source: user`). If **this candidate** cannot be stated without slogans ("AI developer productivity"), drop the seat. If the *user request* is still a slogan, return to step 2; do not end the hunt by dropping.

5. **Steelman ceiling.** Strongest case a skeptical founder would still build this. Occupancy ceiling 0-10 **before** search. If `v1_as_shipped` joins two or more mechanisms with "and", list those **slices** first; the ceiling is at least the densest occupied slice. Published `exact_mechanics_density` must not exceed this ceiling unless new named incumbent rows appear.

6. **Search incumbents.** Load [search-playbook.md](references/search-playbook.md). Hit all four mandatory query classes, then collect >=5 incumbents, each with name, URL fetched this run, contiguous-substring quote, seat-match label, leftover. 404, unverified fetch, or paraphrase -> that row is `NEED_EVIDENCE`; do not invent. Do not stop at five adjacent logos.

7. **Seat-match + dual-score.** Load [calibration.md](references/calibration.md) (before the first 0-10), then [seat-match.md](references/seat-match.md), then [rubric.md](references/rubric.md). One label per incumbent; strictest mismatch wins. `problem_density` counts `adjacent_pain`; `exact_mechanics_density` counts `exact` only and must be <= steelman ceiling.

8. **Gates.** Apply auto-rejects and falsification from [rubric.md](references/rubric.md). Load [keep-gate.md](references/keep-gate.md). A Sparse/Greenfield `as_company` keep requires `keep_gate: pass`. On `keep_gate: fail`, emit Occupied / `file_on` / `drop` as the company verdict even if leftover prose is eloquent.

9. **Emit** the candidate card from [output-template.md](references/output-template.md), including the `niche` block, `slices`, `search_classes`, and `keep_gate`. Split `as_company` / `as_oss` / `as_plugin`. Set `file_on` when the honest leftover is a flag, PR, or plugin. Do not emit a headline rater decision (that belongs to a rater, not the finder). Finder disposition is the split verdicts plus `file_on` plus `claim_hygiene` plus `keep_gate`. Do not emit this card when step 2 stopped on `intake_blocked`. Do not emit `as_company` Sparse/Greenfield when `keep_gate` is `fail`.
