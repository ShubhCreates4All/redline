# 0002: v1 targets freelancers, built for recurring use, priced for price-sensitive prosumers

## Decision
Redline v1 is built for freelancers and solo contractors, not small business
owners, renters, or gig workers. It is built assuming the user will come back
and sign many documents over time, not just one. It is priced (conceptually —
billing itself is out of scope this version) for someone already paying
Fiverr-gig rates ($15–90), not someone used to attorney rates ($300–461/hr).

## Alternatives
- Small business owners: the strongest *quantified* pain in the research
  (82% worry about liability, 77% reputational damage) and the highest
  willingness-to-pay, but higher-stakes commercial documents where a wrong
  flag costs more, and a worse fit for a self-serve, low-touch product.
- Renters/tenants: the single most vivid anecdote in the research (a lease
  term switched from 6 months to 1 year, caught after signing), but the
  thinnest evidence volume and the lowest recurring usage — most renters
  sign one lease a year, if that.
- Gig workers: the strongest systemic-harm evidence (HRW: 40 of 127 surveyed
  deactivated at least once), but the document in question is usually a
  platform ToS with no counterparty to send a counter-offer to — a poor fit
  for half the feature list.
- Optimizing for a one-off, high-stakes user instead of a recurring one: would
  have made the library and red-lines list "nice to have" rather than the
  core loop, undercutting the product's own scope.

## Why
Freelancers are the segment already named in the product's own scope
("freelance agreement"), have named, specific, sourced harm (Doran's
non-compete, Estevez's indemnification exposure), and a clean price anchor
($390–400 average professional review). More importantly, a freelancer signs
contracts repeatedly — the only segment among the four where a saved library
and an editable, reusable red-lines list compound in value instead of being
used once and forgotten.

## Consequences
- This is explicitly not the best-evidenced pain in the research (that's
  small business owners) — the brief should say so, not imply Redline chased
  the strongest signal.
- The most vivid single story in the research (the renter's bait-and-switch
  lease) will not be the launch story; freelancer stories are real but less
  visceral, so marketing and onboarding copy need to work harder.
- Feature and UX decisions should default to rewarding repeat use (the
  library, the red-lines list) over polishing a single first-run experience.
- Confidence and tone should be pitched to beat "nothing" and a $99
  competitor (QwickContractReview), not to satisfy someone who already
  pays attorney rates — see round three's confidence-calibration decision.
