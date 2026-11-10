# 01 — Git and local history

## Goals

- Describe the working tree, staging area, and repository history.
- Inspect a change before recording it.
- Create a useful commit and read a short history.

## The mental model

Git records snapshots as commits. Files you edit are in the working tree.
Staging selects which changes belong in the next commit; it does not publish
them. A commit records the staged snapshot in local history. A remote is a
separate copy that can be shared later.

## Explore the workflow

In a new practice directory:

```sh
mkdir git-practice
cd git-practice
git init
git status
```

Create `README.md` with a title and one sentence about the practice project.
Then inspect, stage, and commit it:

```sh
git status
git diff
git add README.md
git diff --staged
git commit -m "Add project introduction"
git log --oneline
```

Edit the sentence and add a second line. Inspect the unstaged diff. Stage only
the intended file and inspect the staged diff before making a second commit.

Useful commands:

| Command | What it answers |
| --- | --- |
| `git status` | What is changed, staged, or untracked? |
| `git diff` | What changed but is not staged? |
| `git diff --staged` | What will the next commit contain? |
| `git log --oneline --decorate` | Which commits and branch pointers exist? |

## Lab 1 — A history your teammate can read

Work in pairs. Each person creates a small local project in their own
directory, then exchanges directories or shares the screen with their partner.
Make at least two focused commits. The partner should use `git log` and the
diffs to explain the sequence without being told what happened.

**Done when:** the working tree is clean, each commit message describes its
change, and the partner can explain what each commit added.

**Debrief:** Which was clearer: one large commit or several focused commits?
What did staging let you control?

For the full command-by-command walkthrough and expected checks, use
[lab 1 in the guided lab guide](./labs/README.md#lab-1--make-a-history-your-teammate-can-read).

## Check your understanding

1. Does `git add` send changes to GitHub? Why not?
2. What is the difference between `git diff` and `git diff --staged`?
3. What does a commit message help a future teammate understand?

Continue with [branches and merging](./m02-branches.md).
