# Redline v1 — Spec

Status: ready-for-agent

## Problem Statement

Freelancers and solo contractors sign contracts, freelance agreements, and occasional leases or ToS repeatedly, not once. Today they either sign without reading closely (because careful reading takes unbilled time), pay $390–400 for a full attorney review, pay $15–90 for an ad hoc Fiverr review, or use a drafting tool (Rocket Lawyer, LawDepot) that was never built to catch risk in a document someone else handed them. The harm isn't that a clause was unreadable in the moment — it's that nobody was still watching for it by the time it mattered: a non-compete enforced years after a brief engagement, an indemnification clause that leaves a freelancer self-funding a client's legal defense, a unilateral-termination clause that cuts off income with no appeal.

## Solution

Upload a document and get: a plain-English summary; risk flags ranked into exactly three severity tiers (Critical, Moderate, Worth noting), each showing the exact source sentence it came from; a drafted counter-offer attached to every flagged clause; a Q&A box that answers questions using only the document's own text and refuses when the text doesn't support an answer; an editable list of the user's own red lines that actively drives which clauses get flagged and how severely; and a saved library of past documents so the analysis compounds across a freelancer's whole career of contracts, not just one.

## User Stories

1. As a freelancer, I want a plain-English summary of an uploaded contract, so that I understand what I'm agreeing to without reading full legal text.
2. As a freelancer, I want every risk flag to show the exact sentence it came from, so that I can verify the flag against the real document instead of trusting a paraphrase.
3. As a freelancer, I want risk flags ranked into Critical / Moderate / Worth noting, so that I know what to fight for first instead of treating every flag as equally urgent.
4. As a freelancer, I want severity to reflect financial exposure — including income I'd lose from a restriction like a non-compete, not just money I could be forced to pay out — so that a clause with no upfront cost but real income cost still lands at the tier it deserves.
5. As a freelancer, I want a non-compete clause that meaningfully restricts my future paid work flagged as Critical, so that a clause with no direct payout isn't underranked just because no money changes hands up front.
6. As a freelancer, I want an indemnification clause with uncapped liability flagged as Critical, so that I don't discover after signing that I'm on the hook for a client's legal exposure.
7. As a freelancer, I want an auto-renewal or hard-to-cancel subscription clause flagged as Critical by default, so that I don't get silently charged for years after I believed I'd cancelled.
8. As a freelancer, I want a unilateral-termination or deactivation clause with no cure or appeal path flagged as Critical when it removes my income, so that I understand the other party can act first and I have no way to contest it after the fact.
9. As a freelancer, I want an IP/work-product assignment clause scaled between Moderate and Critical based on how much of my reusable work it reaches, so that losing rights to a one-off deliverable is distinguished from losing rights to a framework I reuse across clients.
10. As a freelancer, I want liability caps (or their absence) flagged at Moderate by default, so that I'm alerted to a real gap even where there's no dispute history to calibrate exact severity against.
11. As a freelancer, I want fee escalator clauses flagged at "Worth noting" by default, so that a cheap-to-check, plausible-to-matter clause type isn't skipped just because it's the least evidenced.
12. As a freelancer, I want every flag on a jurisdiction-sensitive clause type (non-competes especially) to say plainly that enforceability varies by state and I should verify locally, so that I'm not given a severity that silently assumes a jurisdiction I'm not in.
13. As a freelancer, I do not want to be asked for my state or location anywhere in this flow, so that using the product doesn't require handing over information the product isn't designed to act on precisely anyway.
14. As a freelancer, I want a drafted counter-offer attached to every flagged clause, so that I have concrete replacement language to send back instead of just being told something is risky.
15. As a freelancer, I want each counter-offer to reference the specific clause it's countering, so that I'm not handed generic "negotiate this" advice with nothing to act on.
16. As a freelancer reviewing a genuinely clean document, I want a plain "no critical issues" verdict with at least one specific fair term cited the same way a risk flag is, so that I can tell the difference between "this looks fine" and "the tool didn't actually look."
17. As a freelancer, I never want to see an empty flag list with no accompanying statement, so that silence never gets mistaken for a clean bill of health.
18. As a freelancer, I want flags and verdicts stated plainly with no hedging language ("might," "could possibly"), so that the citation — not vague qualifiers — is what I use to judge the model's confidence.
19. As a freelancer facing genuine uncertainty about whether something is worth flagging, I want the tool to flag it anyway at an appropriately low tier rather than stay silent, so that a real risk is never missed just because the model wasn't fully sure.
20. As a freelancer, I want a Q&A box where I can ask follow-up questions about the uploaded document, so that I don't have to re-read the whole thing to check one detail.
21. As a freelancer, I want the Q&A box to answer strictly from the document's own text, so that I'm never given an answer that sounds authoritative but isn't actually grounded in what I signed.
22. As a freelancer, I want the Q&A box to explicitly say when the document doesn't address my question, so that I don't mistake a gap in the contract for a gap in the tool's attention.
23. As a freelancer, I want to see and edit my own list of red lines (the clause types I care about and how I want them treated), so that the analysis reflects my own priorities, not just a fixed default set.
24. As a freelancer, I want the seven default red-line clause types (auto-renewal, unilateral termination, non-compete, indemnification, IP assignment, liability caps, fee escalators) pre-populated when I first use the product, so that I start from a sensible baseline instead of a blank list.
25. As a freelancer, I want an edit to my red lines to change the very next analysis I run, so that updating my preferences doesn't require waiting on a rebuild or reload of anything behind the scenes.
26. As a freelancer, I want every document I've uploaded and analyzed saved to a library I can come back to, so that my past reviews aren't lost the moment I close the tab.
27. As a freelancer, I want to reopen a past document's summary, flags, and counter-offers from my library, so that I can refer back to a past negotiation without re-uploading and re-analyzing the file.
28. As a freelancer, I want only the extracted text of my document stored — never the original file — so that my documents aren't retained in a form the product isn't designed to keep safely.
29. As a freelancer, I want my uploaded file parsed in my own browser before anything is sent anywhere, so that the raw file itself never has to leave my machine.
30. As a freelancer, I want my red lines and my library to be private to my own account, so that another user of the product can never see documents or preferences I haven't chosen to share (sharing itself is out of scope — see Out of Scope).

