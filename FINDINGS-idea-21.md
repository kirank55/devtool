# Idea 21 — independent occupancy re-score

Object: the **seat** claimed as a keep on
[kirank55/devtool#5](https://github.com/kirank55/devtool/pull/5)
(`0208a387c8c52c17a566bf01693d9716cb5ccb5a`, “hunt batch 21-30: pitchable
found at 21”). Not the PR process.

Finder disposition (not a rater `/100`): **`file_on`**. `as_company` is
**Occupied 6**. It is **not** a Sparse/Greenfield company keep.
`keep_gate: fail`. Auto-rejects **1, 2, 5**.

PR #5 labeled every incumbent `adjacent_pain`, set
`exact_mechanics_density: 0`, `file_on: none`, `keep_gate: pass`. That
card searched only Collector docs plus one OneUptime blog (G2 miss) and
redefined the seat as “the orchestrator around `tail_sampling`” (G4/G5/G6
false keep; same labeling mistake as the calibration Occupied-bundle
cases).

## Restatement

```yaml
candidate_seat: OTel Collector per-service tail_sampling cap gate with fail-closed checked-in policy on otelcol-contrib
v1_as_shipped: otelcol-contrib binary plus checked-in sampling-policy.yaml declaring per-service spans_per_second and burst caps, consulted by the tail_sampling processor at startup; Collector refuses to start when the file is absent or incomplete; emits sampling-decision metrics
entry: restated
niche:
  substrate_or_stack: OpenTelemetry Collector contrib (tail_sampling processor)
  immutable_host: otelcol-contrib
  ship_form: unset
  unique_data_or_distribution: unset
  hard_nos: []
  source: user
slices:
  - tail_sampling processor
  - per-service cap policy (string_attribute/and + rate_limiting spans_per_second/burst_capacity)
  - fail-closed --config file gate
search_classes:
  host_primitive: OpenTelemetry Collector tail sampling processor rate_limiting spans_per_second burst_capacity and string_attribute service.name
  dropin_cli: Grafana Alloy otelcol.processor.tail_sampling; otelcol-contrib --config
  orchestrator: Honeycomb Refinery per-service sampling; Datadog Adaptive Sampling; Jaeger remote_sampling strategies.json
  tracker_leftover: tailsamplingprocessor count_traces_sampled by service.name issue 24449
verdicts:
  as_company: Occupied 6
  as_oss: Occupied 6
  as_plugin: Occupied 6
density_scores:
  problem_density: 7
  exact_mechanics_density: 3
incumbents:
  - name: OTel Collector contrib tail_sampling processor
    url: https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/processor/tailsamplingprocessor/README.md
    quote: "`rate_limiting`: Sample based on the rate of spans per second using a token bucket algorithm implemented by golang.org/x/time/rate. This allows for burst traffic up to a configurable capacity while maintaining the average rate over time."
    seat_match: exact
    leftover: YAML combining `and` + `string_attribute` on `service.name` with this `rate_limiting` policy; composite `max_total_spans_per_second` already allocates per-policy caps. Same README.
  - name: OpenTelemetry Collector --config
    url: https://opentelemetry.io/docs/collector/configuration/
    quote: "If the merger of files does not constitute a complete configuration, the user receives an error since required components are not added by default."
    seat_match: exact
    leftover: none on the fail-closed slice — missing/incomplete `--config` already refuses start (also journald: cannot load configuration / no such file or directory on contrib, issue 3097).
  - name: Grafana Alloy otelcol.processor.tail_sampling
    url: https://grafana.com/docs/alloy/latest/reference/components/otelcol/otelcol.processor.tail_sampling/
    quote: "The `rate_limiting` block configures a policy of type `rate_limiting`. The policy samples based on rate."
    seat_match: exact
    leftover: drop-in wrap of the same processor; `spans_per_second` and `burst_capacity` are first-class Alloy arguments.
  - name: OTel contrib jaegerremotesampling extension
    url: https://raw.githubusercontent.com/open-telemetry/opentelemetry-collector-contrib/main/extension/jaegerremotesampling/README.md
    quote: "This extension can be configured to proxy requests to a backing remote sampling server, which could potentially be a Jaeger Collector down the pipeline, or a static JSON file from the local file system."
    seat_match: adjacent_pain
    leftover: head-based per-service rates from a checked-in `sampling_strategies.json` on the same Collector host, not the tail_sampling processor.
  - name: Honeycomb Refinery sampling methods
    url: https://docs.honeycomb.io/manage-data-volume/sample/honeycomb-refinery/sampling-methods
    quote: "Since this is a high volume service, we use the EMA Dynamic Sampler (`EMADynamicSampler`) with a target rate of 1/50 traces."
    seat_match: adjacent_pain
    leftover: dedicated sampling proxy with checked-in `rules.yaml` per named service/environment; different host than otelcol-contrib.
  - name: Datadog Adaptive Sampling
    url: https://docs.datadoghq.com/tracing/trace_pipeline/adaptive_sampling/
    quote: "When you choose adaptive sampling as your sampling strategy, you select a target monthly volume for trace ingestion for one or more services."
    seat_match: adjacent_pain
    leftover: vendor APM per-service budget, not an otelcol processor.
  - name: tailsamplingprocessor metrics by service.name
    url: https://github.com/open-telemetry/opentelemetry-collector-contrib/issues/24449
    quote: "I would like too see metrics that are split by service.name and policy. To be able to understand who produce traffic and what rules are in use."
    seat_match: adjacent_pain
    leftover: filed enhancement for `count_traces_sampled` dimensions — auto-reject 5 / file_on the processor, not a vacant process.
auto_rejects_fired: [1, 2, 5]
falsification:
  1_vacant_process: fail
  2_not_a_wrapper: fail
  3_mechanical_gap: fail
steelman:
  occupancy_ceiling: 7
  why_build: "Strongest remaining case: hand-writing N `and` policies is verbose, so a thinner sampling-policy.yaml compiler that fail-closes on budget overflow would be nicer UX."
claim_hygiene: ok
file_on: https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/processor/tailsamplingprocessor/README.md
keep_gate: fail
deny_catalog: embedded_baseline
rate_next: not_run
```

## Why PR #5’s keep fails

| Gate | PR #5 card | This run |
| --- | --- | --- |
| G1 quotes | 5 OTel/OneUptime substrings | 7 literals from pages fetched this run |
| G2 classes | host_primitive + `--config` + OneUptime blog + “feature request” with no issue URL | class 1 `rate_limiting`/`and`/`string_attribute`; class 2 Alloy + `otelcol --config`; class 3 Refinery / Datadog / Jaeger; class 4 issue 24449 |
| G3 leftover names host | `file_on: none` while leftovers name the processor and `--config` | `file_on` the README |
| G4 vacant process | passed by calling the processor “not a gate” | **fail** — three `exact` rows |
| G5 bundle | `v1` joins processor + per-service caps + fail-closed file; scored Sparse because no one logo sells the conjunction | Occupied bundle; each slice has an `exact` or adjacent host |
| G6 auto-reject 5 | not fired | fired — leftover is YAML / metric labels on `tail_sampling` |
| G8 split | `as_plugin: Sparse 3` with named host leftovers | `as_plugin: Occupied 6` |
| G9 steelman | ceiling 4, published exact 0 | ceiling 7, published exact 3 |

Headline UX already shipped on the named host:

- Per-service match: `string_attribute` / OTTL `resource.attributes["service.name"]` / Grafana Tempo `and` + `key = "service.name"`.
- Caps + burst: `rate_limiting.spans_per_second` + `burst_capacity`; composite `max_total_spans_per_second`.
- Fail-closed file: `otelcol --config`; incomplete merge errors; contrib exits when the config path is missing.
- Decision metrics: `count_traces_sampled` (issue 24449 leftover is a label, not a processor).

That is auto-reject **1** (named incumbent is the UX), **2** (v1 is config on an existing binary), **5** (add YAML / a metric dimension to `tail_sampling`).

`as_oss` is also Occupied: a policy-YAML generator is gist-shaped on the same host.

## Pitchable?

**No, not as a company.** Rubric keep requires Sparse/Greenfield `as_company`, no auto-reject, all three falsification tests, and `keep_gate: pass`. This seat is Occupied 6 with `file_on` the tail sampling processor. Adjacent vendors (Honeycomb Refinery, Datadog Adaptive Sampling, Jaeger `service_strategies`) already sell per-service caps; they are extra problem density, not a reason to found a Collector wrapper.
