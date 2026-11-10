# 04 — Issues, pull requests, and review

## Goals

- Describe the GitHub flow from task to merged change.
- Open a pull request with enough context for a reviewer.
- Give and respond to constructive review feedback.

## A collaboration loop

1. Agree on a small task; record it as an issue if the repository uses issues.
2. Create a focused branch and make a change.
3. Commit and push the branch.
4. Open a pull request (PR) against the intended base branch.
5. Explain the problem, the approach, and how the result was checked.
6. Review the diff, discuss feedback, and make follow-up commits on the branch.
7. Merge only after review and required checks are complete.

A PR is a conversation around a proposed change, not just a button to merge.
Authors should make the scope and verification clear. Reviewers should point to
the relevant change, explain the concern, and ask a question when intent is
unclear.

## Review checklist

- Does the change address the agreed task?
- Is the diff limited to the intended files and behavior?
- Are names, wording, and examples understandable to a new contributor?
- Are there accidental secrets, generated files, or unrelated edits?
- Is the evidence for testing or checking stated?

Use comments to help the author improve the change. Critique the change, not
the person. The author should respond to each thread and say what changed or
why a suggestion was not applied.

## Lab 4 — Review, revise, and merge

Continue from lab 3. Each learner opens a PR for their branch. Pair with a
reviewer who checks the diff and leaves one specific question or suggestion.
The author discusses the feedback, makes a follow-up commit where appropriate,
and pushes it. The reviewer verifies the update. Merge through GitHub using
the repository's allowed method, then update the local default branch.

**Done when:** a PR has a useful summary, a review exchange, and a merged
result; the author can point to the commit that addressed feedback.

**Debrief:** What made feedback actionable? What context was missing from the
PR description?

For detailed GitHub steps, review prompts, and local synchronization
commands, use [lab 4 in the guided lab
guide](./labs/README.md#lab-4--review-revise-and-merge-a-pull-request).

Continue with [conflicts and safe recovery](./m05-recovery.md).
