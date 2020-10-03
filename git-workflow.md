# Git workflow: tips and tricks
🚀🚀🚀

## Review: command line basics, navigating around the filesystem
`cd` ("current directory") helps you move around the file system:
* `cd project-name` navigates into your project folder (you'll do this every time you clone from GitHub)
* `cd ..` moves up a directory

`ls` ("list") lists files in the current directory. 

## Basic git commands
* Clone a repo from GitHub `git clone {url}`
* Create a new branch: `git checkout -b new-branch-name`
* Switch to an existing branch (commit or stash your changes first): `git checkout branch-name` 
* Show all branches: `git branch`


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
* Add your new changes: `git add .` (or `git add -p` to review changes first)
* Commit your new changes: `git commit -m 'Update stuff and fix bugs'`
* Push to GitHub: `git push` (this works now without specifiying where you're pushing, because you already set the upstream branch above!)

## Pro tip: review your changes before pushing to GitHub
Use `git add -p` to review your changes before pushing. It's a helpful line-by-line interface that will help you catch any `console.log`s, white space errors, and other things you meant to fix before sharing your code with the team.

Alternatively, you can use `git show` to see your last commit and `git diff main` to see all the changes made on your branch (this is what GitHub shows in the UI for the code changes in a pull request). `git log` is also useful to see a list of your commmit messages and make sure there are no "wip"s or other annoyingly vague placeholders in the commit history.

There are many good approaches here, but regardless of the workflow you choose, just make sure Either way, be sure to review your own code before sharing! When collaborating on a team, thoughtful review is a better strategy than "huck and pray"

## Merging in the latest changes from GitHub
When collaborating as part of a team, you'll often want to pull down the latest changes that have been merged into the main branch on GitHub by other developers while you've been working
```
git pull origin main
```

A less common use case: you and other developers are working on the same feature branch, so you want to pull down the latest changes:
```
git pull origin head
```

This updates your local codebase with the latest code from GitHub. Once you're upstream branch is set, you can simply type `git pull`

## Naming commits
Make sure your commit messages are clear and concise, so anyone viewing the list of commits can get a bird's eye view of recent dev work. "First commit on the new feature", "wip trying to get this working" and "fix the bug" are all examples of vague, unhelpful commits that no one wants to see in the history!

Every team has their own preferences, and some even have specific requirements for verb tense ("Add booking feature" vs "Added booking feature") and other phrasing details. Some also like to include an id to reference the feature/bug story on your team's project tracker, either in commits or when you submit a pull request.

Though the phrasing of your commit messages will probably never be the most important thing, it's a subtle cue that, along with other thoughtful approaches to the way you lay out your code and communicate with your team, will make everyone love working with you! 

## Collaborating on GitHub and keeping your branch up to date

The first time you push a new branch, be sure to include the `-u` flag (or `--set-upstream`) to make sure git knows that you'd like to map your local branch to a branch of the same name on GitHub. Git is set up for a range of use cases (and existed long before GitHub), so it doesn't assume this intuitive 1:1 mapping by default. But once you've run this command just once, you should be able to `git pull` and `git push` without the extra typing in the future.


## Amdending commits
Did you save a "wip" commit before calling it a night? Update the commit message (and optionally add more code changes) with `git commit --amend`

Note that this is a more advanced approach and may require some knowledge of vim, unless you've setup VSCode as your default editor from your shell.

## Common errors
Have you ever seen an error like this?
```
$ git push
fatal: The current branch test-branch has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin branch-name
```
This means you need to set up your local branch to track . Run the command given (or the equivalent `-u` flag) and you should be good to go!

Another common mistake is forgetting to fork before you clone. Please make sure you see your own Github name in the top left corner before you clone!

(Note: many older codebases have a default branch called `master`, but it's more common for new apps to call the default branch  `main`. `develop` and other names are also common for bigger production apps where there may be multiple stages between pushing your code and going live to users.)
