# warrisk-no/.github

Org-wide defaults for warrisk-no repositories.

## Issue forms

`.github/ISSUE_TEMPLATE/` holds the forms every repo gets unless it has its own
`.github/ISSUE_TEMPLATE/` folder: Bug, Feature or enhancement, Spike, Chore or tech debt,
Decision. Each sets its work-type label and GitHub issue type (Bug, Feature, Task). Blank
issues are still allowed.

The labels (`feature`, `enhancement`, `bug`, `security`, `spike`, `chore`, `tech-debt`,
`epic`, `decision`, `incident`) exist on the active repos. Claude Code files issues with the
same labels and types through the `/warrisk:issue-from-spec` and `/warrisk:bug-report`
skills in [claude-skills](https://github.com/warrisk-no/claude-skills).

## Issue triage

`.github/workflows/issue-triage.yml` is a reusable workflow. On a new issue it adds the
labels for the form's security and tech-debt boxes, and if the issue still has no
work-type label, Claude classifies it: one work-type label, the issue type, existing area
labels, and a comment when a bug has no evidence or repro. It never edits the issue text.

A repo turns it on with `.github/workflows/issue-triage.yml`:

```yaml
name: Issue triage

on:
  issues:
    types: [opened]

permissions:
  contents: read
  issues: write
  id-token: write

jobs:
  triage:
    uses: warrisk-no/.github/.github/workflows/issue-triage.yml@main
```

Claude authenticates with Anthropic workload identity federation, so there is no API key:
the job's GitHub OIDC token is exchanged for a short-lived Anthropic token. The IDs are org
Actions variables (`ANTHROPIC_FEDERATION_RULE_ID`, `ANTHROPIC_ORGANIZATION_ID`,
`ANTHROPIC_SERVICE_ACCOUNT_ID`, `ANTHROPIC_WORKSPACE_ID`). The federation rule in the
Claude Console only admits tokens whose `job_workflow_ref` is this workflow on `main`, so
no other workflow can obtain an Anthropic token through it.