## Implementation Decisions

- **Three modules, matching three seams:**
  1. **`analyzeDocument(text, redLines)`** — takes the browser-extracted document text and the user's current red-lines list, returns the plain-English summary, the full set of risk flags (each with severity tier, verbatim source sentence, and an attached counter-offer), or, when nothing critical is found, a clean verdict carrying at least one cited fair term. This single call/module is the source of features 1, 2, 3, and the clean-document behavior — the counter-offer is produced alongside its flag, not as a separate downstream pass, since it depends on the same source-sentence context.
  2. **`answerQuestion(text, question)`** — takes the document text and a user question, returns either a grounded answer or an explicit refusal. Kept separate from `analyzeDocument` because it's interactive and per-question rather than one-shot batch, and its grounding rule is stricter: refuse rather than infer, with no exception.
  3. **A persistence layer** for the user's own data: an editable red-lines repository (read by `analyzeDocument` on every run, not cached from onboarding) and a document library repository (extracted text plus the results of the most recent `analyzeDocument` run, keyed to the authenticated user). No model call involved; this is plain CRUD.
- **Stack** (already settled, not reopened here): Next.js on Vercel; Supabase for auth and both repositories above; all model calls route through OpenRouter, never a direct provider call.
- **Parsing boundary:** the uploaded file is parsed client-side in the browser. Only the extracted text ever crosses into `analyzeDocument`, `answerQuestion`, or the persistence layer — the original file is never transmitted or stored.
- **Citation contract:** every flag and every clean-verdict fair term carries a source sentence that must exist verbatim (exact substring) in the parsed document text. `analyzeDocument` output that doesn't parse into valid (flag, source sentence) pairs — or whose source sentence fails a verbatim check — is rejected, not shown to the user.
- **Severity model:** exactly three tiers (Critical, Moderate, Worth noting), never a numeric score. Assigned primarily by financial exposure, defined broadly to include foregone or restricted future income (e.g. a non-compete), not just direct payout. Each flag's severity reasoning must name the dollar amount or income at risk in terms checkable against the cited sentence.
- **Jurisdiction handling:** clause types marked jurisdiction-sensitive (non-competes at minimum) get an explicit "enforceability varies by state, verify locally" note attached to the flag. The product never collects or infers the user's jurisdiction anywhere in the flow.
- **Confidence and error preference:** no hedging language in any flag, verdict, or counter-offer copy. When the model is uncertain whether something is worth flagging at all, it flags it (typically at "Worth noting") rather than staying silent. A clean document always states its verdict plainly with a real cited fair term — never an empty flag list with no accompanying statement.
- **Red-lines list:** seeded with the seven default clause types (auto-renewal/hard-to-cancel subscription, unilateral termination/deactivation without cure or appeal, non-compete, indemnification, IP/work-product assignment, liability caps, fee escalators) and their default severity postures from the brief. Fully editable per user, and read live by `analyzeDocument` on every invocation.
- **Library:** stores extracted text plus the analysis output (summary, flags, counter-offers) per document, scoped to the authenticated user via Supabase auth. No cross-user access; no sharing surface.

