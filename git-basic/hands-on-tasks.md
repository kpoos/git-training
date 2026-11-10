# Hands-on tasks

Use these tasks alongside the course modules. Work in a disposable practice
repository, not production code. Work in pairs or small teams and rotate the
author and reviewer roles.

For complete command-by-command instructions and expected checkpoints, use
the [guided lab walkthroughs](./labs/README.md).

## Task 1 — Build a readable local history

**Practice:** working tree, staging area, diffs, commits  
**Deliverable:** a local `team-playbook` repository with three focused
commits, including a small source-code change.

1. Create a folder named `team-playbook`, initialize Git, and create
   `README.md` with:

   ```markdown
   # Team Playbook

   A small collection of agreements and tips for working together.
   ```

2. Check `git status`, stage only `README.md`, inspect the staged diff, and
   commit it as `Add team playbook introduction`.
3. Create `greeting.py` with:

   ```python
   def greet(name):
       return f"Hello, {name}!"
   ```

   Inspect and commit only this file as `Add greeting function`.
4. Create `working-agreements.md` with:

   ```markdown
   # Working agreements

   - Keep each change focused on one task.
   - Ask before changing another person's work.
   - Review the staged diff before committing.
   ```

   Inspect and commit it separately as `Document team working agreements`.
5. Show your partner `git log --oneline` and ask them to explain all three
   commits.

**Acceptance checks:** three focused commits; meaningful messages; clean
working tree; partner can explain what each commit contains.

## Task 2 — Collaborate with branches

**Practice:** branches, merging, conflict resolution  
**Deliverable:** two contributions merged into the playbook.

1. Create a branch named `add-review-checklist` and create
   `review-checklist.md` with:

   ```markdown
   # Review checklist

   - [ ] Does the change solve the agreed task?
   - [ ] Is the diff limited to the intended change?
   - [ ] Are instructions and examples clear to a new teammate?
   ```

   Commit the change.
2. Create a second branch from the default branch named
   `add-meeting-checklist`. Create `meeting-checklist.md` with:

   ```markdown
   # Meeting checklist

   - [ ] Share the goal and agenda before the meeting.
   - [ ] Record decisions and owners.
   - [ ] Send follow-up actions to the team.
   ```

   Commit and merge it.
3. Merge both branches into the default branch and inspect the history.
4. For a deliberate code conflict, create two branches from the same `main`
   commit. On `conflict-first`, replace the return line in `greeting.py` with:

   ```python
       return f"Hello, {name.title()}!"
   ```

   On `conflict-second`, replace that same original line with:

   ```python
       return f"Welcome, {name}!"
   ```

   Commit each branch's version.
5. Merge `conflict-first`, then merge `conflict-second`. Inspect the conflict
   in `greeting.py`, agree on a final function, remove Git's conflict
   delimiters, stage the resolution, and complete the merge. For example:

   ```python
   def greet(name):
       return f"Welcome, {name.title()}!"
   ```

**Acceptance checks:** both non-conflicting checklists are present; the
conflicted function reflects the team's decision; no conflict markers remain.

## Task 3 — Share work through a remote

**Practice:** clone, fetch, pull, push, tracking branches  
**Deliverable:** a branch published to the shared GitHub practice repository.

1. Clone the facilitator-provided repository. Confirm the remote with
   `git remote -v`.
2. Create a uniquely named branch, such as `add-<your-name>-git-tip`.
3. Add `src/tips/<your-name>.py` with a unique filename and this content,
   replacing `YOUR NAME` with your name:

   ```python
   """A short Git tip contributed by YOUR NAME."""


   def tip():
       return "Run git status before switching branches."
   ```

   Stage, inspect, and commit only this file.
4. Push the branch with upstream tracking:

   ```sh
   git push -u origin add-your-name-git-tip
   ```

   Replace `add-your-name-git-tip` with your actual branch name.
5. Ask a partner to run `git fetch origin` and locate your branch in
   `git branch --all` or `git log --all --oneline`.

**Acceptance checks:** the branch is on the remote; the default branch has not
been changed directly; both learners can identify the published commit.

## Task 4 — Open and review a pull request

**Practice:** GitHub flow, PR descriptions, review feedback  
**Deliverable:** one reviewed and merged pull request per learner.

1. Open a PR from your task branch to the repository's default branch.
2. Describe the problem, summarize the change, and state what you checked.
3. Ask your partner to review the diff and leave one specific question or
   improvement suggestion.
4. Respond to the comment. Make a follow-up commit if the suggestion is
   accepted, then push the update.
5. Ask the reviewer to confirm the change before merging through GitHub.
6. Update your local default branch after the merge.

**Acceptance checks:** the PR is focused and understandable; feedback has a
clear response; the merged change appears on the default branch.

## Task 5 — Recover safely

**Practice:** unstage, restore, revert, and conflict recovery  
**Deliverable:** a short explanation of each operation and its result.

Use a disposable clone. Before each operation, inspect `git status` and
explain to a partner whether the change is unstaged, staged, committed, or
published.

1. Edit a tracked file and stage it. Run
   `git restore --staged <file>`, then verify the edit is still in the working
   tree.
2. Commit a small source-code change, then run `git revert --no-edit HEAD`.
   Inspect the new history
   and describe why the original commit remains.
3. Create two branches that replace the same return line in `greeting.py`
   with different messages. Merge both branches and resolve the conflict
   with your partner.

**Acceptance checks:** no work is accidentally discarded; the revert is a new
commit; the learner can explain why published history should not be reset.
Do not use `git reset --hard` or force-push.

## Task 6 — Team capstone: publish a learning guide

**Practice:** complete team collaboration workflow  
**Deliverable:** a small Git learning guide built through reviewed PRs.

1. Agree on the guide's audience, format, file structure, and a definition of
   done.
2. Create one task or issue per contribution. Examples: a Git vocabulary
   page, a command reference, or a troubleshooting note.
3. Each author creates a branch from the latest default branch and makes one
   focused contribution.
4. Each author opens a PR with a summary and verification notes.
5. A different teammate reviews every PR. Rotate roles so each learner is an
   author and a reviewer.
6. Address the feedback, merge approved changes, and confirm the final guide
   is consistent.
7. Hold a short retrospective and record one improvement for the next
   collaboration.

**Acceptance checks:**

- [ ] Every contribution has a task and a focused branch.
- [ ] Every PR has a useful description and a teammate review.
- [ ] Review feedback is resolved or discussed.
- [ ] The guide is coherent, and all intended contributions are merged.
- [ ] No credentials, private information, or unrelated files were committed.
- [ ] Each learner can explain the path from local edit to merged change.

## Optional extension

Fork a public training repository (or ask the facilitator for a fork-based
exercise), make a small documentation improvement in your fork, and propose
it upstream with a PR. Do not submit practice changes to a real project
without permission.
