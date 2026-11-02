# 07: Clean verdict and jurisdiction-sensitivity disclosure

**What to build:** Two extensions to the analysis engine's output: (1) when a document has no critical issues, return a plain "no critical issues" verdict with at least one specific fair term cited the same way a risk flag is — never an empty flag list with no accompanying statement; (2) any flag on a jurisdiction-sensitive clause type (non-competes at minimum) carries an explicit note that enforceability varies by state and the user should verify locally, without the product ever collecting or inferring the user's jurisdiction.

**Blocked by:** 05

**Status:** ready-for-agent

- [ ] Analyzing a fixture document with no critical issues returns a plain clean verdict, not an empty flag list
- [ ] That clean verdict includes at least one fair term with its own verbatim-checked source sentence
- [ ] Every flag on a jurisdiction-sensitive clause type (non-competes at minimum) includes a "verify locally, enforceability varies by state" note
- [ ] No part of the flow asks the user for their state or location
