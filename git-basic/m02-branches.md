# 02 — Branches and merging

## Goals

- Create and move between branches.
- Explain how a branch supports independent work.
- Merge a completed change and inspect the result.

## Branches as parallel work

A branch is a movable name for a line of commits. Creating a branch gives a
change its own path without changing the default branch. A merge integrates
that path into another branch. Git may merge automatically; if both sides
changed the same part of a file, it asks a person to resolve the conflict.

## Guided practice

From the practice repository created in module 01:

```sh
git switch -c add-project-goal
```

Add a goal to `README.md`, inspect and commit the change, then return to the
default branch and merge:

```sh
git status
git diff
git add README.md
git diff --staged
git commit -m "Add project goal"
git switch main
git merge add-project-goal
git log --oneline --graph --decorate --all
```

If the initial branch is not named `main`, use the name shown by
`git branch --show-current` while on the default branch.

## Lab 2 — Integrate two changes

In a pair, start from a clean working tree. The author creates a branch and
adds a new, separate bullet to the project README. The reviewer creates a
different branch from the same starting point and adds a different bullet.
Take turns merging the branches into the default branch.

Then repeat with both learners editing the same sentence on separate branches.
Try the merge and read the conflict markers before resolving the file together.
Keep the agreed final wording, remove all conflict markers, then stage and
commit the resolution.

**Done when:** the resulting history contains both separate changes and the
conflicted file contains one deliberate, agreed version.

**Debrief:** What information did Git preserve in the conflict? Who should
decide the final wording?

For complete commands to create two independent branches and a deliberate
conflict, use [lab 2 in the guided lab
guide](./labs/README.md#lab-2--integrate-two-branches-and-resolve-a-conflict).

## Safe conflict routine

1. Stop and inspect `git status`.
2. Open each conflicted file and read both sides of the conflict.
3. Agree on the intended result with the other contributor.
4. Edit the file and remove `<<<<<<<`, `=======`, and `>>>>>>>` markers.
5. Run the relevant checks, then stage the resolved file.
6. Inspect `git diff --staged` and complete the merge as Git instructs.

Do not choose a side blindly: that can discard a teammate's work.

Continue with [remotes and shared work](./m03-remotes.md).
