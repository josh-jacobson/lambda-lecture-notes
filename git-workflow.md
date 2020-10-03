# Git workflow: tips and tricks

## Review: command line basics, navigating around the filesystem
`cd` ("current directory") helps you move around the file system:
* `cd project-name` navigates into your project folder (you'll do this every time you clone from GitHub)
* `cd ..` moves up a directory

`ls` ("list") lists files in the current directory. 

## A typical workflow
* Fork to your own repo (remember to do this before you clone!)
* On the GitHub page for your forked repo (you should see your own username up top), copy the git url from the code button
* `git clone {url}`
* cd into new directory
* Create a new local branch: `git checkout -b feature-branch-name`
* !CODE! ☕️
* Add your new changes: `git add .`
* Commit your changes: `git commit -m 'Add my exciting new feature...'`
* Everything so far is just on your computer, in your own local git repo. Now, if you're sure your code is ready to share, push to GitHub:
   * `git push -u origin feature-branch-name` 
   * The `-u` flag sets the upstream branch so you can just say `git push` and `git pull` in the future
* !CODE SOME MORE!
* Add your new changes: `git add .` 
    * Pro tip: use `git add -p` to review your changes before pushing. 
    * Alternatively, use `git show` (show last commit) or `git diff master` (show all the changes you've made on your branch, relative to the master branch -- this is what GitHub does when it shows you a preview of the changes in a pull request)
    * Either way, be sure to review your own code before sharing! When collaborating on a team, thoughtful review is a better strategy than "huck and pray"
* Commit your new changes: `git commit -m 'Update stuff and fix bugs'`
* Push to GitHub: `git push` (this works now without specifiying where you're pushing, because you already set the upstream branch above!)

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


## A helpful shortcut: `head`


## Naming commits
Make sure your commit messages are clear and concise, so anyone viewing the list of commits can get a bird's eye view of recent dev work. "First commit on the new feature", "wip trying to get this working" and "fix the bug" are all examples of vague, unhelpful commits that no one wants to see in the history!

Every team has their own preferences, and some even have specific requirements for verb tense ("Add booking feature" vs "Added booking feature") and other phrasing specifics, or including other relevant info like the id for the feature/bug story on your team's project tracker. 

Though the phrasing of your commit messages will probably never be the most important thing, it's a subtle code style cue that, along with other thoughtful approaches to the way you lay out your code and communicate with your team, will make everyone love working with you! 

## Collaborating on GitHub and keeping your branch up to date

The first time you push a new branch, be sure to include the `-u` flag (or `--set-upstream`) to make sure git knows that you'd like to map your local branch to a branch of the same name on GitHub. Git is set up for a range of use cases (and existed long before GitHub), so it doesn't assume this intuitive 1:1 mapping by default. But once you've run this command just once, you should be able to `git pull` and `git push` without the extra typing in the future.

## Pushing your branch to GitHub
``` 
git push origin head
```

## Amdending commits
Did you save a "wip" commit before calling it a night? If you're `git commit --amend`

Note that this is a more advanced approach and may require some knowledge of vim, unless you've setup VSCode as your default editor from your shell.

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
