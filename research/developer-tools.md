# Developer Tools Research — devtool branch

Branch: `devtool` | Date: 2026-09-18 | Method: primary-source only (official docs fetched this run)

> Scope: bounded map of major dev-tool/infra categories in 2026 to support devtool-finder seat-hunting. Every factual claim below traces to a primary source fetched this run. Unverifiable items are marked `NEED_EVIDENCE`.

## 1. CI/CD — GitHub Actions
- Homepage/docs: https://docs.github.com/en/actions
- What it does: workflow automation inside the repo for CI/CD and custom jobs.
- Quote (contiguous substring, fetched 2026-09-18):
  > "Automate, customize, and execute your software development workflows right in your repository with GitHub Actions."
- Seat-match note: crowded aisle — native CI plus marketplace actions; sparse seats would need to be a specific leftover (e.g. provenance/attestations, ARC scale-sets), not "better CI".

## 2. Containers — Docker Docs
- Homepage/docs: https://docs.docker.com/
- What it does: learn/install/use Docker products for building and running containers.
- Quote:
  > "Docker Documentation helps you learn Docker, install Docker products, and find reference material for everyday development and operations tasks."
- Adjacent 2026 signal from same page: Sandboxes / Build Cloud / Hardened Images are the active surface (e.g. "Sandboxes created with version 0.43.0 mount shared agent skills read-only by default").
- Seat-match note: crowded core; thin edges around agent sandboxes + hardened-image supply chain.

## 3. Orchestration — Kubernetes Docs
- Homepage/docs: https://kubernetes.io/docs/home/
- What it does: `NEED_EVIDENCE` — this run's fetch returned nav tree only (truncated), no definitional sentence captured. Do not cite a definition without re-fetching https://kubernetes.io/docs/concepts/overview/components/ .
- Fetched evidence: docs tree contains Concepts / Tasks / Tutorials / Cluster Administration / Scheduling / Security — confirms scope is container orchestration + cluster ops.
- Seat-match note: `NEED_EVIDENCE` for any density claim; treat as Occupied by default per devtool-finder fail-closed rule.

## 4. IaC — Terraform (HashiCorp Developer)
- Homepage/docs: https://developer.hashicorp.com/terraform/docs
- What it does: infrastructure as code across low- and high-level resources.
- Quote:
  > "Terraform is an infrastructure as code tool that lets you build, change, and version infrastructure safely and efficiently."
- Seat-match note: crowded for generic IaC; sparse only in named provider/registry gaps with literal user quotes.

## 5. IDE / Agent editor — VS Code Docs
- Homepage/docs: https://code.visualstudio.com/docs
- What it does: editor + agent harness (chat, agents window, customizations, MCP, hooks).
- Quote:
  > "Hand off tasks to autonomous AI agents that iterate until the job is done."
- Seat-match note: extremely crowded (editor + Copilot + extensions + MCP). Finder disposition should be `file_on` (plugin/extension) unless a named stack seat with empty exact-mechanics exists.

## 6. AI coding assistant — GitHub Copilot Docs
- Homepage/docs: https://docs.github.com/en/copilot/about-github-copilot (landing fetched: https://docs.github.com/en/copilot/about-github-copilot via redirect to get-started)
- What it does: AI assistance across IDE, GitHub.com, CLI, SDK.
- Quote (from get-started landing fetched this run):
  > "Learn how to sign up for and use GitHub Copilot."
- Seat-match note: `NEED_EVIDENCE` for capability claims — re-fetch the About page for a definitional quote before scoring. Treat as Occupied.

## 7. Observability — Prometheus Docs
- Homepage/docs: https://prometheus.io/docs/introduction/overview/
- What it does: systems monitoring and alerting; time-series metrics + PromQL + pull model.
- Quotes:
  > "is an open-source systems monitoring and alerting toolkit originally built at"
  > "Prometheus collects and stores its metrics as time series data, i.e. metrics information is stored with the timestamp at which it was recorded, alongside optional key-value pairs called labels."
- Seat-match note: crowded for metrics core; thin in OTel bridge, Perses dashboards, long-term storage UX — needs separate seat restatement + search.

## 8. Testing (e2e) — Playwright Docs
- Homepage/docs: https://playwright.dev/docs/intro
- What it does: end-to-end test framework + runner + tooling for modern web apps.
- Quote:
  > "Playwright Test is an end-to-end test framework for modern web apps."
- Supporting fact from same page:
  > "By default tests run headless in parallel across Chromium, Firefox and WebKit"
- Seat-match note: crowded for cross-browser e2e; sparse only in named leftover (e.g. trace-viewer triage, flake-sharding for a specific stack).

## Sparse-seat hints (evidence-only, not verdicts)
- Crowded (do not propose as company without keep-gate pass): generic CI, generic containers/K8s, generic IaC, generic IDE, generic AI completion, generic metrics, generic e2e.
- Thin edges worth a proper devtool-finder hunt (each needs intake → 5+ seats → 4-class search before any keep): agent sandbox reproducible envs (`sbxenv.yaml`-style), hardened-image/VEX + attestations verification, Actions Runner Controller self-host ops, Terraform provider gaps in a named niche, PromQL→Perses migration UX, Playwright trace/flake triage as a seat (not PR hygiene).
- Devtool-finder rule reminder: `as_company` defaults to Occupied / `file_on`; Sparse/Greenfield requires `keep_gate: pass` with literal quotes + mandatory search classes.

## Sources (all fetched this run, 2026-09-18)
1. https://docs.github.com/en/actions
2. https://docs.docker.com/
3. https://kubernetes.io/docs/home/
4. https://developer.hashicorp.com/terraform/docs
5. https://code.visualstudio.com/docs
6. https://docs.github.com/en/copilot/about-github-copilot
7. https://prometheus.io/docs/introduction/overview/
8. https://playwright.dev/docs/intro
