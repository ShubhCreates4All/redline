# 0005: Flag jurisdiction-sensitive clause types explicitly, don't collect jurisdiction

## Decision
Redline does not ask the user's state or adjust severity by jurisdiction in
v1. Instead, when a flagged clause type is known to vary significantly in
enforceability by state (non-competes especially), the flag says so
explicitly — e.g. that enforceability varies by state and the user should
verify locally — rather than staying silent on the gap or asserting a
severity that assumes one jurisdiction.

## Alternatives
- Ignore jurisdiction entirely, one blanket disclaimer somewhere in the UI:
  cheapest, but risks a "Critical" flag on a clause that's actually
  unenforceable where the user lives — actively wrong, not just incomplete.
- Ask the user's state up front and adjust severity accordingly: most
  accurate, but real scope growth beyond the six features in this version —
  a new input, a state-law dataset to build and maintain, and a new way for
  the product to be wrong that doesn't exist today.

## Why
A non-compete is largely unenforceable in California but binding in most
other states — the same clause text deserves a different severity depending
on where the freelancer is based, and the research's non-compete evidence
(Doran, the HRW gig-worker data) doesn't distinguish jurisdictions either.
Naming the gap per-flag costs no new input, no dataset, and no new scope,
while a silent blanket disclaimer still lets a wrong-for-this-state severity
reach the user unchallenged.

## Consequences
- The clause-type list needs a jurisdiction-sensitivity marker (non-competes
  at minimum) that the flag-generation prompt checks before asserting
  severity with full confidence.
- This is a deliberate, named exception to ADR 0004's "state findings
  plainly, no hedging" rule: jurisdiction variance is a real, specific
  uncertainty (not generic model doubt), so naming it is information, not
  hedging.
- If a future version adds jurisdiction as an input, this ADR is the record
  of why v1 shipped without it — see CLAUDE.md: ask before building the
  obvious next step.