Supabase hosting and app isolation must follow [docs/supabase-setup.md](../../docs/supabase-setup.md). The user selected the existing Free project shared with Trippal staging. No paid upgrade is authorized.

## Testing Decisions

- Test only external behavior at each seam — input in, output or persisted state out — never internal prompt text or which model was called.
- **`analyzeDocument`:** fixture-based tests using sample contract texts (including a non-compete scenario shaped like the Doran case, which must land Critical, and a clean-document fixture with at least one genuinely fair term). For every flag produced, mechanically assert the cited source sentence is a verbatim substring of the fixture text — a flag that fails this check is a failing test, independent of whether the flag's content is otherwise reasonable. Separately assert: severity tier matches the financial-exposure model on known scenarios; the clean-document branch never returns an empty flag list without a verdict statement; jurisdiction-sensitive clause types include the verify-locally note; no flag or verdict string contains hedging language.
- **`answerQuestion`:** fixture pairs of (document text, question) covering both a grounded case (answerable from the text) and a refusal case (no basis in the text) — assert the refusal case returns an explicit refusal, never a fabricated or general-knowledge answer.
- **Persistence layer:** standard repository tests — create/edit/list a red line and confirm the next `analyzeDocument` call reflects the edit; create/list library entries; assert cross-user isolation (one user's repository calls never return another user's rows); assert only extracted text is ever persisted, never raw file bytes.
- No existing test suite in this greenfield repo to follow as prior art — these three seams set the pattern going forward.

## Out of Scope

- Payments/billing, in any form.
- OCR for scanned documents — permanently excluded, not deferred: a citation quoted from misread text breaks the citation contract by construction.
- Sharing a document, red-lines list, or library entry between users.
- Collecting or inferring the user's jurisdiction as an input; jurisdiction-sensitive clauses are disclosed per-flag instead.
- Anything not one of the six features above (plain-English summary, severity-ranked cited flags, per-flag counter-offers, grounded Q&A, editable red lines, saved library).

## Further Notes

- Built for a recurring user (a freelancer signing many documents over time), not a one-off high-stakes user — the red-lines list and library are core loop, not optional polish.
- Tone and confidence are calibrated to beat "nothing" and a $99 flat-fee competitor, not to match attorney-grade rigor.
- Secrets live in `.env.local` only (gitignored); no new dependency gets added without asking first.
