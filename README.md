# seazn.club.workflow

Scheduled GitHub workflows for seazn.club.

## What runs here

- `simulation-nightly.yml` — the scheduled simulation run.

## What no longer runs here

The cron sweeps (registrations, billing events, funnel reminders, AI preview retention, billing quantity,
billing AI credit grant, weekly news digest) were retired from this repo on 2026-11-17. They run from the
cron Worker in the main repo (`onryde/seazn.club`, `apps/cron-worker`, deployed as `seazn-cron-prod` and
`seazn-cron-stg`), whose `src/schedule.ts` is the one list of jobs.

Why retired rather than kept as a second caller: a GitHub runner's `curl` to production is challenged by
Cloudflare Bot Fight Mode at random (HTTP 403), and on the Free plan that mode cannot be exempted per path
or per IP. The Worker calls the same endpoints from inside the zone and is not challenged.

To run a job by hand, use the Worker's manual trigger, not a workflow here.
