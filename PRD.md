# Redline — Brief (v1)

## Who this is for, specifically, and what they do today instead

Freelancers and solo contractors — people who sign contracts, freelance
agreements, and occasional leases or ToS repeatedly, not once. Not small
business owners, not renters, not gig workers; see "The calls I made" below
for why each is excluded and who that leaves worse off.

Today, this person does one of four things: signs without reading it
closely, because reading a contract carefully takes time they're not billing
for; pays a flat fee for an attorney review, averaging $390–400
(ContractsCounsel, 34 projects); pays $15–90 for an ad hoc review on Fiverr —
evidence that a price-sensitive version of this need already has a market;
or uses a free template tool (Rocket Lawyer, LawDepot) that helps them
*draft* a document but was never built to catch risk in one someone else
handed them. A fifth option now exists too: QwickContractReview.com, a
$99 flat-fee AI review service targeting this exact segment — direct
validation that the price point and framing work, and direct competition.

## The problem

> "[Freelance creators repeatedly turn down future work] because they were
> 'so intimidated'" by a non-compete clause buried in a past contract —
> including a former client who tried to enforce a seven-year non-compete
> four years after a brief freelance engagement.
> — Colleen Doran, illustrator (research/who-has-the-pain.md, via
> https://colleendoran.substack.com/p/the-none-compete-clause)

The harm here isn't that the clause was unreadable — it's that nobody was
still watching for it by the time it mattered. The same pattern shows up in
Forbes freelancer Dolia Estevez, left to self-fund her own legal defense
under her contract's indemnification clause, and in Human Rights Watch's
2025 survey of 127 Texas gig workers, where 40 had been deactivated at least
once under a unilateral-termination clause and nearly half of those were
later cleared of the thing that got them deactivated — the clause let the
platform act first and ask questions never. A freelancer signs dozens of
these over a career. Redline exists because reading closely once isn't the
failure mode; forgetting to keep watching is.

## What the first version does

1. Plain-English summary of the uploaded document.
2. Risk flags ranked by severity, each showing the exact source sentence it
   came from.
3. A drafted counter-offer for each flagged clause.
4. A Q&A box that answers only from the document's own text.
5. An editable list of the user's own red lines that drives the analysis.
6. A saved library of past documents.

Nothing beyond this list ships in v1. If something looks like the obvious
next step and isn't on this list, it gets asked about before it gets built
(see CLAUDE.md).

## What good looks like

These are the specific, checkable claims a later test pass should hold this
product to:

- **Every flag's source sentence exists verbatim in the uploaded text.**
  Checkable mechanically: quote-match the cited sentence against the parsed
  document. A flag that fails this check is a bug (ADR 0001), not a rare
  edge case to tolerate.
- **Severity tier matches financial exposure, broadly defined.** Given
  Doran's non-compete case as a test input, the flag should land at
  Critical — because the exposure is foregone future income, not a direct
  payout (ADR 0003). A financial-exposure-blind severity call (e.g. ranking
  a non-compete "Moderate" because no money changes hands up front) is a
  failure of the model, not an acceptable judgment call.
- **A clean document gets a plain, specific "no critical issues" verdict**
  with at least one cited fair term — never a bare empty flag list, which
  reads as "didn't look" rather than "looked, and it's fine" (ADR 0004).
- **Every non-compete flag (and any other jurisdiction-sensitive clause
  type) names that enforceability varies by state**, without collecting or
  guessing the user's actual jurisdiction (ADR 0005).
- **The Q&A box refuses to answer what the document doesn't say.** Asked a
  question the text has no basis for, it says so — it does not infer, guess,
  or fill the gap from general contract knowledge.
- **A counter-offer references the specific clause it's countering** and
  proposes concrete replacement language, not just "negotiate this."
- **Editing a red line changes future analysis without a rebuild** — the
  red-lines list is read by the analysis, not a static preference that gets
  ignored after onboarding.

## My red lines: which clauses I flag, how severely, and why

All seven clause types the research surfaced are flagged in v1, ranked by
financial exposure (ADR 0003), including two with no documented real-world
disputes — flagged anyway on the bet that press silence reflects privacy,
not safety.

1. **Auto-renewal / hard-to-cancel subscription clauses — Critical by
   default.** The single most-evidenced harm in the research (FTC actions,
   a NYC law passed in response, a live lawsuit): a subscriber's business
   debit card was charged for nine years, over $2,500 total, after they
   believed they'd cancelled. Compounding, easy-to-miss financial exposure —
   the clearest possible case for the top tier.
2. **Unilateral termination / account deactivation — Critical if it removes
   income without cure or appeal.** HRW's Texas gig-worker data (40 of 127
   deactivated at least once, nearly half later cleared) shows this isn't
   rare, and there's no way to contest it after the fact — the clause lets
   the other side act first.
3. **Non-compete clauses — Critical if scope or duration meaningfully
   restricts future paid work.** Doran's evidence is the reason this segment
   was chosen at all (see "The calls I made"). Flagged as
   jurisdiction-sensitive per ADR 0005: enforceability swings from binding
   to void depending on the state, so severity is stated alongside a
   verify-locally note, not asserted as if one law applied everywhere.
4. **Indemnification clauses — Critical whenever liability is uncapped.**
   The Estevez/Forbes case is the starkest evidence in the whole set of what
   this looks like realized: a freelancer self-funding her own legal
   defense because her contract made her responsible for the client's
   exposure, not just her own work.
