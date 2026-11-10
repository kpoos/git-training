# Labs and facilitator guide

This is the command-by-command companion to the [Git learning
path](../toc.md). Follow the labs in order: labs 1–2 work locally, labs 3–4
use a shared GitHub practice repository, lab 5 practices safe recovery, and
lab 6 combines the workflow. Commands are grouped into steps with checks so
learners can compare what they see with the expected state. Each worked
exercise includes the exact starter or changed file content needed for its
commits; text marked as a replacement is a change to an existing file, not a
second file to add.

The commands use a POSIX-style shell (macOS, Linux, or Git Bash). If a command
fails, stop and read the complete message; do not keep running later commands
as if it succeeded. Git's output can vary slightly by version.

## Preparation

### Check Git and set your commit identity

Run:

```sh
git --version
git config --global user.name
git config --global user.email
```

The first command should print a Git version. If either identity command
prints nothing, configure it:

```sh
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use the email appropriate for the training environment. A GitHub `noreply`
address is an option if you do not want your personal email shown in commits.
These settings label commits; they are not GitHub sign-in credentials.

### Get a safe practice repository

For labs 1–2 and 5, use a new local directory. For labs 3–4 and 6, ask the
facilitator to provide a disposable GitHub repository and permission to push
branches (or a fork for each learner). Do not use production repositories or
put passwords, access tokens, private keys, or personal data in a repository,
command, screenshot, or remote URL.

The examples use a default branch called `main`. For a repository whose
default branch has a different name, substitute the actual name wherever
`main` appears. To see the current branch:

```sh
git branch --show-current
```

### How to work through each lab

Take turns as **operator** (predicts and runs a command), **reviewer** (checks
the result), and **facilitator/navigator** (asks about state before the next
step). Before changing state, say whether the change is in the working tree,
staging area, local history, or remote repository. At every checkpoint,
compare the actual result with the expected result before continuing.

## Lab 1 — Make a history your teammate can read

**Module:** [01 — Git and local history](../m01-foundations.md)

**Time:** 35–45 minutes

**Goal:** Create a repository, commit a text file and a small source-code
file separately, and explain what each commit contains.

**You need:** A new practice directory; no network access is needed.

**Finished evidence:** Three focused commits, a clean working tree, and a
partner's accurate explanation of the history.

### 1. Create a repository

Choose a location where a new folder named `git-practice` does not already
exist, then run:

```sh
mkdir git-practice
cd git-practice
git init -b main
git status
```

If your Git version does not support `git init -b main`, use `git init`, then
rename the initial branch:

```sh
git branch -M main
```

**Check:** `git status` says you are on `main` and there are no commits yet.
The exact wording differs between Git versions. If `mkdir` says the folder
already exists, choose another name rather than deleting an existing folder.

### 2. Create and inspect the first file

Create `README.md` with this exact content:

```markdown
# Team Playbook

A small collection of agreements and tips for working together.
```

Then inspect the repository:

```sh
git status
git diff
```

**Check:** `README.md` is listed as an untracked file. `git diff` may show
nothing because ordinary `git diff` does not display untracked files.

Stage the file, then inspect exactly what is about to be committed:

```sh
git add README.md
git status
git diff --staged
```

**Check:** The file is staged (usually shown as a new file), and the staged
diff contains the title and description. If the content is wrong, edit the
file and run `git add README.md` again before committing.

### 3. Record the first commit

```sh
git commit -m "Add team playbook introduction"
git status
git log --oneline
```

**Check:** The log has one commit with the message above, and the working tree
is clean. A commit records the staged content locally; it does not publish
anything to GitHub.

### 4. Add a source-code file in its own commit

Create `greeting.py` with this exact content:

```python
def greet(name):
    return f"Hello, {name}!"
```

This is a small Python example to give the branch and conflict exercises a
real code change. You do not need to install Python or run the program to
practice Git.

Review and commit only the source file:

```sh
git status
git diff
git add greeting.py
git diff --staged
git commit -m "Add greeting function"
git status
```

**Check:** `git show --stat HEAD` lists only `greeting.py`; `git status` is
clean.

### 5. Add working agreements in a third commit

Create `working-agreements.md` with this exact content:

```markdown
# Working agreements

