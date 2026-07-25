# 402 Sentinel

**Status: concept — nothing built yet. Gauging demand before writing code.**

A self-serve scanner for x402 sellers. Point it at your own x402 payment endpoint and it tests for five known settlement-layer failure patterns, returning pass / warn / fail on each:

| # | Check | Why it matters |
|---|---|---|
| 1 | Non-idempotent webhooks | The same settlement event processed twice means double fulfillment |
| 2 | Mempool-only confirmation | An unconfirmed transaction treated as settled |
| 3 | Over-broad wallet allowances | Approvals wider than the payment actually needs |
| 4 | Laggy-indexer trust | State decisions running on stale, lagging indexer data |
| 5 | Unbounded retry windows | Retries with no cap or expiry, opening replay and race conditions |

## Why this exists

These failure patterns are documented across the x402 ecosystem, but the current answer is bespoke review — someone reads your code or you find out in production. There's no self-serve, automatable way to check your own endpoint and get a concrete result.

402 Sentinel would be that: a scanner (CLI or hosted), not a consulting engagement. Run it yourself, get pass/warn/fail per check, fix what fails, run it again.

## Current stage

This is at demand validation. Whether it gets built depends on whether people running real x402 endpoints say they'd use it. If that's you, two questions:

1. Would you actually run this against an endpoint you operate?
2. Would you be willing to point an early version at a real endpoint (test or production)?

Answer in the linked discussion, or open an issue here. A "no, because…" is as useful as a yes.

## Who's behind it

Built by [Tomboj](https://github.com/rtomboj). Small tool, honest scope.
