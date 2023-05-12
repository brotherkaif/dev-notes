# GIT: Interactive Rebasing

## Overview

Interactive rebasing is a Git command that allows you to modify the order, content, and structure of your commit history. It is a powerful tool that can be used to clean up your history, fix mistakes, and make your code easier to understand.

To start an interactive rebase, you need to be on the branch that you want to rebase. Then, you can use the following command:

```bash
git rebase -i <SHA-1>
```

Where `<SHA-1>` is the SHA-1 hash of the commit that you want to start the rebase from.

Once you run this command, Git will open a text editor with a list of your commits. Each commit will be listed with a number and a command. The commands are as follows:

- `pick`: This command tells Git to apply the commit as-is.
- `edit`: This command tells Git to stop at the commit and allow you to edit the commit message or the contents of the commit.
- `squash`: This command tells Git to combine the current commit with the next commit.
- `drop`: This command tells Git to delete the commit.

You can use any combination of these commands to modify your commit history. Once you are finished, you can save the text editor and exit. Git will then apply your changes.

Here are some examples of how you can use interactive rebasing:

- To fix a mistake in a commit, you can use the `edit` command to stop at the commit and edit the commit message or the contents of the commit.
- To combine two commits, you can use the `squash` command to combine the two commits into one commit.
- To delete a commit, you can use the `drop` command to delete the commit.

Interactive rebasing is a powerful tool that can be used to clean up your commit history and make your code easier to understand. However, it is important to note that interactive rebasing does rewrite your history, so it is important to use it carefully.

## Example

Let's say you have the following commit history:

```bash
$ git log

commit 831c549788579f5f94a375992752922635607625
Author: John Doe <johndoe@example.com>
Date:   Fri Mar 11 10:00:00 2023 -0800

    Initial commit

commit 123456789abcdef0123456789abcdef0123456789
Author: John Doe <johndoe@example.com>
Date:   Fri Mar 11 10:15:00 2023 -0800

    Add some code

commit 987654321abcdef0123456789abcdef012345678
Author: John Doe <johndoe@example.com>
Date:   Fri Mar 11 10:30:00 2023 -0800

    Fix a bug
```

Now, let's say you want to combine the second and third commits into a single commit. You can do this using interactive rebasing.

First, switch to the branch that you want to rebase:

```bash
$ git checkout feature
```

Then, run the following command to start an interactive rebase:

```bash
$ git rebase -i HEAD~2
```

This will open a text editor with a list of your commits. Each commit will be listed with a number and a command. The commands are as follows:

- `pick`: This command tells Git to apply the commit as-is.
- `edit`: This command tells Git to stop at the commit and allow you to edit the commit message or the contents of the commit.
- `squash`: This command tells Git to combine the current commit with the next commit.
- `drop`: This command tells Git to delete the commit.

To combine the second and third commits, change the `pick` command for the third commit to `squash`. Then, save the text editor and exit.

Git will then combine the second and third commits into a single commit. The new commit will have the commit message of the second commit, and the contents of the third commit.

Your new commit history will look like this:

```bash
$ git log

commit 831c549788579f5f94a375992752922635607625
Author: John Doe <johndoe@example.com>
Date:   Fri Mar 11 10:00:00 2023 -0800

    Initial commit

commit 987654321abcdef0123456789abcdef012345678
Author: John Doe <johndoe@example.com>
Date:   Fri Mar 11 10:30:00 2023 -0800

    Add some code and fix a bug
```
