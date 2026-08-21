---
name: tackle-issue
description: Take a GitHub issue from selection or complete intake through implementation, verification, and submitted pull requests. Use when the user asks to tackle, fix, pick up, implement, or resolve an issue and expects the work to be published for review.
---

# Tackle Issue

Own the requested issue through submitted, reviewable pull request(s). Invoking this skill authorizes creating a branch, committing in-scope work, pushing it, and opening PRs. It does not authorize merging, manually closing issues, assigning people, or changing unrelated work.

## 1. Establish the issue

- Resolve the exact repository from the URL, reference, or current checkout. Ask only if more than one interpretation remains plausible.
- If the user did not specify an issue, inspect open issues and open PRs, exclude issues already covered by open PRs, then offer a concise shortlist ordered from simplest to most complex. Explain the ranking and ask the user to choose before implementation. Use linked development items and closing references, not title matching alone, to determine coverage.
- Once the user specifies or selects an issue, resolve its exact number.
- Read the title, complete current body, metadata, and every current comment. Follow pagination until exhausted; do not treat a search result or summary as complete.
- Inspect each issue or PR participant's repository role, author association, and contribution history before treating their statements as project direction. Guidance from an owner, maintainer, collaborator, or established contributor carries substantial weight but is not automatically authoritative. Give unsupported claims from people without a demonstrated project relationship much less weight, while still evaluating concrete evidence on its merits.
- Inspect native sub-issue relationships, not only prose links. For a parent or meta issue, read every relevant sub-issue completely and track which sub-issues the implementation actually completes.
- Inspect attachments and linked discussions, issues, commits, or PRs when they contain requirements or evidence needed to understand the issue.
- Reconcile the conversation chronologically. Treat later maintainer clarification as current guidance, but surface unresolved contradictions instead of choosing silently.
- Do not post assignment or progress comments unless the user requests them. If "pick up" is intended to mean assignment, confirm the assignee before changing it.

## 2. Read the repository contract

- Read every applicable `AGENTS.md`, contribution guide, relevant design or status documentation, and local workflow instruction before editing.
- Inspect the affected code, tests, history, and current worktree. Preserve unrelated and user-owned changes.
- Translate the issue and comments into explicit acceptance criteria. State assumptions, a short plan, and how each step will be verified.
- If the requested behavior conflicts with the repository contract or still requires a product decision, stop and ask with concrete evidence.

## 3. Implement the complete fix

- Start from the intended base. Name the branch after the feature, behavior, or outcome being delivered, using a concise hyphenated description such as `room-socket-connections`. Do not include the issue number and do not use a `codex/` prefix. Follow any other mandatory repository branch constraints.
- Reproduce the defect or establish a failing test or check when practical.
- Make the smallest change that satisfies the acceptance criteria. Add or update focused tests and any required documentation, trackers, generated files, or metadata in the same scope.
- Use Conventional Commits for the final history unless the repository explicitly requires an incompatible commit convention.
- Run the strongest relevant checks. Investigate failures and distinguish regressions from pre-existing failures with evidence.

## 4. Shape the pull requests

- Prefer one focused PR. Split work only when parts are independently useful or a dependency stack materially improves reviewability.
- Use `$prepare-pull-request` when available to protect local work, shape commits and branches, verify each PR layer, and publish cleanly.
- Compare every PR with its actual base and review the complete diff before committing or pushing. Never include unrelated files silently.
- For multiple PRs, document bases and dependencies. Partial or prerequisite PRs must use a non-closing reference such as `Part of #<number>` or `Relates to #<number>`.

## 5. Publish the fixing PR

- Immediately before creating or updating each PR, fetch the issue conversation again, follow pagination until exhausted, and check for new comments. Incorporate new requirements or evidence; surface conflicts instead of publishing stale work.
- Follow the repository's PR template and publishing rules. Keep the body concise and include the issue-level outcome, material risks or omissions, and stack dependencies when relevant. Let `$prepare-pull-request` govern the PR narrative and screenshot decisions.
- Put each closing keyword on its own line in the PR that makes the corresponding issue complete: `Closes #<number>`.
- For parent or meta issues, do not close the parent directly unless repository policy says that is correct. Close completed leaf issues individually and leave incomplete work open.
- Include a closing reference exactly once across the PR set for each issue completed by the work. For an issue in another repository, use `Closes <owner>/<repo>#<number>`.
- Ensure a closing PR ultimately targets the repository's default branch so the hosting platform can close the issue automatically; retarget stacked PRs after prerequisites merge when needed.
- Use draft only when implementation or required verification remains. Otherwise publish ready for review. Do not merge unless separately requested.

## 6. Report the handoff

- Do not call the issue tackled until the required PR or PRs exist remotely.
- Report PR URLs, branch and base relationships, commit hashes, checks and results, untested areas, and excluded local changes.
- Identify every issue each PR closes and what remains before merge. For a parent or meta issue, state whether it was deliberately left open and list incomplete sub-issues.
