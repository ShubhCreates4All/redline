# 0003: Severity is three tiers, ranked by financial exposure (including foregone income)

## Decision
Every risk flag gets one of three severity tiers — Critical, Moderate, Worth
noting — assigned primarily by financial exposure: how much money the user
stands to lose, directly or as foregone future income, if the clause plays
out against them. All seven clause types the research identified are
flaggable in v1, including liability caps and fee escalators, which have zero
documented real-world disputes behind them (only law-firm hypotheticals).

## Alternatives
- Two tiers (flag / don't flag): simpler, but collapses "this could bankrupt
  you" and "this is annoying but survivable" into the same signal.
- A continuous 1–10 score: more granular, but implies a precision the model
  can't actually back up, and invites the user to argue the number instead of
  the substance.
- Reversibility (can the harm be undone) or power asymmetry (can the other
  party act unilaterally) as the primary criterion instead of financial
  exposure: both map cleanly onto real evidence (non-compete duration,
  gig-worker deactivation) but are harder to compress into a plain-English
  flag than "this could cost you $X."
- Excluding liability caps and fee escalators from v1, or flagging them at
  reduced confidence, since the research found no real disputes for either.

## Why
Financial exposure is the criterion a freelancer can most easily act on —
"this could cost you $X" is immediately legible in a way "this is
irreversible" or "this is asymmetric" are not. It also matches the two
best-evidenced harms directly: the indemnification case (a freelancer
self-funding her own legal defense) and the auto-renewal case ($2,500+ over
nine years) are both, at bottom, stories about uncapped or compounding
financial exposure. Flagging the two weakly-evidenced clause types anyway is
a bet that press coverage tracks *visibility*, not *harm* — an uncapped
liability clause likely gets resolved quietly, not through an FTC action.

## Consequences
- "Financial exposure" must be implemented broadly — it includes foregone or
  restricted future income, not just money a clause could force the user to
  pay out directly. Read narrowly, a non-compete clause has no direct payout
  and would systematically under-rank, even though it's one of the sharpest
  pieces of freelancer-specific evidence in the research. This is a
  deliberate, load-bearing interpretation, not an implementation detail.
- Liability-cap and fee-escalator flags will have no real-world magnitude
  data to calibrate a financial-exposure estimate against, unlike
  auto-renewal or indemnification. This is a direct input into the
  confidence-calibration decision (see ADR 0004) — the model is more likely
  to overstate confidence here than anywhere else in the severity model.
- Every flag's severity must be justified in terms a user can check against
  the source sentence (see ADR 0001) — "Critical" or "Moderate" is not
  enough on its own; the reasoning has to name the dollar amount or the
  income at risk.