- Keep each change focused on one task.
- Ask before changing another person's work.
- Review the staged diff before committing.
```

Inspect, stage, and check this file:

```sh
git status
git diff
git add working-agreements.md
git diff --staged
git commit -m "Document team working agreements"
git status
git log --oneline --decorate
```

**Check:** There are three focused commits: the README, the source-code
function, and the agreements file. `git status` reports a clean working tree.

### 6. Ask a partner to reconstruct the story

Show your partner the history and each commit's patch:

```sh
git log --oneline
git show --stat HEAD
git show HEAD
git show HEAD~1
git show HEAD~2
```

`HEAD` names the current commit; `HEAD~1` and `HEAD~2` name its first and
second prior commits in this simple history. Ask the partner to describe
which files each commit added and why keeping the code change separate makes
the history easier to understand.

**Debrief:** Could your partner infer why the two changes were separate? Did
staging help you review what would be recorded?

## Lab 2 — Integrate two branches and resolve a conflict

**Module:** [02 — Branches and merging](../m02-branches.md)

**Time:** 40–55 minutes

**Goal:** Merge two independent changes, then create and resolve a deliberate
content conflict.

**You need:** The clean `git-practice` repository from lab 1.

**Finished evidence:** Both independent additions remain, the conflict has an
agreed resolution, and no conflict markers remain.

### 1. Start from a clean branch

```sh
git status
git switch main
git log --oneline
```

Continue only if the working tree is clean. If not, stop and inspect
`git status` and `git diff`; do not hide or discard work to force the lab to
continue.

### 2. Make and merge the first independent change

```sh
git switch -c add-review-checklist
```

Create `review-checklist.md` with this exact content, then inspect and commit
it:

```markdown
# Review checklist

- [ ] Does the change solve the agreed task?
- [ ] Is the diff limited to the intended change?
- [ ] Are instructions and examples clear to a new teammate?
```

```sh
git status
git add review-checklist.md
git diff --staged
git commit -m "Add review checklist"
git switch main
git merge --no-ff --no-edit add-review-checklist
git status
```

**Check:** Git reports a successful merge. `review-checklist.md` exists on
`main`. `--no-ff` keeps a visible merge commit in this exercise; ordinary
merges may use a different history shape.

### 3. Make and merge a second independent change

```sh
git switch -c add-meeting-checklist
```

Create `meeting-checklist.md` with this exact content:

```markdown
# Meeting checklist

- [ ] Share the goal and agenda before the meeting.
- [ ] Record decisions and owners.
- [ ] Send follow-up actions to the team.
```

Then:

```sh
git status
git add meeting-checklist.md
git diff --staged
git commit -m "Add meeting checklist"
git switch main
git merge --no-ff --no-edit add-meeting-checklist
git status
git log --oneline --graph --decorate --all
```

**Check:** Both checklist files exist on `main`. The graph shows both
branches' contributions integrated. A partner should be able to identify
which commit added each file.

### 4. Create two branches that change the same line of code

Start both branches from the same current `main` commit:

```sh
git switch main
git switch -c conflict-first
```

In `greeting.py`, replace this existing line:

```python
    return f"Hello, {name}!"
```

with this version:

```python
    return f"Hello, {name.title()}!"
```

Review and commit the first version:

```sh
git diff -- greeting.py
git add greeting.py
git diff --staged
git commit -m "Format names in greeting"
```

Return to the common starting point and make a different edit to the same
line:

```sh
git switch main
git switch -c conflict-second
```

On `conflict-second`, `greeting.py` still contains the original line because
this branch starts from `main`, not from `conflict-first`. Replace that same
original line with this different version:

```python
    return f"Welcome, {name}!"
```

Then commit the second version:

```sh
git diff -- greeting.py
git add greeting.py
git diff --staged
git commit -m "Change greeting to welcome"
```

**Check:** `conflict-first` and `conflict-second` each have one new commit,
and both replace the same original source-code line with different text.

### 5. Merge one side, then trigger and resolve the conflict

Merge the first branch:

```sh
git switch main
git merge --no-ff --no-edit conflict-first
```

Now merge the second branch:

```sh
git merge --no-ff --no-edit conflict-second
```

Git should report a conflict in `greeting.py`. Do not run another merge or
commit yet. Inspect the state and the conflict:

```sh
git status
git diff
```

Open `greeting.py`. Git has inserted conflict delimiters around the competing
return statements. The combined diff shows the `HEAD` version from `main` and
the incoming version from `conflict-second`; the precise labels can vary.
Discuss the behavior the function should have and replace the entire
conflicted function with this agreed result:

```python
def greet(name):
    return f"Welcome, {name.title()}!"
