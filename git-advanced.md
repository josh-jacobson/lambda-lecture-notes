# Advanced git workflow tips

## Rebase
If there a bunch of new changes on GitHub and you want to make sure your new commits get applied on top, simply run:
`git rebase origin main`

(or `master` or whatever the main branch is called in your repo). This often results in conflicts that you have to resolve manually, so I like to backup my current changes to another branch before rebasing.

## Merging vs Rebasing

Here's the difference:
* Merging two branches brings everything together, with your commit histories combined so everything is in order based on when each commit was made
* Rebasing is a form of "rewriting history", putting all of your new changes on top rather than mixing them in

Every team has their own preferences. I'm personally a fan of rebasing for the cleaner chronology of each new feature in the commit history.

## A helpful shortcut: `head`
`head` points to the latest commit on your current branch.

Instead of typing out `git push origin my-current-branch-name` you can simply say `git push origin head`

As long as you add the `-u` flag to map to the upstream branch in GitHub the first time you push, you won't really have to worry about specifying where to push anyhow. But for that first push, it's easy to make a typo and I prefer to use `head` because I know it'll automatically map to a branch with the same name on GitHub.

So I just always default to this (feel free to assign it to a shorter alias):
```
git push -u origin head
```

## Understand local, remote and "origin"
When you clone a repo from GitHub, git will automatically assign a "remote" repository called origin with the address you cloned from. 

When you create new branches and make commits, that's all part of your *local* git repository. Origin is an entirely separate git repository, and you set up a mapping where your local branches track changes from the remote branch (including those made by your collaborators), and you can pull those changes down and also push your own newer changes. Know that it's possible to have multiple remote branches as well!
