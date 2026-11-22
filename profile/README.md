<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/tracewick-lockup-on-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="assets/tracewick-lockup-on-light.svg">
    <img alt="Tracewick" src="assets/tracewick-lockup-on-light.svg" width="420">
  </picture>
</p>

<p align="center">
  <strong>Continuous sampling profiles for PHP.</strong><br>
  Flame graphs from live traffic, built on <a href="https://www.mediawiki.org/wiki/Excimer">ext-excimer</a>.
</p>

---

### What it is

Tracewick samples PHP stacks with ext-excimer and exports wall-time or CPU profiles to
Grafana Pyroscope. Applications write a local spool; the Go agent handles aggregation,
pprof encoding and network delivery outside the request path. The library bounds its work
and reports runtime failures through diagnostics.

### Why

Most performance problems only show up under real traffic, with real data and real concurrency.
Staging profiles and one-off traces miss them. Tracewick gives you continuous, low-cost visibility
into where production time actually goes, per endpoint and per release.

### Status

**Core and agent `1.0.0-rc.1` are published.** These are release candidates for 1.0,
not final stable releases. Pin candidate versions explicitly and read the migration notes
when upgrading from 0.2. The core supports PHP **8.2–8.5**; sampling requires ext-excimer.

The Symfony bundle's published `0.2.0` requires core `^0.2`. Support for core 1.0 is
pending [bundle PR #25](https://github.com/tracewick/symfony-bundle/pull/25), including
installation and upgrade checks against the actual published RC. The
[Flex recipe](https://github.com/symfony/recipes-contrib/pull/2116) is awaiting upstream review.

### Projects

| Project | Description | Status |
|---|---|---|
| [tracewick/tracewick](https://github.com/tracewick/tracewick) | PHP sampling, runtimes and local spool | [1.0.0-rc.1](https://github.com/tracewick/tracewick/releases/tag/v1.0.0-rc.1) |
| [tracewick/agent](https://github.com/tracewick/agent) | Recommended delivery sidecar; Linux amd64/arm64, binaries and GHCR | [1.0.0-rc.1](https://github.com/tracewick/agent/releases/tag/v1.0.0-rc.1) |
| [tracewick/symfony-bundle](https://github.com/tracewick/symfony-bundle) | HTTP, Console and opt-in Messenger integration | [0.2.0](https://github.com/tracewick/symfony-bundle/releases/tag/v0.2.0); core 1.0 support pending |
| [tracewick/benchmarks](https://github.com/tracewick/benchmarks) | Reproducible overhead, accuracy, recovery and soak evidence | Published reports and raw data |

Laravel integration remains planned. Automatic OpenTelemetry trace/span correlation is
deferred with no target release.

### Delivery and installation

Use the [core quick start](https://github.com/tracewick/tracewick#quick-start) to write
spool v2, then follow the [agent installation guide](https://github.com/tracewick/agent#install).
Run one normal reader per spool with compatible UID/GID. Delivery is at least once;
spool admission is soft, so operators set disk limits through volumes or quotas.
PHP `tracewick-drain` remains supported for cron, one-shot delivery and as a reference reader.

The RC releases include SBOMs and keyless signatures. Verification instructions:
[core](https://github.com/tracewick/tracewick/blob/main/docs/verify-release.md) ·
[agent archives and images](https://github.com/tracewick/agent/blob/main/deploy/verify-release.md).
Composer does not verify these signatures automatically. Agent RC images have versioned
tags and do not replace the stable `latest` image.

### Measured results

- [72-hour RoadRunner + agent soak](https://github.com/tracewick/benchmarks/blob/main/reports/2026-11-22-soak-rr-agent-72h.md):
  2,592,001 requests at 10 RPS, no HTTP failures or reported profiler drops;
  PHP worker RSS and CPU per request remained stable in that run.
- [Current-development campaign](https://github.com/tracewick/benchmarks/blob/main/reports/2026-11-22-development-runtime.md):
  three equal-work baseline/on pairs measured a median **+0.462% PHP CPU per request**
  at sample rate 0.1, plus recovery and real Symfony delivery checks.

Reports record exact source pins, workloads and limitations. The campaigns use different
revisions; these measurements are not universal overhead or leak-free guarantees.

All Tracewick projects are open source under the Apache License 2.0.