```

Save the file, then verify the markers are gone and stage the resolution:

```sh
git status
git diff -- greeting.py
git add greeting.py
git diff --staged
```

The staged diff should show the agreed function and no merge-marker lines.
Complete the merge:

```sh
git commit
git status
git log --oneline --graph --decorate --all
```

Git may open an editor with a suggested merge message. Keep the suggested
message, save, and close the editor. If unsure how to use the editor, ask the
facilitator before starting the merge rather than aborting or deleting files.

**Check:** `git status` is clean; both independent checklist files remain;
`greeting.py` contains the agreed function and no conflict markers; history
contains the merged work.

**Debrief:** Why did Git stop when both branches replaced the same code line?
What behavior did each version request, and what decision had to come from
the people?

## Lab 3 — Publish a branch without colliding

**Module:** [03 — Remotes and shared work](../m03-remotes.md)

**Time:** 35–50 minutes  
**Goal:** Clone a shared repository, publish a uniquely named branch, and
inspect a teammate's branch without changing the default branch.

**You need:** A facilitator-provided GitHub practice repository or personal
fork, with permission to push branches.

**Finished evidence:** A branch and commit exist locally and remotely; the
default branch was not changed directly.

### Facilitator: create the demo repository and its starter files

Create a new, empty GitHub repository named `git-remote-practice`. Do not
select GitHub's option to add a README or other starter files. In a terminal,
make a local copy of the two starter files below, then connect it to the new
GitHub repository. Replace `<repository-url>` with the clone URL shown by
GitHub; do not put credentials in the URL.

Create `README.md`:

```markdown
# Greeting demo

A tiny Python example used to practice Git branches and pull requests.

Learners add one small, independent tip module under `src/tips/`.
```

Create `src/greetings.py`:

```python
def greet(name):
    return f"Hello, {name}!"
```

Initialize and publish the starter project:

```sh
mkdir git-remote-practice
cd git-remote-practice
git init -b main
mkdir -p src/tips
```

Create the two files shown above in this directory, then run:

```sh
git status
git add README.md src/greetings.py
git diff --staged
git commit -m "Create greeting demo starter"
git remote add origin <repository-url>
git push -u origin main
```

Invite learners as collaborators or have them fork the repository. The empty
`src/tips/` directory does not need to be committed; Git tracks files, not
empty directories.

### 1. Clone the practice repository

Copy the repository's HTTPS or SSH clone URL from GitHub. Do not copy a URL
containing a username, password, or token. Replace `<repository-url>` below
with that URL:

```sh
git clone <repository-url>
cd <repository-directory>
git remote -v
git status
git branch --show-current
```

For example, `<repository-directory>` is usually the repository name. Use the
actual folder created by `git clone`.

**Check:** `git remote -v` shows `origin` pointing at the practice repository.
The working tree is clean. You are on the repository's default branch (often
`main`).

### 2. Create a uniquely named branch

Choose a name with lowercase letters and hyphens, unique among the group, for
example `add-alex-git-tip`:

```sh
git switch -c add-your-name-git-tip
git branch --show-current
```

Substitute your own branch name in every later command. Do not use spaces or
another learner's branch name.

**Check:** The current branch is your new feature branch, not `main`.

### 3. Add a small code example and commit it

Each learner creates a separate file named `src/tips/<your-name>.py`. Replace
`<your-name>` with a short unique name using lowercase letters and
underscores, for example `alex.py`. Use this exact content and replace only
`YOUR NAME`:

```python
"""A short Git tip contributed by YOUR NAME."""


def tip():
    return "Run git status before switching branches."
```

For example, the file for a learner named Alex could be
`src/tips/alex.py`, with this complete content:

```python
"""A short Git tip contributed by Alex."""


def tip():
    return "Run git status before switching branches."
