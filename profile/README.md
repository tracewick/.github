<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/tracewick-lockup-on-dark.svg">
    <source media="(prefers-color-scheme: light)" srcset="assets/tracewick-lockup-on-light.svg">
    <img alt="Tracewick" src="assets/tracewick-lockup-on-light.svg" width="420">
  </picture>
</p>

<p align="center">
  <strong>Always-on, low-overhead production profiler for PHP.</strong><br>
  Flame graphs from live traffic, built on <a href="https://www.mediawiki.org/wiki/Excimer">ext-excimer</a>.
</p>

---

### What it is

Tracewick samples your PHP application while it serves real requests and turns those samples into
flame graphs you can act on. It is designed to stay enabled in production on high-load services:
sampling is cheap, the overhead is bounded, and the profiler is fail-open, so a problem inside
Tracewick never breaks, blocks or noticeably slows down your application.

### Why

Most performance problems only show up under real traffic, with real data and real concurrency.
Staging profiles and one-off traces miss them. Tracewick gives you continuous, low-cost visibility
into where production time actually goes, per endpoint and per release.

### Status

🚧 **Early development, pre-alpha.** APIs, formats and package names may still change. The first
tagged release will be an alpha.

### Projects

| Project | Description | Status |
|---|---|---|
| `tracewick/tracewick` | Core PHP library: sampling, aggregation and export | Coming soon |
| `tracewick/symfony-bundle` | Symfony integration | Planned |
| `tracewick/laravel` | Laravel integration | Planned |
| Agent | Collector and forwarder written in Go | Planned |

All Tracewick projects are open source under the Apache License 2.0.
