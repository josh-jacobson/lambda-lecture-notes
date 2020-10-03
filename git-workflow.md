# Git workflow: tips and tricks


## A typical workflow
* fork to your own repo (remember to do this before you clone!)
* on the GitHub page for your forked repo (should be under your own username), copy the git url from the code button
* `git clone {url}`
* cd into new directory
* Create a new branch:
```
git checkout -b 'feature-branch-name'
```
* !CODE! ☕️
* git add .
* git commit -m 'Add new feature message...'
* git push origin -u fname-lname
* !CODE SOME MORE!
* git add .
* git commit -m 'made something'
* git push

## Collaborating on GitHub and keeping your branch up to date

The first time you push a new branch, be sure to include the `-u` flag (or `--set-upstream`) to make sure git knows that you'd like to map your local branch to a branch of the same name on GitHub. Git is set up for a wide range of use cases (and existed long before GitHub), so it doesn't assume this intuitive 1:1 mapping by default. But once you've run this command just once, you should be able to `git pull` and `git push` without the extra typing in the future.

## Pushing your branch to GitHub
``` 
git push origin head
```

## Merging in the latest changes from GitHub
```bash
git pull origin master
```

This updates your local codebase with the latest code from GitHub. Usually you can simply type `git pull`

## Merging 
When working on a team, you'll often be collaborating with other developers and need to 

Here's the difference:
* Merging two branches mixes everything togetherwill bring everything together, with your commit histories mixed in

Every team has their own preferences. I personally like rebasing for a few reasons, but you're free to choose any workflow that works best for you and your team!

## Squashing commits
`git commit --amend`


## Understand local, remote and "origin"
When you clone a repo from GitHub, git will automatically assign a "remote" repository called origin with the address you cloned from. 

When you create new branches and make commits, that's all part of your *local* git repository , and merge  local codebase is managFor example, this lecture notes repo 

## Common errors
Have you ever seen an error like this?
```
$ git push
fatal: The current branch test-branch has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin branch-name
```
This means you need to set up your local branch to track . Run the command given (or the equivalent `-u` flag and you should be good to go!

Another common mistake is forgetting to fork before you clone. Please make sure you see your own Github name in the top left corner before you clone!
