# Git: Working with Remote Branches

## Learning Goals

- Demonstrate getting updates from remote
- Demonstrate merging branches
- Demonstrate deleting branches
- Demonstrate updating remotes and merging changes in one step

## Introduction

Remember we mentioned going into the wilderness &mdash; no Wi-Fi, no Instagram,
etc.? Getting updates to branches come into play when there are branches that
live on a remote repository. 

## Demonstrate Getting Updates From Remote

If you wanted to cache all the information about all the branches on all
your remotes, you need to use `git fetch` to update the cache for each remote
name.

Let's suppose a colleague has created a new branch and pushed it to a location
that you _both_ use as your `origin` remote. To freshen your local repository
issue:

```bash
$ git fetch
```

Git, yet again, assumes you mean `origin`, but if you had multiple remotes, you
might provide a name like `my-startup`.


```bash
$ git fetch my-startup
```

This synchronizes your remote tracking branches with what's going on on the
remotes. Because of this, your remote tracking branches update. Go into the
heart of the desert and you will have ***all*** the commits for all the
branches. You'll have their histories tracing back to the initial commit.

`git fetch` **only** downloads new data from a remote repository. Fetch will
never change anything on your local branch. Fetching is what you do when you
want to fetch all the changes that happened in a remote repository since your
last sync.

> **IMPORTANT**: Your local tracking branch is only as up-to-date as the last
> time we **explicitly** downloaded the data from the remote.

Here, the `git fetch` command is being used.

!["git fetch"](https://curriculum-content.s3.amazonaws.com/prework/git-workflow/git%20fetch.gif)

## Demonstrate Merging Branches

Merging allows us to take branches and integrate their content into another
branch. From Git's point of view, it doesn't care whether the branch is local
or remote or remote-tracking. It finds the difference between the branch you're
on and the branch you're merging in and weaves them in together.

We can use `git merge other-branch-name` to integrate the changes from one
branch to the branch to the branch we are currently on. Here are some examples

Assuming we're on `master`:

```bash
$ git merge other-branch
$ git merge origin/idea-my-friend-had
$ git merge my-startup/time-travel-engine
```

So, if we want to take the changes we created on `new-branch-name` and merge
them back into the `master` branch, now that we've confirmed the changes are
safe to integrate, we do so by using these commands:

```bash
git checkout master # This switches us back to the master branch
git merge new-branch-name # This integrates our new branch, new-branch-name, and its changes into master
```

Now all the changes that were made on the branch `new-branch-name` are
integrated into `master`. With work on this branch completed and merged, we no
longer need it. Any additional work moving forward can be done on a new branch.

## Demonstrate Deleting Branches

Since we've merged our changes into master, we can safely delete our local version
of `new-branch-name`. A branch can be deleted by providing the `-d`/`–D` options
with the `git branch` command. Before deleting the `new-branch-name`, we should
be on another branch. Currently, we're still on `master`.

The `-d` option stands for `--delete`, which would delete the local branch only
if you have already _pushed_ and _merged_ it with your remote branches.

The `-D` option stands for `--delete --force`, which deletes the branch
regardless of its push and merge status. Be careful with the usage of this one,
however, this is useful when you have a branch with changes that you don't want
to merge (maybe you experimented with things here and decided to throw them
out).

To delete an obsolete local branch (that has been pushed and merged), we type
`git branch -d <branch-to-delete>`. To make sure this branch was successfully
deleted, we type `git branch`. It should no longer exist in the list of local
branches.

With `git branch -d <branch name>` we get a little warning before it's deleted.
IF it has not been pushed and merged, it will reject the command. With
`git branch -D <branch name>`, it will force-delete the branch without warnings.

!["git branch -d vs. git branch -D"](https://curriculum-content.s3.amazonaws.com/prework/git-workflow/git%20branch%20delete.gif)

To delete the remote tracking branch, we can use `git push <remote_name (most
likely origin)> --delete <branch-name>`. To list all remaining remotes, again,
we can type `git branch -a`. It should no longer exist in the list of remote
branches.

## Demonstrate Fetching and Updating the Local Branch

You might think that fetching (to update the cache) and then merging (to pull
the changes into the local tracking branch you're on) is an unnecessarily two-step long process.
If you're on a local tracking branch, you can issue `git pull`. This will:

1. Run `git fetch` and update all the remote tracking branches
2. Bring in the changes, if any, from the remote tracking branch to your local
   tracking branch

The following are equivalent (assume we're on `new-idea` local tracking branch):

```bash
$ git fetch origin
$ git merge origin/new-idea
```

```bash
$ git pull origin/new-idea
```

Since we're on a local tracking branch, Git will assume you mean "the branch of
the same name" at `origin`, if you've been following the code patterns we've
given to you.

```bash
$ git pull
```

## Conclusion

Retrieving branches from remote repositories allows us to pick up where we left
off, or add onto someone's work. Some developers will be fixing bugs, others
will be implementing new features, etc. Branch-based development allows us to
stay organized and work more freely and collaboratively.

## Resources

* [What is the difference between ‘git pull’ and ‘git fetch’?](https://www.javacodegeeks.com/2018/09/git-pull-git-fetch.html)
* [What's the difference between git fetch and git pull?](https://www.git-tower.com/learn/git/faq/difference-between-git-fetch-git-pull)
* [git fetch](https://www.atlassian.com/git/tutorials/syncing/git-fetch)
* [Delete a local and a remote GIT branch](https://koukia.ca/delete-a-local-and-a-remote-git-branch-61df0b10d323)