5. **IP / work-product assignment — Moderate to Critical, scaled by how much
   of the freelancer's reusable work it reaches.** Losing rights to a
   one-off deliverable is different from losing rights to a framework used
   across every client relationship; the second is closer to losing a
   business asset. Confidence here is lower than the four above — the only
   concrete anecdote in the research comes from a contract-advice site, not
   journalism.
6. **Liability caps (or their absence) — Moderate by default, with no
   real-world magnitude to calibrate against.** No documented dispute was
   found for this clause type — only law-firm hypotheticals — so severity is
   an estimate, not a pattern-matched judgment the way auto-renewal's is.
   This is the clause type most likely to produce an overconfident-sounding
   flag; see ADR 0003's consequences.
7. **Fee escalators — Worth noting by default.** Least evidenced clause
   type in the research (explainer content only, zero real disputes) — kept
   in scope because it's cheap to check and plausible to matter, not because
   evidence demands it.

## The calls I made and what I gave up

| Choice | Chosen against | Who's worse off |
|---|---|---|
| Freelancers as the segment | Small business owners — the single *best-quantified* pain in the research (82% worry about liability, 77% reputational, backed by real attorney-rate data) | Small business owners get nothing from v1, despite having the strongest numbers behind them |
| Built for a recurring user | A one-off, high-stakes user with no history | Someone who will only ever sign one document (a renter with a single lease) gets a product tuned for reuse features — the library, the red-lines list — they'll never benefit from |
| Priced for a price-sensitive prosumer | A higher-budget professional used to attorney rigor | Anyone expecting output rigorous enough to anchor a high-stakes negotiation; this product is built to beat "nothing" and a $99 competitor, not to beat a lawyer |
| Flag liability caps and fee escalators despite zero documented disputes | Restricting v1 to only the clause types the research actually evidences | Trust, if either flag turns out overconfident — there's no real dispute data to calibrate the estimate against, unlike the other five clause types |
| Three severity tiers, not a continuous score | A power user who wants to precisely rank many flags against each other to decide what to fight for first | That user gets ties (several "Critical" flags with no ordering between them) instead of a ranked list |
| Financial exposure (incl. foregone income) as the only severity criterion | Reversibility or power-asymmetry as the criterion | A clause that's dangerous for a non-financial reason — say, a data-privacy overreach with no clear dollar figure — is likely to underrank under this model, even though it wouldn't under a reversibility- or asymmetry-based one |
| Over-flag when uncertain | Staying quiet until confident | A user who gets enough low-value "Worth noting" flags to start skimming past all of them, including the ones that mattered — the tier system is meant to prevent this, but doesn't guarantee it |
| State findings plainly, no verbal hedging | Hedging explicitly when the model is unsure | A user in a genuinely ambiguous case gets a flatly stated judgment with no signal that the model itself wasn't sure — they have to infer uncertainty from the citation alone |
| Say "clean" plainly rather than always surfacing a low-tier finding | Always showing at least one flag to feel consistently useful | The product has less to visibly "show for itself" on a fine document — a plain clean verdict is less inherently convincing than a caught mistake, even when it's the honest answer |
| Flag jurisdiction-sensitivity, don't collect the user's state | Asking for jurisdiction up front and adjusting severity precisely | A freelancer whose state makes a flagged clause a non-issue (or a much bigger issue) still has to go verify that themselves — the product tells them to check, not what they'd find |

## What we are not building, and why

- **Payments/billing.** Not one of the six. Adding it now would mean
  building monetization before the analysis itself is proven trustworthy —
  the thing this version exists to establish.
- **OCR for scanned documents.** Actively excluded, not just deprioritized:
  a citation quoted from misread text is a citation to something that isn't
  actually in the document, which defeats the entire premise of ADR 0001.
  OCR doesn't get safer with more engineering here — it's incompatible with
  the citation guarantee by construction.
- **Sharing a document between users.** Not one of the six, and every one of
  Redline's six features is designed around a single user's own documents
  and their own red lines — sharing raises access and consent questions this
  version has no design for.
- **Collecting the user's jurisdiction.** Considered directly (ADR 0005),
  not just left off the original list — real scope growth (a new input, a
  state-law dataset to build and maintain) for a version whose job is to
  prove the core analysis works, not to be state-law-precise from day one.

## What the research could not tell us

- **What a freelancer would actually pay for this product specifically.**
  Every price signal in the research is a proxy — attorney flat-fee
  averages ($390–400), Fiverr's price floor ($15–90), a direct competitor's
  price ($99) — not a stated willingness to pay for *this*, and payments are
  out of scope this version regardless (see above).
- **Reddit was unreachable this session for all four research passes.**
  Given how much freelancer, tenant, and gig-worker discourse plausibly
  lives there, this is a real hole in the evidence base, not a formality —
  research/summary.md flags it as worth a manual spot-check before anything
  built here gets treated as fully validated.
- **No gig-worker-specific spend data, renter-specific "I'd pay $X" quotes,
  or early-employee offer-letter pricing** beyond the general $420
  employment-contract average — these remain open questions the research
  didn't answer, not segments it ruled out.
- **Whether stated desire converts to actual paid usage at all.** The one
  hard adoption data point found — MetLife's legal-benefit enrollment — is
  discouraging: 78% call the benefit a "must-have," yet only 6–8% enroll
  even at $14–27/month via payroll deduction, with no separate purchase
  decision required. This doesn't invalidate the segment choice, but it's a
  direct caution against assuming stated pain will convert to usage, whatever
  Redline eventually charges.
- **Liability caps and fee escalators have no documented real disputes
  behind them at all** — only law-firm marketing hypotheticals. The research
  could not confirm these clause types actually hurt freelancers in
  practice; flagging them anyway (see "My red lines") is a bet the research
  itself cannot back up.
