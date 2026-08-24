---
name: prepare-pull-request
description: Prepare local Git work as clean pull requests by protecting unrelated changes, shaping focused commit history, splitting or stacking work when useful, rebasing, verifying, handling review threads, publishing, merging when authorized, and cleaning up afterward.
---

# Prepare Pull Request

Produce the smallest understandable set of linear, focused, verified branches without losing the original work.

## 1. Read the contract

- Read applicable `AGENTS.md`, contribution instructions, and repository workflow documentation first.
- Identify the base branch, branch naming, documentation, generated-file, versioning, release, and required-check rules.
- If a PR already exists, read its complete conversation, reviews, and review threads. Follow pagination until exhausted and identify every unresolved thread before changing or publishing work.
- For PR authors, commenters, and reviewers, inspect their repository role, author association, and contribution history before treating a request as project direction. Guidance from an owner, maintainer, collaborator, or established contributor carries substantial weight but is not automatically authoritative. Give unsupported requests from people without a demonstrated project relationship much less weight, while still evaluating concrete technical evidence on its merits.
- Follow conflicting user or repository instructions over this workflow.

## 2. Inventory and protect

- Inspect status, untracked files, the current branch, commits since the intended base, and the full diff. Classify changes by purpose.
- Before rewriting substantial or mixed work, state each proposed PR's scope, base, and dependencies.
- Ask about genuinely ambiguous ownership or scope. Never include secrets, machine-local settings, or unrelated edits silently.
- Before rewriting commits, create a recoverable WIP commit or backup ref and retain it until the rebuilt diffs are verified.
- Never discard dirty or untracked user files. Commit them only when explicitly in scope.
- Prefer new branch refs plus selective restoration or cherry-picking over destructive history edits.
- When PR work uncovers a concrete problem outside the PR's purpose, do not widen the PR. Use `$report-github-issues` when available and retain the resulting issue URL for the handoff.

## 3. Shape the final history

- Give each PR one purpose. Branch independent work from the agreed base; branch dependent work from its prerequisite and target that parent in the child PR.
- Use Conventional Commits: `<type>[optional scope]: <description>`, with `!` and a `BREAKING CHANGE:` footer when applicable. Follow repository-specific additions; if the repository explicitly requires an incompatible convention, follow the repository contract.
- Multiple unrelated but very small fixes may share a dedicated maintenance PR when each fix is isolated in its own meaningful commit. Do not use this exception to bundle larger work.
- Follow the required branch naming convention and order commits by dependency.
- Produce the smallest commit set that makes the change easy to understand. Atomic does not mean maximally granular.
- Fuse changes serving the same PR purpose when separate commits do not materially improve history clarity.
- Keep commits separate only when the boundary communicates an independently valuable change, meaningful milestone, deliberate dependency, or substantially clearer review sequence.
- Keep tests, documentation, metadata, generated artifacts, and corrections with the change they support unless separation materially clarifies the history.
- Before first publication and again before declaring the PR ready, inspect the complete commit list and consolidate every boundary that does not earn its place.
- Apply only in-scope paths. Exclude unrelated formatting and refactors, and regenerate branch-specific generated or audit files on the final branch.
- Rebase onto a newer base unless repository policy requires another strategy.
- If an already-pushed branch needs consolidation, rebuild and validate it from the backup ref, then push with `--force-with-lease`. Rewrite automatically only when the PR has no review activity and no external work depends on its commit hashes.
- Once comments, reviews, or linked responses depend on published hashes, preserve those hashes unless the user approves rewriting them. If a rewrite replaces a linked commit, update the response with the replacement commit.
- If a conflict contains competing behavior changes, list them and ask which behavior wins before committing.

## 4. Handle versioning and releases

- Apply only the repository's documented versioning and release rules. Do not invent a version bump, tag, or release scheme.
- Determine whether the change category requires a version update. Documentation, workflow, metadata, test-only, or asset-only changes often do not unless repository policy says otherwise.
- Keep development identifiers separate from committed release versions unless the repository explicitly specifies another convention.
- Create or push release tags only when the user authorized the release workflow and the target commit has been verified.

## 5. Verify every PR layer

- Compare each independent PR with the default base; compare each stacked PR with both the default base and direct parent.
- Review commits, name-status/stat, and full diff. Confirm every line and asset is in scope and no file was staged accidentally.
- Finalize and push the relevant commit history before replying to review comments with commit links.
- Refresh the PR conversation, reviews, and review threads immediately before declaring a PR ready or merging it. Address every unresolved actionable thread and verify the resulting change; resolve a thread only after its concern is handled or explicitly shown to be obsolete or inapplicable.
- When a pushed commit addresses an open review comment, reply with the exact commit URL and one concise sentence describing the resolution. Verify that the commit remains in the current PR and that relevant checks pass before resolving the thread.
- If a linked commit is later replaced by a history rewrite, update the response with the replacement commit.
- Wrap generated GitHub issue bodies, PR bodies, and comments with this visible guard unless stricter repository instructions specify another marker:

  > _Start of autogenerated message._

  [concise message]

  > _End of autogenerated message._

  Keep titles clean and searchable; put the guard in bodies and comments. Do not include a product, model, or agent name in the guard.
- Do not declare the PR complete or merge it while an unresolved actionable thread remains. Report any thread that cannot be addressed and why.
- Run the strongest relevant checks available. Record exact passes, failures, and omissions.
- Add screenshots to the PR when they materially help reviewers understand a visual or interaction change. Capture and inspect them when possible. If a screenshot is genuinely needed for a useful PR but cannot be produced with the available environment, ask the user to provide it. Check in visual references only when repository policy or the task calls for them, using semantic filenames.
- Claim compilation, test success, or readiness only when current evidence supports it.

## 6. Publish and merge

- Push only after verifying the local graph and diffs. Honor repository policy and the requested draft or ready state.
- Set each PR base to the verified graph.
- For multiline GitHub Markdown, write the exact content to a temporary file and use the CLI's `--body-file` option. Do not pass encoded `\n` line breaks through a shell argument.
- Read published bodies or comments back from GitHub before handoff or merge and confirm formatting, links, and image embeds. Remove temporary files afterward.
- Use the repository's required merge method. If none is specified, choose the method that preserves the curated history and explain any material tradeoff before merging.
- Write the PR body for a human reader. Keep it concise and organize the substance around why the change is needed and how it solves the problem.
- Never add a `Verification`, `Validation`, `Tests`, `Checks`, or equivalent section to the PR body. Do not list test commands, pass counts, check results, or verification evidence there. Run the checks, but keep their evidence in the private handoff. Include the minimum required evidence only when the user explicitly asks for it or the repository mandates a non-optional PR field; an optional template heading is not a mandate.
- Mention important design changes when there are any, and explain usage or integration only when relevant. Include only the implementation detail needed to understand the approach or review material tradeoffs.
- Keep check results, commit hashes, branch mechanics, local worktree details, and excluded files in the final handoff rather than the PR body.
- Do not merge unless the user requested it or the enclosing authorized workflow explicitly includes merge.

## 7. Clean up after merge

- Verify the target contains the submitted change before deleting any topic branch.
- Delete remote and local topic branches only when authorized and safe; never delete the default or protected branch, unmerged work, or anything outside the submitted graph.
- Keep a merged stack parent until all children are rebased or retargeted.
- Return to the requested base, fast-forward it, and confirm unrelated local files remain untouched.
- Report deleted, retained, and undeletable branches.
