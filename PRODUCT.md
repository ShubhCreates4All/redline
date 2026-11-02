# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

Next.js, deployed on Vercel. Supabase for auth and database. Model calls go through OpenRouter — never a direct model-provider call. (Settled prior to this record; see `CLAUDE.md`.)

Supabase hosting must remain Free. The selected shared staging target and required app isolation are recorded in [docs/supabase-setup.md](docs/supabase-setup.md).

## Users

Freelancers and solo contractors who sign contracts, freelance agreements, and occasional leases or ToS repeatedly, not once — chosen over small business owners, renters, and gig workers (see ADR 0002). Built for a recurring user coming back across a career of documents, not a one-off high-stakes signer.

## Product Purpose

Given an uploaded contract/lease/freelance-agreement/ToS, produce: a plain-English summary; risk flags ranked into three severity tiers, each citing the exact source sentence it came from; a drafted counter-offer per flagged clause; a Q&A box that answers only from the document's own text; an editable list of the user's own red lines that drives the analysis; and a saved library of past documents. Success means a freelancer catches a costly clause (an enforced non-compete, an uncapped indemnification, a silent auto-renewal) before signing, not after it's already cost them.

## Positioning

Every claim is traceable: each risk flag and each "clean document" fair term quotes a verbatim source sentence checked to exist in the parsed text, so a skeptical user can verify it in seconds rather than trust it blind. Severity is assigned by financial exposure defined broadly — including foregone or restricted future income, not just direct payout — which a narrower model would systematically underrank (e.g. non-competes). The product states findings plainly with no hedging, and flags at low confidence rather than staying silent, on the belief that a missed Critical clause is a worse failure than an extra, easily-dismissed flag. It's built to beat "nothing" and a $99 flat-fee competitor (QwickContractReview), not to match attorney-grade rigor.

## Operating Context

A user uploads a document, which is parsed entirely in their browser — only the extracted text is ever sent or stored, never the original file. They review the summary and severity-ranked flags, each with its source sentence and a drafted counter-offer; ask follow-up questions in a Q&A box grounded only in the document's text; maintain an editable red-lines list (seeded with seven default clause types) that drives what gets flagged and how severely; and build a saved library of every document they've analyzed over time.

## Capabilities and Constraints

- Exactly three severity tiers (Critical, Moderate, Worth noting), never a numeric score.
- Every risk flag and every clean-document fair term must cite a source sentence that exists verbatim in the parsed document text; a flag that can't is rejected, not shown.
- No hedging language in flags, verdicts, or counter-offers; uncertainty is expressed only through tier placement, not verbal qualifiers.
- A clean document states its verdict plainly with at least one cited fair term — never an empty flag list with no accompanying statement.
- Jurisdiction-sensitive clause types (non-competes at minimum) carry an explicit "verify locally, enforceability varies by state" note. The product never collects or infers the user's jurisdiction.
- Seven default red-line clause types: auto-renewal/hard-to-cancel subscription, unilateral termination/deactivation without cure or appeal, non-compete, indemnification, IP/work-product assignment, liability caps, fee escalators. Fully user-editable; read live by analysis on every run.
- OCR for scanned documents is permanently excluded — a citation quoted from misread text breaks the citation guarantee by construction.
- No payments/billing, and no sharing a document between users, in this version.
- Undecided: exact pricing. Every price signal in the research (attorney flat-fee averages, Fiverr's price floor, the $99 competitor) is a proxy, not a stated willingness to pay for this product specifically.

## Brand Commitments

Name: Redline. No logo, tagline, or voice guide recorded yet.

## Evidence on Hand

No real Redline customer testimonials, case studies, or press exist yet — this is pre-launch. The product's own research (`research/`) cites real third-party incidents used to justify design decisions (a freelance illustrator's non-compete enforced years after the engagement; a Forbes freelancer self-funding legal defense under an indemnification clause; HRW's 2025 survey of 127 Texas gig workers; FTC auto-renewal enforcement actions) — these are evidence behind the product's decisions, not Redline's own evidence, and must not be represented as such.

## Product Principles

1. A claim with no traceable source is a bug, not a missing feature — citation is the product's core trust mechanism.
2. Financial exposure, read broadly to include foregone income, is the only severity criterion — not reversibility or power asymmetry.
3. Over-flag when uncertain rather than stay silent; a missed Critical clause is a worse failure than an extra dismissible flag.
4. State findings plainly; hedging language is banned, and uncertainty is expressed through tier alone (jurisdiction-variance disclosure is a deliberate exception, since it's information, not hedging).
5. Build for a recurring user: the red-lines list and library are the core loop, not onboarding polish.

## Accessibility & Inclusion

None established yet.
