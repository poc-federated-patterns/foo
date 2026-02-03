# Triggering Bar via Repository Dispatch

This workflow triggers `poc-federated-patterns/bar` asynchronously via `repository_dispatch`.

- File: `.github/workflows/trigger-bar-dispatch.yml`
- Trigger: `workflow_dispatch`
- Action: Uses `actions/github-script@v7` (Octokit) to call `repos.createDispatch` with an event and payload

## PAT Requirements

Create a fine-grained PAT and store it in foo's repository secrets as `BAR_PAT`.

- Repository access: `poc-federated-patterns/bar`
- Permissions:
  - Contents: Read and write
  - Actions: Read and write (to trigger workflows)

`GITHUB_TOKEN` cannot dispatch to other repos.

## Inputs

- `event_type`: `build-request` or `deploy-request`
- `environment`: `staging` or `production`

## Payload Structure

```json
{
  "ref": "<foo run sha>",
  "triggered_by": "<actor>",
  "source_repo": "poc-federated-patterns/foo",
  "source_run_id": "<run id>",
  "environment": "staging|production"
}
```

## Observability

- Dispatch is fire-and-forget: check bar's Actions tab for the run
- For completion notifications, see TASK-001-4 (callback pattern)