```

The tip is deliberately the same for everyone; each learner's unique file
keeps the branch and pull-request exercises independent.

The author owns their unique file, so learners can work in parallel without
editing the same lines. From the repository directory, create the folder if
needed, create the file, then review and commit it:

```sh
mkdir -p src/tips
git status
git diff
git add src/tips/<your-name>.py
git diff --staged
git commit -m "Add <your-name>'s Git tip"
git status
git log -1 --oneline
```

Replace `<your-name>` in both the file path and commit message. Inspect the
entire staged file in `git diff --staged`. If it includes unrelated content,
unstage it with `git restore --staged src/tips/<your-name>.py`, edit the file,
and inspect it again.

**Check:** The latest commit describes your change, and the working tree is
clean.

### 4. Push and set upstream tracking

```sh
git push -u origin add-your-name-git-tip
git branch -vv
```

Use your actual branch name. The first command publishes the branch and
records its upstream, so later `git push` and `git pull` commands know which
remote branch to use.

**Check:** The push completes without error. `git branch -vv` shows your
branch tracking `origin/add-your-name-git-tip`; the remote branch contains
your `src/tips/<your-name>.py` file.

### 5. Have a partner fetch and inspect your branch

The partner should run these commands from their own clone:

```sh
git fetch origin
git branch --all
git log --oneline --decorate --all
```

Ask them to locate your `origin/add-your-name-git-tip` branch and identify
your commit. Fetching downloads remote references but does not merge them
into the partner's current branch.

**Check:** Your branch is visible under `remotes/origin/` in `git branch
--all`. The default branch remains unchanged.

If push is rejected because the remote branch already exists, stop and check
the branch name with your partner; do not force-push. If authentication
fails, use the organization's approved sign-in flow or ask the facilitator.

**Debrief:** Which branch did your push update? What changed on your
partner's computer after `git fetch`?

## Lab 4 — Review, revise, and merge a pull request

**Module:** [04 — Issues, pull requests, and review](../m04-pull-requests.md)

**Time:** 45–60 minutes

**Goal:** Propose a branch as a pull request (PR), discuss one specific
review comment, make a revision, and merge after approval.

**You need:** A pushed branch from lab 3 and GitHub access to the practice
repository.

**Finished evidence:** The PR has a clear description, a review exchange, and
a merged result; the author can identify the revision commit.

### 1. Open a PR for your branch

On GitHub:

1. Open the practice repository.
2. Select **Pull requests**, then **New pull request** (or the prompt to
   compare your recently pushed branch).
3. Set the **base** to the repository's default branch and the **compare**
   branch to your feature branch. Check both names before continuing.
4. Select **Create pull request**.
5. Give the PR a specific title, such as `Add a Git learning tip`.
6. In the description, state:
   - **Purpose:** what learner need or task this addresses.
   - **Change:** which file or content you added or changed.
   - **Verification:** what you reviewed or checked.
7. Assign your partner as reviewer if the repository permits it, then create
   the PR.

**Check:** The PR shows only your intended diff. If it includes unrelated
changes or targets the wrong base branch, do not merge it; ask the facilitator
to help correct the PR setup.

### 2. Review a partner's PR

The reviewer opens the **Files changed** tab and reads the diff. On the
`return` line, leave this specific suggestion: "Please explain why checking
the working tree before switching branches is useful." If commenting on a
line, use GitHub's line-comment feature; otherwise leave a general review
comment.

Before submitting, choose the review action offered by the repository. Use
**Comment** for discussion, **Request changes** when the change should not
merge yet, or **Approve** only when it is ready. Do not approve your own PR.
A review is about the proposed change; phrase feedback so the author knows
what to consider and why.

### 3. Respond and make a revision if appropriate

The author replies in the PR conversation and accepts the suggestion. For
example, if the branch is `add-alex-git-tip`, change
`src/tips/alex.py` from:

```python
"""A short Git tip contributed by Alex."""


def tip():
    return "Run git status before switching branches."
```

to this complete revised file:

```python
"""A short Git tip contributed by Alex."""


def tip():
    return "Before switching branches, run git status and confirm the working tree is clean."
