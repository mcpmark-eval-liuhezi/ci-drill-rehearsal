# CI Incident Drill — Runbook Log

Rehearsal of the quarterly CI incident runbook, executed end to end against the `mcpmark-eval-liuhezi/ci-drill-rehearsal` sandbox repository. This pull request carries the drill's checklist (`DRILL_CHECKLIST.md`) and this file is the recorded runbook log.

## Recorded evidence

- **Cancelled workflow run id:** `39801528231` (run number 2 of `CI Drill Sleep`, triggered manually via `workflow_dispatch` on the default branch `main`)
- **Final status of that run:** `completed`, with conclusion `cancelled`
- **Log deletion:** **Succeeded** — the delete call returned HTTP `204 No Content`, and a follow-up attempt to retrieve the run's logs returned HTTP `404 Not Found`, confirming the logs are gone
- **Secret scanning check:** The check returned `403 Resource not accessible by personal access token` when querying `/repos/mcpmark-eval-liuhezi/ci-drill-rehearsal/secret-scanning/alerts`. This is the actual result returned — no assumption is made about whether alerts exist, because the token in use is not permitted to read secret scanning alerts for this repository.

## Step-by-step log

| # | Drill step | Outcome |
| --- | --- | --- |
| 1 | Trigger a fresh manual (`workflow_dispatch`) run of the sleep workflow on the default branch | Run `39801528231` queued and started; job `sleep` entered its `Long-running sleep` step |
| 2 | Cancel the run while still in progress | Cancellation accepted (HTTP `202 Accepted`); run settled to status `completed` / conclusion `cancelled` |
| 3 | Delete the cancelled run's logs | Succeeded (HTTP `204 No Content`); logs verified gone via HTTP `404` on retrieval |
| 4 | Check the repository for secret scanning alerts | Returned `403 Resource not accessible by personal access token` — recorded as-is, not an assumption |
| 5 | Rename the pull request and rewrite its description as this runbook log | Done — title updated to `[DRILL COMPLETE] Rehearse CI incident runbook` |
| 6 | Commit this same log to the `drill/step-1` branch | Done — committed as `DRILL_RUNBOOK_LOG.md` so it appears among this pull request's changed files |
| 7 | Start a review and deliberately leave it pending | Done — pending review with exactly one comment on `DRILL_CHECKLIST.md`, left un-submitted |

Drill verdict: pass
