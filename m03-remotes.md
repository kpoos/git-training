# 03 — Remotes and shared work

## Goals

- Distinguish local commits from remote commits.
- Clone, fetch, pull, and push a branch.
- Coordinate a shared repository without pushing directly to its default
  branch.

## The remote workflow

A remote is a named reference to another repository, commonly called `origin`
for the repository you cloned. `git fetch` downloads remote updates without
integrating them into your current branch. `git pull` fetches and integrates
updates. `git push` publishes local commits to a remote branch.

Use a dedicated branch for work and check the destination before publishing:

```sh
git clone <repository-url>
cd <repository-directory>
git remote -v
git switch -c add-team-note
# edit a file
git status
git add <file>
git diff --staged
git commit -m "Add team note"
git push -u origin add-team-note
```

Replace placeholders with the actual URL, directory, branch, and file. Avoid
putting credentials in a remote URL; use the approved GitHub sign-in method.

To check for teammates' work:

```sh
git fetch origin
git status
git log --oneline --graph --decorate --all
```

Before starting a new task, update the local default branch from its remote.
Only do this with a clean working tree:

```sh
git switch main
git pull --ff-only origin main
```

If Git reports that branches have diverged or the working tree is not clean,
stop and inspect `git status` rather than forcing an update.

## Lab 3 — Publish without colliding

The facilitator creates a practice repository and adds learners as
collaborators, or learners work in personal forks. Everyone clones the
repository. Each learner creates a uniquely named branch, makes one small
change in a different file or section, commits it, and pushes that branch.
Partners fetch and inspect one another's branches without changing the
default branch.

**Done when:** each learner can show a local branch, its remote counterpart,
and the commit that connects them.

**Debrief:** What does fetching do that pulling does not? Which branch did
your push update?

For a complete clone, branch, push, and partner-fetch walkthrough, use
[lab 3 in the guided lab guide](./labs/README.md#lab-3--publish-a-branch-without-colliding).

Continue with [issues, pull requests, and review](./m04-pull-requests.md).
