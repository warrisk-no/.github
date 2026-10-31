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

New issues are triaged by GitHub's issue triage agent automation, configured per repo. Its
instructions are kept in [`issue-triage-instructions.md`](issue-triage-instructions.md):
change them there in a PR, then paste them into the automation's settings.
