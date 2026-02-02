# Calling bar with `secrets: inherit`

This workflow demonstrates that `secrets: inherit` passes the caller's (foo) secrets to bar's reusable workflow. It does not grant bar access to its own repo secrets.

## Workflow

- File: `.github/workflows/call-bar-with-bar-secrets.yml`
- Trigger: `workflow_dispatch`
- Action: Calls `poc-federated-patterns/bar/.github/workflows/reusable-internal.yml@main` with `secrets: inherit`

## Setup

1. In foo, define a repo secret named `CALLER_SECRET` (any value).
2. Optionally, in bar define a repo secret named `BAR_INTERNAL_SECRET` — the demo will show it's not available to the callee when invoked via `workflow_call`.

## Run

1. Dispatch the workflow "Call Bar (Demonstrates secrets inherit)" from the Actions tab in foo.
2. Observe in bar's job logs:
   - `✅ Caller secret received: XXXX****` (if `CALLER_SECRET` is set in foo)
   - `❌ Bar's own secret NOT available (expected behavior)`

See also: bar/docs/understanding-secrets-inherit.md for background and alternatives (OIDC, GitHub App, environment secrets).
