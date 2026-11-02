# 05: Core analysis engine — summary + severity-ranked cited flags

**What to build:** Given a saved library document and the user's current red-lines list, produce a plain-English summary and a full set of risk flags, each assigned exactly one of three severity tiers (Critical, Moderate, Worth noting) by financial exposure — including foregone or restricted future income — and each carrying a source sentence mechanically verified to exist verbatim in the document text.

**Blocked by:** 02, 03

**Status:** ready-for-agent

- [ ] Running analysis on a saved document returns a plain-English summary
- [ ] Running analysis returns a list of risk flags, each tagged with exactly one of the three severity tiers
- [ ] Every flag's source sentence is checked to exist verbatim (exact substring) in the document's extracted text; any candidate flag that fails this check is rejected before being shown
- [ ] Severity assignment reflects financial exposure defined broadly — a fixture shaped like a non-compete with no direct payout but real restricted income lands at Critical, not a lower tier, when scope or duration meaningfully restricts future paid work
- [ ] The set of flaggable clause types matches the user's current red-lines list, read live at analysis time, not cached from an earlier session
- [ ] No flag or summary copy uses hedging language ("might," "could possibly")
