# 03 - Git

## Branches

A branch is an independent line of development used to work on separate tasks.

Common commands:

- `git branch`: list branches
- `git switch -c feature/name`: create and switch to a new branch
- `git switch main`: switch back to main
- `git merge feature/name`: merge changes into the current branch
- `git branch -d feature/name`: delete a local branch after merging

Typical workflow:

1. Start from `main`.
2. Create a feature branch.
3. Make changes and commit them.
4. Switch back to `main`.
5. Merge the feature branch.
6. Push the updated `main`.
