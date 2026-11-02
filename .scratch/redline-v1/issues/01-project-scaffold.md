# 01: Project scaffold

**What to build:** A deployed Next.js application on Vercel with Supabase authentication wired up, and one proven round-trip call to a model through OpenRouter. From the user's perspective: visit the app, sign in, and the app can successfully reach a model.

**Blocked by:** None (can start immediately)

**Status:** ready-for-agent

- [ ] A user can sign up / sign in via Supabase auth and reach an authenticated area of the app
- [ ] The deployed app successfully round-trips a call through OpenRouter (never a direct model-provider call) and displays a result, proving the model-calling path works end-to-end
- [ ] Secrets (Supabase keys, OpenRouter key) are read from environment variables and are never committed
- [ ] No unauthenticated user can reach the authenticated area

## Supabase hosting decision

Use the existing Free project shared with Trippal staging, not Trippal production. Follow [the setup requirements](../../../docs/supabase-setup.md) before provisioning or wiring authentication. A new organization does not provide an extra active free project slot.

- [ ] Redline targets the documented shared staging reference and Supabase remains on Free
- [ ] Redline has a dedicated schema, server-controlled app membership, and RLS; anonymous and Trippal-only accounts have no Redline data access
- [ ] Redline-only accounts have no Trippal staging data or privileged RPC access; existing Trippal objects and access rules remain intact
- [ ] Shared Auth callbacks and Redline-specific browser sessions work for both apps; user data operations enforce RLS without a project-wide service-role client

These requirements are pending implementation and verification; this ticket remains open.
