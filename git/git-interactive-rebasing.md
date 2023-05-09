# GIT: Interactive Rebasing

## Scenario

- You are working on a branch and `main` contains newer changes
- You have conflicts that need resolving between the two branches

## Steps

- Ensure both `main` and your `<branch>` are both up to date using `git pull`

```bash
git checkout main
git pull
git checkout <branch>
git pull
```

- Whilst the `<branch>` is checked out, initiate an interactive rebase session
- IMPORTANT: You might want to do this in a separate persistent terminal session instead of the integrated terminal in your code editor

```bash
git rebase -i origin/main
```

- This will open a git commit message in vim that will allow you to "cherrypick" the commits you want to skip
- You will want to skip the commits that have come in from `main` and leave commit that you have made on your `<branch>`

- You will then be presented with a flow whereby you will be informed of any merge conflicts
- Go into each file and resolve the conflicts
- Check the status and then stage the changes
- IMPORTANT: Do NOT run `git commit`!

```bash
# check the status is okay
git status

# stage the changes
git add .
```

- When you have staged the changes, you can continue the interactive rebase

```bash
git rebase --continue
```

- This will move the rebase session into the next phase
- Repeat the steps until all the conflicts are resolved, you should see a message indicating a successful rebase

```bash
Successfully rebased and updated refs/heads/<branch>.
```

- IMPORTANT: you need to force push your changes (as you have essentially re-written history)

```bash
git push --force
```
