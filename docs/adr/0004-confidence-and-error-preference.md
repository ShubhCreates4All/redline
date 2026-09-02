# 0004: Over-flag when uncertain, state findings plainly, say so when a document is clean

## Decision
When the model is unsure how serious a clause is, it still states its
judgment plainly — no verbal hedging ("this might possibly be a concern").
The source-sentence citation (ADR 0001) is the hedge; the user checks the
text and judges for themselves. Given genuine uncertainty about whether
something is worth flagging at all, the model flags it — at the appropriate
tier, usually "Worth noting" rather than "Critical" — rather than staying
silent. When a document has no real issues, the model says so plainly and
names one specific fair term with its own source sentence, rather than
manufacturing a "Worth noting" item to seem consistently useful.

## Alternatives
- Hedge explicitly when confidence is low ("we're not certain, but..."):
  more honest about the model's own uncertainty, at the cost of the
  confident, actionable tone the product depends on.
- Stay quiet when uncertain rather than over-flag: protects against
  crying-wolf fatigue, but risks the exact failure the citation guarantee
  exists to prevent — a costly clause Redline said nothing about.
- Always surface at least one low-severity finding, even on a clean
  document, to keep the product feeling consistently useful.

## Why
A missed Critical clause is a freelancer signing something costly with
Redline having said nothing — that is a worse failure than an extra flag
that costs the user 30 seconds to read and dismiss. The three-tier severity
model (ADR 0003) is what makes over-flagging survivable: weak or uncertain
concerns land at "Worth noting," not "Critical," so volume doesn't imply
danger. And a tool that always finds a problem stops being believed, which
protects nobody — even the flags it gets right lose their power once the
user has learned to discount them.

## Consequences
- Prompting and output parsing must support a real "no critical issues"
  result with a positive-finding citation, not just an empty flag list —
  an empty list reads as "the model didn't look," not "the model looked and
  it's fine."
- No flag may ship without a severity tier and a source sentence, even a
  low-confidence one — "uncertain" changes the tier, not whether it's shown.
- Copy and UI must never use hedging language ("might," "could possibly")
  to express model uncertainty; certainty is expressed only through tier
  placement.
