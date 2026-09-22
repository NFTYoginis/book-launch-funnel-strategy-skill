# The locked-token launch pattern

A reusable answer to a specific, common launch problem: everything about a launch is ready except one external dependency that hasn't landed yet. Read directly from `GabeYoga-HQ/Detox Book/launch/LAUNCH-STATUS.md`, a real launch that shipped this way.

## The problem this solves

A book launch routinely has one genuinely blocking external dependency — most often, the sales page doesn't exist yet, so there's no URL to point a buy CTA at. The naive response is to wait: hold every asset until the dependency resolves, then write all the CTA copy at once. This wastes the time the dependency takes to resolve — every other piece of the launch (emails, cards, pitches, captions) could have been finished in parallel.

## The pattern

1. **Identify the single unknown.** Usually one thing: a URL. Occasionally a date, a price, or a name not yet finalized.
2. **Build everything else to completion**, with the one unknown represented as a single, consistently-named placeholder token (e.g. `{{BUY_URL}}`) everywhere it would otherwise appear.
3. **Track every file that carries the token.** The real trail's own count: 8 files, each with a buy CTA, all using the identical token.
4. **When the dependency resolves, run one find-and-replace pass** across every file carrying the token — a single mechanical swap, not a re-write.
5. **Verify with a zero-remaining check.** Grep for the token string across the whole launch tree; a clean launch shows zero matches. The real trail's own instruction: *"Verify with a grep that zero `{{BUY_URL}}` tokens remain."*

## Why this beats waiting or guessing

Waiting wastes the parallel time the dependency's resolution takes. Guessing at the eventual URL (or shipping a placeholder link that goes live prematurely) risks a broken or wrong CTA reaching a real reader. The locked-token pattern gets the full time-value of building everything else in parallel, while guaranteeing the swap is mechanical, complete, and independently verifiable — a grep either confirms zero tokens remain or it doesn't, with no ambiguity about whether the swap actually finished.

## What NOT to do with this pattern

- **Don't use more than one token for the same unknown.** A launch with `{{BUY_URL}}` in some files and a hand-typed placeholder URL in others defeats the verification step — the grep can't catch what it isn't looking for.
- **Don't skip the zero-remaining verification.** A swap that "should have" hit every file is not the same as a swap confirmed to have hit every file. Run the grep; don't assume.
- **Don't use this pattern for more than one genuinely blocking unknown at a time** without naming each token distinctly. Two unresolved unknowns sharing one token (or two similarly-named tokens easy to confuse) reintroduces the ambiguity the pattern exists to remove.

## Worked reference — the real swap

The real launch had every asset finished — 8 files, each carrying a buy CTA — while the actual sales page was still being built by another worker. Rather than waiting, the launch shipped copy-ready with `{{BUY_URL}}` standing in everywhere a buy link belonged. Once the sales page's real URL existed, one session ran the find-and-replace across all 8 files and confirmed completion with a grep for the token — zero remaining, swap complete, nothing missed and nothing left half-done.