```

Use your own name in the filename and docstring. Then run these commands on
the same feature branch:

```sh
git status
git diff -- src/tips/alex.py
git add src/tips/alex.py
git diff --staged
git commit -m "Clarify when to check Git status"
git push
```

Replace `alex.py` with your own filename. Because lab 3 set upstream
tracking, `git push` updates the PR branch. If you do not accept a suggestion,
explain your reasoning in the thread instead. Do not make a follow-up commit
just to create activity.

**Check:** The PR's **Commits** and **Files changed** tabs show the updated
branch. The reviewer confirms whether the concern is resolved.

### 4. Merge and synchronize the local repository

Once review and any required checks are complete, use the repository's
allowed merge button and method. The author or facilitator should confirm the
base and compare branches one final time before merging.

After GitHub reports the PR merged, update the local default branch:

```sh
git switch main
git pull --ff-only origin main
git status
git log --oneline --decorate -5
```

If the default branch has another name, substitute it. `--ff-only` prevents
Git from silently creating an unexpected merge when the local and remote
branches have diverged. If it refuses, stop and inspect `git status` and the
history with the facilitator.

**Check:** The merged change appears in the latest history and the working
tree is clean.

**Debrief:** What context made the PR easy to review? How did the author show
that feedback was considered?

## Lab 5 — Recover without panic

**Module:** [05 — Conflicts and safe recovery](../m05-recovery.md)

**Time:** 35–50 minutes

**Goal:** Distinguish an unstaged edit, a staged edit, and a committed change;
practice safe unstage and revert operations; resolve a merge conflict.

**You need:** The `git-practice` repository from labs 1–2. Work only in this
disposable repository.

**Finished evidence:** Each operation's effect is explained, the committed
change remains visible in history, and the working tree is clean at the end.

### Safety pause — identify the state before every undo

Before an undo command, run:

```sh
git status
git diff
git diff --staged
git log --oneline -5
```

Say aloud what is modified, staged, committed, and published. The following
exercises are local and disposable. Do not practice `git reset --hard` or
force-push as a recovery shortcut. If a command's effect is unclear, stop and
ask for help.

### 1. Unstage a change and keep the edit

Confirm you are in the lab repository and on `main`:

```sh
git switch main
git status
```

At the end of `greeting.py`, change the function's return statement from the
version currently on `main`:

```python
    return f"Welcome, {name.title()}!"
```

to this version:

```python
    return f"Welcome, {name.strip().title()}!"
```

The only difference is that the edited version removes leading and trailing
spaces from the input name. Stage the changed source file and verify its
state:

```sh
git add greeting.py
git status
git diff --staged
```

Now unstage it without discarding the edit:

```sh
git restore --staged greeting.py
git status
git diff -- greeting.py
git diff --staged
```

**Check:** `greeting.py` is modified but no longer staged;
`git diff -- greeting.py` still shows the code edit, and `git diff --staged`
is empty. The file's edit remains in your working tree.

Stage and commit the change so the next exercise starts cleanly:

```sh
git add greeting.py
git diff --staged
git commit -m "Trim spaces in greeting names"
git status
```

**Check:** `git status` is clean.

### 2. Revert a commit by adding a new commit

Inspect the latest commit, then reverse it:

```sh
git log -1 --oneline
git show --stat HEAD
git revert --no-edit HEAD
```

`--no-edit` uses Git's default revert message. Inspect the result:

```sh
git status
git log --oneline -3
git show --stat HEAD
```

**Check:** The history now contains a new revert commit and still contains
the original practice-tip commit. The change is reversed in the current
files, but the original commit was not erased or rewritten.

If a revert reports conflicts, stop and inspect `git status`; do not guess
which version to keep. Ask the facilitator to guide the resolution.

### 3. Resolve a conflict using the safe routine

Create a fresh conflict on `main` so this exercise is independent of the
conflict resolution already completed in lab 2. The preceding revert restores
the version of `greeting.py` that was on `main` before the trim-spaces commit.
First confirm the repository is clean:

```sh
git status
git switch main
```

In `greeting.py`, the original line on `main` is:

```python
    return f"Welcome, {name.title()}!"
```

```sh
git switch -c recovery-first
```

Replace the original return line with this first-branch version:

```python
def greet(name):
    return f"Hello, {name.title()}!"
