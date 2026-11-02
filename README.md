Production: [redline-black-mu.vercel.app](https://redline-black-mu.vercel.app)

# Redline

Redline analyzes contracts, leases, freelance agreements, and terms of service.
This repository currently contains product plans and research. It does not yet
contain the Next.js application.

The Vercel project `redline` is connected to `ShubhCreates4All/redline` on GitHub.
Pushes to `main` trigger production deployments.

## Production settings

These four settings must be set on Vercel for Production and in the gitignored
`.env.local` file. No values belong in this README.

| Setting | Vercel Production | `.env.local` |
| --- | --- | --- |
| `NEXT_PUBLIC_SUPABASE_URL` | Missing | Missing |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Missing | Missing |
| `OPENROUTER_API_KEY` | Missing | Missing |
| `OPENROUTER_MODEL` | Missing | Missing |

All four settings were absent during setup and were skipped. Configure them
before using the application, then push to `main` to rebuild with the settings.
