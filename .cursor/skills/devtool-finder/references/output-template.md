# Output template (finder candidate card)

Headline is a **candidate**, not a rater decision. No overall `/100`. Do not emit a headline rater verdict (that belongs to a rater, not the finder).

Do not emit this card when the scope gate failed. That path emits the niche card in [intake.md](intake.md) only. `niche` here is copied from a passed gate (or derived on a named-seat restatement). Unique data is copied verbatim; it does not move density scores.

```yaml
candidate_seat: <one-line stack position>
v1_as_shipped: <concrete v1 and stack placement>
entry: generated | restated

niche:
  substrate_or_stack: <named stack noun>
  immutable_host: <named host they cannot replace>
  ship_form: company | oss | plugin | unset
  unique_data_or_distribution: <string or unset>
  hard_nos: []
  source: user | agent_opt_out

slices: [<mechanism>, ...]        # split v1 on "and"; required when v1 is a conjunction

search_classes:                   # four classes from search-playbook.md; queries run this hunt
  host_primitive: <query>
  dropin_cli: <query>
  orchestrator: <query>
  tracker_leftover: <query>

verdicts:
  as_company: <Greenfield|Sparse|Occupied|Saturated> <0-10>
  as_oss:     <Greenfield|Sparse|Occupied|Saturated> <0-10>
  as_plugin:  <Greenfield|Sparse|Occupied|Saturated> <0-10>

density_scores:
  problem_density: <0-10>          # counts adjacent_pain
  exact_mechanics_density: <0-10>  # exact only; <= steelman.occupancy_ceiling

incumbents:
  - name: <tool>
    url: <verified URL>
    quote: "<contiguous substring of that page, fetched this run>"
    seat_match: exact | adjacent_pain | language_scoped | wrong_substrate | obsolete | price_packaging
    leftover: <what is missing if this row is exact>

auto_rejects_fired: []            # ids from references/rubric.md
falsification:
  1_vacant_process: pass | fail
  2_not_a_wrapper: pass | fail
  3_mechanical_gap: pass | fail

steelman:
  occupancy_ceiling: <0-10>
  why_build: "<strongest case for building>"

claim_hygiene: ok | unsourced | implausible
file_on: <incumbent repo/issue URL, or none>
keep_gate: pass | fail            # pass required for as_company Sparse/Greenfield; see keep-gate.md
deny_catalog: local_adr_0001 | embedded_baseline | incomplete
rate_next: <not_run | compose_next>   # reminder only: hand a candidate to an idea-rater, never inline a rater verdict
```

Seat-match labels match `references/seat-match.md` (six labels).
`keep_gate: fail` forbids `as_company` Sparse/Greenfield. Default company verdict is Occupied or `file_on`.
