# Output template (finder candidate card)

Headline is a **candidate**, not a rater decision. No overall `/100`. Do not emit a headline rater verdict (that belongs to a rater, not the finder).

```yaml
candidate_seat: <one-line stack position>
v1_as_shipped: <concrete v1 and stack placement>
entry: generated | restated

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
    quote: "<docs/README quote>"
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
deny_catalog: local_adr_0001 | embedded_baseline | incomplete
rate_next: <not_run | compose_next>   # reminder only: hand a candidate to an idea-rater, never inline a rater verdict
```

Seat-match labels match `references/seat-match.md` (six labels).
