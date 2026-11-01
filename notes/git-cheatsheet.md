# Git Cheatsheet

Personal reference for the Git commands I use while learning data engineering.

## How Git moves my work

```text
Working folder  --git add-->  Staging area  --git commit-->  Local repo  --git push-->  GitHub
(files I edit)                (changes I picked)              (saved history)             (remote copy)
```

## The core loop

```bash
git status                       # what changed?
git diff                         # exactly what changed
git add <file>                   # stage a change
git commit -m "Add something"    # save a snapshot
git push                         # send to GitHub
git log --oneline                # view history
```

## Branches and pull requests

```bash
git switch -c <branch-name>      # create and switch to a branch
git push -u origin <branch-name> # publish the branch
# open a pull request on GitHub, review it, merge it
git switch main
git pull                         # sync local main
git branch -d <branch-name>      # delete the merged branch
```

## Undo

| Situation | Command |
|---|---|
| Discard edits to a file (before staging) | `git restore <file>` |
| Unstage a file but keep the edits | `git restore --staged <file>` |
| Fix the last commit message (not yet pushed) | `git commit --amend -m "New message"` |

## Rules I follow

- One change per commit; write the message in the imperative ("Add SQL notes").
- Never commit secrets, `.env` files, virtual environments, or large data files. Put them in `.gitignore`.

## Lessons learned

### Nov 1, 2026

- Learned how Git moves work through four places: working folder, staging area, local repo, and GitHub.
- Completed the branch, pull request, and merge cycle on `de_learning`.