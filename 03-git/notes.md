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

## Merge conflicts

A merge conflict happens when Git cannot automatically combine changes from two branches.

This usually happens when two branches change the same lines in the same file.

Conflict markers:

- `<<<<<<< HEAD`: current branch version
- `=======`: separator between versions
- `>>>>>>> branch-name`: incoming branch version

To resolve a conflict:

1. Open the conflicted file.
2. Choose or combine the correct changes.
3. Remove the conflict markers.
4. Stage the resolved file:
   - `git add <file>`
5. Finish the merge:
   - `git commit`

Useful command:

- `git status`: shows which files are in conflict and what to do next.
