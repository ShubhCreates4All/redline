# Redline

Contract / lease / freelance-agreement / ToS analyzer. Given an uploaded document, it produces: a plain-English summary, risk flags ranked by severity (each showing the exact source sentence), a drafted counter-offer per flagged clause, a Q&A box that answers only from the document, an editable list of the user's own red lines that drives the analysis, and a saved library of past documents.

## Stack (settled — do not reconsider)
- Next.js, deployed on Vercel.
- Supabase for auth and database.
- For Supabase provisioning, auth, migrations, or deployment configuration, follow `docs/supabase-setup.md`: use the existing free staging project shared with Trippal, with separate Redline data and access rules. Keep Supabase on Free.
- Model calls go through OpenRouter — never call a model provider directly.

## Non-negotiable invariants
- The uploaded file is parsed in the browser. Only the extracted text is ever stored — never the original file.
- Every risk flag must show the exact source sentence it came from. A flag with no traceable source is a bug, not a missing feature.
- The Q&A box, and every claim the product makes, must be grounded only in the document's own text. Where the text doesn't support a claim, don't make it.

## Scope for this version — build these six, then stop
1. Plain-English summary
2. Risk flags ranked by severity, each with its source sentence
3. A drafted counter-offer per flagged clause
4. Document-grounded Q&A box
5. Editable red-lines list that drives the analysis
6. Saved library of past documents

Excluded on purpose, do not add without asking: payments/billing, OCR for scanned documents, sharing a document between users. OCR would actively break the citation guarantee above — a citation to misread text is worthless. If something looks like the obvious next step and isn't one of the six, ask before building it.

## Standing rules
- Secrets live in .env.local, which is gitignored. Never commit a secret — it's public the moment it's pushed and has to be rotated.
- Ask before adding a dependency.

## Read before deciding or building
- research/summary.md — the user research behind what this product should do.
- PRD.md (once it exists) — the brief; read it before building.

## Agent skills

### Issue tracker

Issues and specs live as markdown files under `.scratch/`. See `docs/agents/issue-tracker.md`.

### Triage labels

Default five-role vocabulary (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`), recorded as a `Status:` line in each issue file. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: `CONTEXT.md` (once it exists) + `docs/adr/` at the repo root. See `docs/agents/domain.md`.

### Grilling

When running a grilling/interview skill (e.g. grill-me) in this project, always ask via multiple-choice options rather than open-ended free-text questions.
