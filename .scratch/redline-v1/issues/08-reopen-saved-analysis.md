# 08: Reopen saved analysis from the library

**What to build:** A signed-in user can reopen a past library entry and see its previously computed summary, flags (with counter-offers and any jurisdiction notes), and clean verdict where applicable, without re-running analysis.

**Blocked by:** 06, 07

**Status:** ready-for-agent

- [ ] Analysis results (summary, flags, counter-offers, clean verdict) are persisted onto the library entry they were run against
- [ ] Opening a past library entry displays its stored results directly, with no new model call triggered
- [ ] One user cannot see another user's library entries or their stored analysis results
