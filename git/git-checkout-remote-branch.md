# With One Remote
With Git versions ≥ 1.6.6, with only one remote, you can do:
```bash
git fetch
git checkout test
```

`git checkout test` will NOT work in modern git if you have multiple remotes. In this case use:
```bash
git checkout -b test <name of remote>/test
```

Or the shorthand:
```bash
git checkout -t <name of remote>/test
```

# With >1 Remotes
Before you can start working locally on a remote branch, you need to fetch it.

To fetch a branch, you simply need to:
```bash
git fetch origin
```

This will fetch all of the remote branches for you. You can see the branches available for checkout with:
```bash
git branch -v -a
```

With the remote branches in hand, you now need to check out the branch you are interested in, giving you a local working copy:
```bash
git checkout -b test origin/test
```
