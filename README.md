# Collaborative Git learning path

A practical, team-based introduction to Git and GitHub. Learners move from local
version history to a reviewed, merged contribution using small, safe changes in
a shared practice repository.

The material is original course content informed by the [Pro Git book and
videos](https://git-scm.com/learn) and GitHub's [learning
resources](https://learn.github.com/skills) and [GitHub flow
guide](https://docs.github.com/en/get-started/using-github/github-flow).

## Who this is for

- Beginners who can use a terminal and edit text files.
- Pairs or small teams working in a GitHub repository they are allowed to use.
- Facilitators who want learners to explain their changes and review each
  other's work, not just memorize commands.

No programming language or GitHub CLI is required. The command examples use
Git's command-line interface; GitHub's web interface can be used for pull
requests and review.

## Outcomes

By the end of the path, learners can:

1. Explain the working tree, staging area, commits, and branches.
2. Create readable commits and inspect project history.
3. Share work with a remote repository without overwriting a teammate's work.
4. Use branches, pull requests, and review comments to collaborate.
5. Resolve a simple merge conflict and choose a safe undo operation.
6. Complete a small team contribution from issue to merged pull request.

## Course sequence

| Module | Topic | Team outcome |
| --- | --- | --- |
| [01 — Git and local history](./m01-foundations.md) | Repository, status, staging, commits, diffs | A teammate can understand the commit history |
| [02 — Branches and merging](./m02-branches.md) | Branches, merge, conflict basics | A change is integrated without losing either version |
| [03 — Remotes and shared work](./m03-remotes.md) | Clone, fetch, pull, push, tracking | Each learner publishes a branch and syncs safely |
| [04 — Issues, pull requests, and review](./m04-pull-requests.md) | GitHub collaboration flow | A reviewer gives actionable feedback and author responds |
| [05 — Conflicts and safe recovery](./m05-recovery.md) | Conflict resolution, restore, revert, reset | Learners recover from a deliberately staged mistake |
| [06 — Team capstone](./m06-capstone.md) | End-to-end collaboration | The team ships a reviewed, documented contribution |

Suggested delivery: six sessions of 60–90 minutes, or a self-paced sequence.
Each session should include time for learners to narrate what they see in
`git status` and to review one another's work.

## Getting started

1. Install Git and verify it with `git --version`.
2. Set a name and email for commit attribution:

   ```sh
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

   Use an email address suitable for commits in your training environment.
   GitHub users may choose a GitHub-provided `noreply` address to keep a
   personal address private.
3. Arrange access to a GitHub practice repository. Use a throwaway repository,
   not production code. For a group, the facilitator should create the
   repository and grant only the access learners need.
4. Read the [hands-on task sheet](./hands-on-tasks.md) and [lab
   guide](./labs/README.md), then follow modules in order.

Never put passwords, access tokens, private keys, or other secrets in a
repository or command example. Do not use `git push --force` in shared work.
Exercises use only disposable training content.

## How to learn together

- Rotate author, reviewer, and facilitator/navigator roles.
- Before changing files, agree on the issue or task and the expected result.
- Keep each branch focused on one change; commit in small, meaningful units.
- Review the diff, not just the final file. Ask questions before suggesting a
  solution.
- The author owns resolving review feedback; the reviewer confirms the result.
- End each lab with a short debrief: what changed, what was surprising, and
  what would be done differently on a real project.

## Contents

- [Course index](./toc.md)
- [Hands-on tasks](./hands-on-tasks.md)
- [Labs and facilitator guide](./labs/README.md)
- [References and source mapping](./references.md)
