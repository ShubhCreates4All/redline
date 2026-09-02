# Redline — Glossary

## Severity tiers
Every risk flag is one of exactly three tiers — never a numeric score, never
a binary flag/no-flag. See ADR 0003.

- **Critical** — high financial exposure, direct or foregone-income.
- **Moderate** — real but lesser exposure.
- **Worth noting** — one-sided or unusual, but not dangerous by the
  financial-exposure test.

## Financial exposure
The severity criterion behind all three tiers (ADR 0003). Defined broadly:
money the user could be forced to pay out **or** income they stand to lose
by being restricted from earning it (e.g. a non-compete). Read narrowly —
direct payout only — it undercounts clauses like non-competes that have no
upfront cost but a real income cost later. Always read broadly in this repo.

## Jurisdiction-sensitive clause
A clause type (non-competes especially) whose real-world danger depends on
which state's law governs it — the same clause can be binding or largely
unenforceable depending on the user's location. Redline doesn't collect
jurisdiction in v1; these clauses get an explicit "verify locally" note
instead of a jurisdiction-blind severity claim. See ADR 0005. This is a
deliberate exception to the no-hedging rule (ADR 0004): naming jurisdiction
variance is information, not hedging.

## Clean document
The intended positive result of a review, not the absence of one: no
critical issues found, stated plainly, with at least one specific fair term
named and cited the same way a risk flag is (ADR 0001, ADR 0004). Never an
empty flag list with no accompanying statement — that reads as "didn't
look," not "looked, and it's fine."
