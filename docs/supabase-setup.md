# Supabase setup for Redline

## Decision recorded November 1, 2026

Keep Supabase on the Free plan. The user chose to share the existing Trippal staging project, with separate Redline tables and access rules. No paid plan, paid branch, or paid add-on is authorized.

| Purpose | Project | Use for Redline |
| --- | --- | --- |
| Shared Trippal staging and Redline | redline, `gkklvsgivoznjxkxlwng` | Yes, subject to the implementation checks below |
| Trippal production | Trippal, `ehkykivnqqbtzgeiqbkn` | No |

Organization: DeeprInnovation, currently Free. Redline's intended Supabase URL is `https://gkklvsgivoznjxkxlwng.supabase.co`.

Both hosted projects were healthy in the dashboard when checked. The staging project already contains Trippal tables. Redline is still a planning/prototype repository with no application scaffold. This records the target and requirements; it does not claim that Redline tables, credentials, auth configuration, or a deployment have been created.

## Workshop checklist checked November 1, 2026

The workshop instructions describe creating a dedicated project. The user selected an existing shared Free project instead, so no third project was created.

| Workshop item | Shared project result |
| --- | --- |
| Project name `redline` | Renamed the dashboard display name from ShubhCreates4All's Project to `redline`. Project reference and URL remain unchanged. It still serves Trippal staging. |
| Leave GitHub empty | The existing ShubhCreates4All/Trippal connection was retained for the shared staging setup. No Redline GitHub connection was added. This differs from a blank new-project form. |
| Generate database password | The existing project already has a password. No password was generated or reset. Redline's planned client uses the publishable key and a signed-in user's session, not a database password. |
| Nearest region | The existing region is East US (Ohio), `us-east-2`. It was retained; moving regions is separate migration work. No nearest-region claim has been verified against a user-supplied location. |
| Enable Data API | Verified on in Integrations > Data API > Overview. |
| Automatically expose new tables | Verified on in Integrations > Data API > Settings. No toggle or access grants were changed. |
| Create and leave open | Reused the existing project and left its Data API settings tab open. No paid plan or new project was created. |

The automatic-exposure switch concerns default grants for new tables in `public`; Redline is planned in the custom `redline` schema. Redline migrations must still include explicit schema/table grants, RLS, and policies together, and expose the custom schema only once secured. Do not rely on the switch to make custom-schema saves work. The repository has no application database files yet, so a signed-in save cannot be tested until the scaffold and persistence work are implemented.

Supabase's [April 28 changelog](https://supabase.com/changelog/45329-breaking-change-tables-not-exposed-to-data-and-graphql-api-automatically) schedules explicit grants for newly created public tables across existing projects from October 30, 2026. Although this project's dashboard still shows the switch on, explicit grants are the dependable implementation requirement. This does not change the observed switch state or claim its underlying defaults have been tested.

## Why a new organization does not add capacity

Supabase allows two active free projects across organizations where the account is an Owner or Administrator. Creating another Free organization does not add a third active free project. Paused projects do not count, but pausing this shared project would stop both Redline and Trippal staging.

Stay within the Free plan's quotas. Check current usage before launching. Free projects may pause after a week of inactivity. If a limit blocks progress, report it and use local development or reduce usage; an upgrade is not the fallback. The no-upgrade decision applies to Supabase and does not establish a budget for OpenRouter.

## Requirements for ticket 01 and persistence work

1. Verify the project reference before every migration or environment change. Redline must target `gkklvsgivoznjxkxlwng`. Preserve existing Trippal tables, functions, grants, and records. Use additive, reviewed migrations scoped to Redline; never reset this shared database.
2. Put Redline application tables in a dedicated `redline` schema and qualify every repository query. Keep authorization membership records in an unexposed schema. A schema name separates objects, but does not itself prevent access.
3. Enable row-level security on each Redline data table. Require both ownership by `auth.uid()` and server-controlled Redline membership for reads and writes, including insert/update checks. Grant only the operations needed by the application. Anonymous callers and authenticated users without Redline membership get no document or preference access.
4. Supabase Auth remains one shared user pool and token issuer. A valid project token alone does not establish access to either app. Enrollment must explicitly grant app membership through trusted server logic; users cannot grant themselves membership by changing user metadata. Trippal staging must also enforce its own access rules before shared hosting is treated as isolated between apps.
5. Coordinate shared Auth settings, email templates, providers, and redirect allowlists with Trippal staging. Add exact Redline callback URLs once known; preserve existing callbacks. Use a Redline-specific browser session cookie/storage name. Separate browser sessions do not replace authorization checks.
6. Keep normal user operations under the user's verified session so RLS applies. Avoid giving Redline a project-wide service-role credential for ordinary data access. Any administrative setup path must be server-only and narrowly controlled; a project service-role key can bypass RLS across both apps.
7. Keep keys in gitignored `.env.local` and the intended Redline deployment's environment settings. Only the publishable/anon key may enter browser code. Keep privileged database credentials and the OpenRouter key server-only. Generate database types including the `redline` schema. If using the Data API, expose only the required schema after grants and RLS are ready; leave the membership schema unexposed.
8. Store only browser-extracted text and analysis results. Original uploads stay in the browser; no Redline file-storage bucket is needed for v1.

## Checks before completion

- Redline user A can create/read/update/delete only their permitted records; user B cannot read or change A's records or change a record's owner to another user.
- Anonymous and Trippal-only accounts cannot access Redline records, including through direct API requests. Redline-only accounts cannot access Trippal staging data or privileged RPCs.
- Users cannot add their own membership or obtain access through editable metadata. Both apps' sign-in and sign-out flows work without redirect or session collisions.
- Before/after inspection confirms existing Trippal objects and access rules remain intact. Verify these checks against user sessions, not a service-role client.
- Verify migrations locally first, then apply only to the shared staging target. Do not use production credentials or run a database reset against either hosted project.

Shared hosting also shares compute, quotas, Auth administration, and outage risk. It is suitable for this cost-constrained development setup, but does not meet a requirement for independently isolated pilot infrastructure. These checks are required work, not completed evidence.

## Sources checked November 1, 2026

- [Supabase billing and the cross-organization project limit](https://supabase.com/docs/guides/platform/billing-on-supabase#free-plan)
- [Billing FAQ](https://supabase.com/docs/guides/platform/billing-faq#how-many-free-projects-can-i-have)
- [Free plan quotas and inactivity pausing](https://supabase.com/pricing)
- [Custom schemas](https://supabase.com/docs/guides/api/using-custom-schemas)
- [Row-level security](https://supabase.com/docs/guides/database/postgres/row-level-security)
- [Local development](https://supabase.com/docs/guides/local-development)
