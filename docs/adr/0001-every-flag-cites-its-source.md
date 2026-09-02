# 0001: Every risk flag cites its source sentence

## Decision
Every risk flag Redline produces must show the exact sentence from the uploaded
document it was derived from. A flag that cannot point to a source sentence is
treated as a bug in the system, not a formatting gap to clean up later.

## Alternatives
- Let the model describe the risk in its own words, with no quoted text, the
  way a human summarizer would.
- Show a paraphrase alongside an approximate location (e.g. "around section
  3") instead of the literal sentence.
- Cite a source sentence only when the model is confident, and fall back to an
  unsourced flag otherwise.

## Why
A flag with a quoted source sentence is something the user can check against
the actual document in seconds — they read the sentence, judge it themselves,
and either trust the flag or catch the model being wrong. A flag stated only
in the model's own words asks for trust with nothing to verify it against, and
a wrong or hallucinated risk becomes indistinguishable from a real one. The
citation is what lets a skeptical user, or Redline itself, catch a mistake
before it costs anyone something.

## Consequences
- The model cannot be prompted to just "explain the risks" — every flag's
  generation must be structured to return a locatable source sentence, and
  outputs that don't parse into (flag, source sentence) pairs are rejected
  rather than shown.
- This is also why OCR is out of scope for this version: a source sentence
  quoted from misread text is a citation to something that isn't actually in
  the document, which defeats the point of citing at all.
- Testing needs fixtures that check the quoted sentence exists verbatim in the
  source text, not just that a flag was produced — flag quality and citation
  correctness are two separate things to test.
- It rules out any future feature that summarizes risk in the aggregate
  without traceability, such as a single overall risk score with no
  per-sentence backing.