```

Inspect and commit that source-code change:

```sh
git diff -- greeting.py
git add greeting.py
git diff --staged
git commit -m "Use hello wording in greeting"
```

Return to the common starting point and create a second branch:

```sh
git switch main
git switch -c recovery-second
```

On `recovery-second`, `greeting.py` still has the original `Welcome` line.
Replace it with a different version:

```python
def greet(name):
    return f"Hi, {name.title()}!"
```

Inspect and commit this source-code change:

```sh
git diff -- greeting.py
git add greeting.py
git diff --staged
git commit -m "Use short greeting wording"
```

Merge the first branch, then attempt the second:

```sh
git switch main
git merge --no-ff --no-edit recovery-first
git merge --no-ff --no-edit recovery-second
git status
```

Git should pause with a conflict in `greeting.py`. Inspect the combined diff
and then the file:

```sh
git diff --cc greeting.py
git status
```

Open `greeting.py`. It now contains both branch versions between Git's
conflict delimiters; do not keep the delimiters in the final source file.
Agree on a final behavior, for example:

```python
def greet(name):
    return f"Hello, {name.title()}!"
```

Resolve it using this
routine:

1. Run `git status` and identify every conflicted file.
2. Open each file and read both versions between the conflict markers.
3. Agree with the other contributor on the intended final content.
4. Edit the file to contain only that final content; remove all conflict
   markers.
5. Run `git diff` and any relevant checks.
6. Run `git add greeting.py` and inspect `git diff --staged`.
7. Complete the merge with
   `git commit -m "Resolve greeting function conflict"` if Git has not already
   completed it.
8. Run `git status` and confirm there are no unresolved paths.

**Check:** A conflict is a request for a human decision, not a command to
discard one side. The final file contains the agreed result and the history
records the integration.

**Debrief:** Why is `git restore --staged` different from `git restore
<file>`? Why is `git revert` generally appropriate for a commit that may
already have been shared?

Continue with [the team capstone](../m06-capstone.md).

## Lab 6 — Ship a learning guide as a team

**Module:** [06 — Team capstone](../m06-capstone.md)

**Time:** 60–90 minutes

**Goal:** Plan, contribute, review, and merge a small guide using issues,
focused branches, and PRs.

**You need:** The shared GitHub practice repository from labs 3–4; at least
two learners.

**Finished evidence:** Each contribution has an agreed task, a reviewed PR,
and a merged result; the team completes the checklist and retrospective.

### 1. Agree on a small feature and its definition of done

Use the shared `git-remote-practice` repository from lab 3. Run this worked
example as one issue with one author and a different reviewer. For the example,
the issue is: **Make `greet` normalize a name and document the
behavior.** The expected result is that `greet("  alex ")` returns
`"Hello, Alex!"`. The author changes the function and adds a test and a short
guide page. Agree on:

- The intended reader and what they should learn.
- The exact files in scope: `src/greetings.py`,
  `tests/test_greetings.py`, and `docs/greeting-tips.md`.
- A consistent structure (for example: purpose, steps, checks, and
  troubleshooting).
- What review and verification each contribution needs.
- A definition of done: clear wording, accurate commands, reviewed diff, and
  no secrets or unrelated files; the test passes if Python is available.

Create a GitHub issue with this description:

```text
## Goal
Normalize whitespace and capitalization in greet(name).

## Acceptance criteria
- greet("  alex ") returns "Hello, Alex!".
- Add a test for the normalized name.
- Document the expected input and output.
```

Keep each contribution small enough for one reviewer to understand in a few
minutes. Assign an author and a different reviewer; rotate roles so every
learner does both.

### 2. Start a contribution from the latest default branch

Each author updates their local copy before creating a branch. Run from the
repository directory, substituting the actual default branch name if it is
not `main`:

```sh
git status
git switch main
git pull --ff-only origin main
git status
```

Continue only when the working tree is clean and the pull succeeds. Create a
branch that names the task:

```sh
git switch -c add-greeting-normalization
git branch --show-current
```

Use a unique branch name for each task. Do not work directly on `main`.

### 3. Make and verify the example contribution

Before creating the example files, create their parent directories:

```sh
mkdir -p tests docs
```

In the example branch `add-greeting-normalization`, replace
`src/greetings.py` with:

```python
def greet(name):
    normalized_name = name.strip().title()
    return f"Hello, {normalized_name}!"
