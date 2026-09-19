# Intake (scope gate)

Load this file at step 2 when the object is not yet a restatable seat, or
when the request is a hunt. Do not load
[seat-generation.md](seat-generation.md) or
[search-playbook.md](search-playbook.md) until this gate passes.

This file answers "is the object a stack seat in a named niche yet?" --
not "how do I search incumbents?" and not "what pain is real?"

**Grill placement and constraints. Never grill pain.** Pain questions
produce slogans. Slogans are not seats.

## Gate

Pass if any one is true:

1. **Named seat.** The user named a stack position or pasted an ADR/idea
   that restates as `candidate_seat` + `v1_as_shipped` + named
   process/protocol + substrate without slogans. If only host or v1 is
   missing, ask those two, then pass. Do not run the hunt questionnaire.
   A slogan ("AI developer productivity", "SaaS for developers") is not
   a named seat -- use the hunt questionnaire. Do not drop it at
   restatement to skip grilling.
2. **Filled niche.** Hunt request plus a niche card where
   `substrate_or_stack` and `immutable_host` are **named stack nouns**
   (not "SaaS", "dev tools", "startup", "developer productivity").
   `ship_form` may be `unset`.
3. **Explicit opt-out.** The user said they do not care / pick a stack /
   use the default inventory. Fill the niche with
   `source: agent_opt_out`. Then pass.

Fail otherwise. Emit the intake card below. **Stop.** Do not generate
seats. Do not search. Do not invent a niche to be helpful.

One-shot with no reply: emit the card and stop. Do not fill blanks from
memory.

Follow-up answers merge into the same niche card. Re-run this gate. Do
not keep `intake_blocked` once `substrate_or_stack` and `immutable_host`
are named stack nouns, or the user opts out.

## Broad prompts that fail the gate

These are not seats. Do not treat them as hunt-ready:

- "give me a SaaS idea"
- "something to build" / "find a startup"
- "developer productivity tool" / "AI for X" with no stack noun
- "find vacant seats" / "hunt product seats" with no stack, host, or protocol

"SaaS" is a billing shape, not a substrate.

**Pass:** "hunt seats around Kafka; we cannot leave MSK; OSS is fine" --
named stack + named host; generate inside broker/queue and wire-proxy
family.

**Fail:** "give me a SaaS idea" -- emit the card, ask questions 1-2 at
minimum, stop.

## Questions (max 5)

Ask only blanks. Do not ask pain, TAM, why it matters, or "what problem
are you solving?"

1. **Stack / substrate.** Named stack family or protocol you will ship
   against (Postgres, Kafka, k8s, npm, GitHub merge queue). Not "SaaS"
   or "dev tools." This is not the immutable host.
2. **Immutable host.** What you cannot replace (RDS, MSK, github.com,
   the broker already in prod). Vacancy is relative to this host. "Kafka"
   alone does not fill this field; "MSK" or "the cluster we already run"
   does.
3. **Ship form.** Company, OSS, or plugin/flag. If they will not say,
   `unset`.
4. **Unique data or distribution.** Logs, schemas, install base,
   marketplace, sales motion. This is where *they* can occupy a seat.
   It is not occupancy evidence.
5. **Hard nos.** Languages, aisles, leftover shapes they will not build.
   Generation filters, not scores.

Stop asking once `substrate_or_stack` and `immutable_host` are named, or
the user opts out. Questions 3-5 never block the gate. Do not stall a
passed niche to collect them.

## Niche card (emit on fail; copy forward on pass)

```yaml
niche:
  substrate_or_stack: <named stack noun or unset>
  immutable_host: <named host they cannot replace, or unset>
  ship_form: company | oss | plugin | unset
  unique_data_or_distribution: <string or unset>
  hard_nos: []
  source: user | agent_opt_out | intake_blocked
unanswered:
  - substrate_or_stack    # required; omit once named
  - immutable_host        # required; omit once named
```

On fail: this card only. No candidate card. `source: intake_blocked`.
Ask the unanswered questions in the same turn.

On pass: copy `niche` onto every raw seat and every candidate card.

## After pass

- Named seat -> step 4 (restate).
- Filled niche or opt-out -> load [seat-generation.md](seat-generation.md).
  Generate >=5 raw seats **inside this niche**. Then `SKILL.md` steps 3-8.
- User answers never replace incumbent URLs. "Nobody does this" is not a
  row. Unique data does not raise `exact_mechanics_density`.
