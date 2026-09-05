# BUILD-PLAN: full/REFIT Launcher

## Job to be done
Give Paul one installable, searchable launcher page with a button to every current project in the fullrefit Vercel account.

## Product shape and tier
Progressive Web App, Tier 2. It is a static read-only launcher with no user accounts, no server writes, and no cross-session application state beyond the browser's install cache.

## What this is not
This is not a replacement for Vercel, Airtable, or a project management system. It does not edit, delete, or infer project metadata. It is not a second source of truth for deployment status.

## Build calls
| Decision | Call | Why | Trade-off accepted |
|---|---|---|---|
| Frontend | Single static HTML, CSS, and JavaScript app | The launcher only renders an audited app catalog and links | Less component abstraction, faster and easier to inspect |
| UI/UX direction | `fullrefit-frontend-execution` with Carbon Forge roles | full/REFIT app surface, high link density, and Paul’s preference for legible restrained UI | More restrained than a decorative dashboard |
| Backend / data | None. A checked-in generated catalog derived from Vercel account output and Airtable record metadata | No runtime API or secret is safe or necessary in a public launcher | Catalog refresh is a deliberate deployment action |
| Deployment | GitHub repository `fullREFIT/fullrefit-launcher` and Vercel project `fullrefit-launcher` | The requested public URL and Git-backed source of truth | Public static catalog exposes project names and URLs already present in the supplied inventory |

## Data model
Each launcher item is inferred from the live Vercel project listing and the matching Airtable row where available:
- `name`: Vercel project name, stated by Vercel.
- `projectId`: Vercel project ID, stated by Vercel.
- `url`: Vercel latest production URL, stated by Vercel when present.
- `status`: Airtable status when present, otherwise active by default. This does not replace Vercel production state.
- `productionStatus`: Airtable production status, stated by the catalog audit.
- `framework`: Airtable framework when present, otherwise blank.
- `description`: Airtable thesis statement when present, otherwise a short project-name fallback.

## Skill sequence
| Phase | Skill | Selected because | Path verified |
|---|---|---|---|
| research | none, handled directly | Live Vercel and Airtable audit was the requested research | `/usr/local/bin/vercel` and Airtable REST response verified |
| spec | `blueprint` | The requested launcher is a net-new web app and needs a BUILD-PLAN | `/Users/paul/.hermes/skills/blueprint/SKILL.md` |
| design-ui | `fullrefit-frontend-execution` | Carbon Forge app surface and accessible link grid | `/Users/paul/.hermes/skills/software-development/fullrefit-frontend-execution/SKILL.md` |
| build-frontend | none, handled directly | Static HTML/CSS/JS is smaller than a framework for this Tier 2 launcher | Not applicable |
| build-backend | none | No backend or secret-bearing runtime is required | Not applicable |
| verify | `webapp-testing` | Verify links, install metadata, mobile layout, and production response | `/Users/paul/.hermes/skills/webapp-testing/SKILL.md` |
| ship | `ship` | Executes the approved web BUILD-PLAN and verifies its acceptance test | `/Users/paul/.hermes/skills/ship/SKILL.md` |

## Rejected candidates
- `web-app-builder` was rejected because this is a net-new launcher rather than a document-rendering surface.
- `runbook-template` was rejected because the launcher is a navigation surface, not a checklist or runbook.
- `vibe-code` was rejected because the project is intentionally Tier 2 and does not need a framework build.

## Execution
Surface: this session. The filesystem, Vercel CLI, GitHub CLI, and Airtable credential path are available and the work fits one session.
Model: current Hermes session for execution after the explicit user instruction authorizes blueprint then ship.
Split: plan in deep tier, execute in standard tier. The plan fixes the architecture, data contract, and acceptance test before implementation.

## Acceptance test
1. The GitHub repository `fullREFIT/fullrefit-launcher` exists and contains the launcher source and generated catalog.
2. The Vercel project `fullrefit-launcher` is deployed at `https://fullrefit-launcher.vercel.app`.
3. The production HTML loads with HTTP 200, has the launcher title, manifest link, and service worker registration.
4. The launcher contains exactly one button or link for each of the 80 live Vercel projects audited in this run, with no duplicate Vercel project IDs.
5. Each button opens the exact `latestProductionUrl` returned by Vercel. Projects without a production URL are shown as unavailable rather than linked to a guessed URL.
6. The Airtable table contains the 17 records created from the missing Vercel project IDs, verified by exact record read-back.
7. Desktop and 375px mobile layouts render without horizontal overflow, and the service worker and manifest are served successfully.

## Open questions
None blocking. The launcher will include archived Airtable items as visibly labelled entries because the user requested a button to each deployed web app. The Airtable stale row is retained because deletion was not requested.

## Next action
Execute the plan by generating the audited 80-item catalog, building the static PWA, pushing `fullREFIT/fullrefit-launcher`, deploying to Vercel, and verifying the live URL and link count.