```

Create `tests/test_greetings.py` with:

```python
import unittest

from src.greetings import greet


class GreetTests(unittest.TestCase):
    def test_strips_spaces_and_capitalizes_name(self):
        self.assertEqual(greet("  alex "), "Hello, Alex!")


if __name__ == "__main__":
    unittest.main()
```

Create `docs/greeting-tips.md` with:

```markdown
# Greeting function

The `greet(name)` function removes spaces at the start and end of a name and
capitalizes it before returning a greeting.

Example: `greet("  alex ")` returns `Hello, Alex!`.
```

Before staging, inspect the complete set of files and changes:

```sh
git status
git diff
```

`git status` should list the new files, but `git diff` does not display
untracked files. Stage exactly the three files for this issue and inspect
their complete contents in the staged diff:

```sh
git add src/greetings.py tests/test_greetings.py docs/greeting-tips.md
git status
git diff --staged
```

If Python 3 is installed, run the test from the repository root:

```sh
python3 -m unittest discover -s tests
```

If that command is unavailable, state that the test could not be run; still
review the test and source diff with a partner. If the staged diff is correct,
commit with a message describing the change:

```sh
git commit -m "Normalize names in greeting function"
git status
git log -1 --oneline
```

**Check:** The commit contains the function, test, and documentation file,
with no unrelated changes. If the staged diff contains unrelated work,
unstage only the unintended path with `git restore --staged <path>`, then
inspect the staged diff again. Do not commit another learner's work.

### 4. Publish and open a PR

```sh
git push -u origin add-greeting-normalization
```

On GitHub, create a PR from this branch to the default branch. Include the
issue, the purpose, a summary of the content, and how it was checked. For
this change, checks include running the unit test if Python is available,
reviewing the rendered Markdown, and confirming the code, test, and guide
agree on the example input and output.

The reviewer compares the PR against its base, checks it against the team's
definition of done, and leaves actionable feedback. The author responds and
pushes any requested revision to the same branch. Follow lab 4's detailed
review and synchronization steps.

### 5. Merge, update, and repeat

After approval and any required checks, merge using the repository's allowed
method. Each learner then updates their local default branch:

```sh
git switch main
git pull --ff-only origin main
git status
```

Before beginning another contribution, create its branch from this updated
default branch. For additional learners, create a separate issue and use
different files or a different independent feature; do not have two authors
make the same change to the same files at the same time. Continue until each
learner has authored and reviewed at least one contribution.

### 6. Confirm the result and reflect

As a team, inspect the merged files on GitHub and locally. Confirm that the
guide reads as one coherent document, links work, examples are safe, and no
unintended files were committed. Review the merged history:

```sh
git log --oneline --graph --decorate -10
git status
```

Complete the checklist:

- [ ] Each change traces to an issue or agreed task.
- [ ] Each author used a focused branch and a descriptive commit.
- [ ] Each PR explains its purpose and checks.
- [ ] A teammate reviewed every PR; review feedback was resolved or discussed.
- [ ] All intended contributions are merged and the guide is coherent.
- [ ] No credentials, private information, or unrelated files were committed.
- [ ] Each learner can explain how a local edit became a merged change.

Retrospective questions: Where did communication prevent a Git problem?
Which review comment improved the guide most? What would you change about
the team's workflow next time?

## Facilitator prompts and stuck-state procedure

Ask these questions before giving a command:

- What does `git status` say right now?
- Is the change unstaged, staged, committed locally, or published?
- Which branch are you on, and which branch will this command affect?
- What should change after this command? What should remain unchanged?
- Have you reviewed `git diff` or `git diff --staged`?
- Could another teammate already depend on this commit?

If someone is stuck:

1. Stop before running another state-changing command.
2. Capture the output of `git status`, `git branch --show-current`, and the
   command that failed.
3. Inspect `git diff` and `git diff --staged`; do not discard edits.
4. Read the error message together and identify whether it concerns the
   working tree, merge, branch, remote, or authentication.
5. Ask the facilitator before using reset, force-push, or any command whose
   effects are unclear.

Never use `git push --force` or `git reset --hard` in these labs. A learner
can always pause, preserve the current state, and ask for help.
