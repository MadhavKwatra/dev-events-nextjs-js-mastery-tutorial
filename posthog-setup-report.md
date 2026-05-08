<wizard-report>
# PostHog post-wizard report

The wizard has completed a deep integration of PostHog analytics into the DevEvent Next.js App Router project.

**Changes made:**

- **`instrumentation-client.ts`** (new): Initializes PostHog client-side using `posthog-js` via the Next.js 15.3+ `instrumentation-client` pattern. Configured with a reverse proxy (`/ingest`), error tracking (`capture_exceptions: true`), and debug mode in development.
- **`next.config.ts`**: Added PostHog reverse proxy rewrites for `/ingest/static/*`, `/ingest/array/*`, and `/ingest/*`, plus `skipTrailingSlashRedirect: true` to support PostHog's trailing slash API requests.
- **`components/ExploreBtn.tsx`**: Added `posthog.capture('explore_events_clicked')` to the existing `onClick` handler.
- **`components/EventCard.tsx`**: Added `"use client"` directive and `posthog.capture('event_card_clicked')` with properties (`event_title`, `event_slug`, `event_location`, `event_date`) on the Link click handler.
- **`components/Navbar.tsx`**: Added `"use client"` directive and `posthog.capture('navbar_link_clicked')` with a `label` property on all nav link click handlers.
- **`.env.local`**: Added `NEXT_PUBLIC_POSTHOG_PROJECT_TOKEN` and `NEXT_PUBLIC_POSTHOG_HOST` environment variables.

| Event name | Description | File |
|---|---|---|
| `explore_events_clicked` | User clicks the "Explore Events" CTA button on the homepage hero section | `components/ExploreBtn.tsx` |
| `event_card_clicked` | User clicks on an event card to view event details (top of conversion funnel) | `components/EventCard.tsx` |
| `navbar_link_clicked` | User clicks a navigation link in the top navbar | `components/Navbar.tsx` |

## Next steps

We've built some insights and a dashboard for you to keep an eye on user behavior, based on the events we just instrumented:

- **Dashboard — Analytics basics**: https://us.posthog.com/project/415579/dashboard/1561139
- **Explore Events button clicks** (trend): https://us.posthog.com/project/415579/insights/Z9hZHrT1
- **Event card clicks over time** (trend): https://us.posthog.com/project/415579/insights/kTfG4i0S
- **Homepage to event detail conversion funnel**: https://us.posthog.com/project/415579/insights/T7Cg27gz
- **Most popular events by clicks** (breakdown by event title): https://us.posthog.com/project/415579/insights/XYPfDCh3
- **Navbar link click distribution** (breakdown by label): https://us.posthog.com/project/415579/insights/JKbrRsaL

### Agent skill

We've left an agent skill folder in your project. You can use this context for further agent development when using Claude Code. This will help ensure the model provides the most up-to-date approaches for integrating PostHog.

</wizard-report>
