# CI Incident Drill - Runbook Checklist

Quarterly rehearsal executed against the `ci-drill-rehearsal` sandbox repository.

## Drill steps

1. **Trigger** - Start a fresh manual (`workflow_dispatch`) run of the `drill-sleep` workflow on the default branch.
2. **Interrupt** - Cancel the run while it is still in progress.
3. **Erase evidence** - Delete the logs of the cancelled run.
4. **Audit** - Check the repository for secret scanning alerts and record the actual result.
5. **Record** - Rename the pull request to carry the `[DRILL COMPLETE]` prefix and rewrite its description as a runbook log.
6. **Persist** - Commit the runbook log to the `drill/step-1` branch so it appears among the pull request's changed files.
7. **Review** - Start a review on the pull request, leave it pending (do not submit), and attach one comment to this checklist file ending with the drill verdict.
