# 05 — Conflicts and safe recovery

## Goals

- Resolve a content conflict without losing either contributor's intent.
- Distinguish restoring a file, reverting a commit, and resetting local
  history.
- Choose a recovery operation appropriate to whether changes were shared.

## Resolve a conflict deliberately

When a merge conflict occurs, Git pauses the merge. Read `git status`, open
each listed file, compare both sides, and decide the correct combined result
with the collaborator. Remove conflict markers, run checks, stage the resolved
files, and finish the merge. The resulting merge commit records the integration.

## Undo operations are not interchangeable

| Situation | Safer starting point | Effect |
| --- | --- | --- |
| Discard unstaged edits to one file | `git restore <file>` | Replaces that file with its index version; discarded edits are lost |
| Unstage a file but keep its edits | `git restore --staged <file>` | Removes it from the index, not from the working tree |
| Undo a commit that may already be shared | `git revert <commit>` | Adds a new commit that reverses the selected change |
| Move local branch history, before sharing | `git reset` | Moves the branch pointer; effects depend on the mode and may discard work |

Before any undo, inspect `git status`, `git diff`, and `git log`. Prefer
`git revert` for a shared commit because it preserves published history. Avoid
resetting shared history. Do not use `git reset --hard` or force-push in these
labs. If uncertain, stop and ask the facilitator before changing history.

## Lab 5 — Recover without panic

In a disposable repository only:

1. Make an unstaged edit and inspect it with `git diff`.
2. Stage a different edit, then use `git restore --staged <file>` and verify
   the file's contents remain in the working tree.
3. Make a small commit. Use `git revert HEAD` to create a new commit that
   reverses it.
4. Create a conflict using the routine in module 02 and resolve it with a
   partner.

Before every recovery operation, explain what is staged, what is committed,
and whether another person could already have the commit.

**Done when:** the learner can describe each operation's effect and the
repository history remains intact.

For a detailed, safe walkthrough with state checks before each undo, use
[lab 5 in the guided lab guide](./labs/README.md#lab-5--recover-without-panic).

Continue with the [team capstone](./m06-capstone.md).
