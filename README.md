# README

This readme contains instructions for playing around with git and modifying our shared file. Commands are written with backticks (\`). Placeholder text will be written surronded by "{}"

## Cloning
1. On the upper right hand side of the repo, click the green `Code` button and copy the url

2. On your terminal navigate to where you want this directory to live and type `git clone https://github.com/igorkorenfeld/gitfun.git` (paste in the url)

## Staging and committing
1. Navigate to where git cloned the `gitfun` folder
1. Open up the `colors.md` file
2. On line 5 of the `color.md` file add in some text with your name and favorite color
4. In your terminal type `git status`, this will show you which files have been modified
3. In your terminal type `git add .` and hit enter. This will add all of the modified files, in this case just `colors.md`, to the "Staging" area. These are files that  are now ready to be "committed".
4. In your terminal type `git status`, this will show you which files are ready to be committed.
4. In your terminal type `git commit -m "{message}"` replacing `{message}` with a description of the changes you've made since the last commit. Messages are typically short and written in the present tense, for example `git commit -m "Add Austin's favorite color"`. Once you hit enter, you have added a commit, which is like a snapshot or savepoint of this file. It is now a part of this project' history and we can always come back to this savepoint.
4. In your terminal type `git status`, which will show  you how many commits ahead or behind your local files are, compared with the source branch on GitHub (also known as remote). Note that is comparing to the status on GitHub since the last time you "pulled" from it, in this case since you cloned the repo.
5. In your terminal type `git push`. This will send your commits (i.e. anything you modified and then committed) to the remote repository on GitHub.

## Pulling
When you are working on a project with other team members, you'll want to periodically make sure your local version of the project is up to date, and sync it with what's on remote (on GitHub).

1. In order to do that you type in `git pull` on your terminal. which will pull the most up-to-date version from GitHub.
2. Note there is now next text on line 3

### A little more detail
`git pull` is a sort of shorthand for two different commands: `git fetch` and `git merge`. The first, `git fetch`, retrieves the version from GitHb, and `git merge` automatically figures out how to combine your current local version with those updates. Sometimes though, it can't figure out how to automatically combine the versions, which is what the next section dives into.


## Merge conflicts
Sometimes git cannot figure out how to automatically combine your local version and the changes made in another collaborator's version. In those cases it will ask you to resolve those conflicts yourself. Let's try and simulate that.

1. When you are ready to try this out, send me a message, so that I can set it up. We basically need to intentionally mis-time the updates.
2. Once you hear back from that it's ready, change the color in line 9 from "{magenta}" to something else.
3. Stage your changes with `git add .`
4. Commit your changes with `git commit -m "{message}"`
5. Try to push up your changes with `git push`
6. This time you should get an error message though!

> CONFLICT (content): Merge conflict in colors.md
Automatic merge failed; fix conflicts and then commit the result.

What's happened is that I made a change to the same text that you tried to change, and pushed that up to the server. You don't have my change locally yet (we intentionally didn't pull so we could get here), and git doesn't know how to resolve it. It doesn't know which change it should pick. Instead it needs you to resolve the conflict. Let's do that
7. Look back in your `colors.md` file. You should see a line that says
> <<<<<<< HEAD

Then whatever you changed that line to
then
> =======
> The best color is aquamarine <br>
> \>>>>>>> {string of letters and numbers}

This is showing your version (the stuff below `<<<<HEAD`), compared with the other collaborator's verison (what's on GitHub, the stuff below `======`)

It's up to you to pick what should actually be committed now — what the file show look like. To do that you can keep the text you want, and delete anything you don't (including `<<<< Head`, `====`, and `>>>>ab124`). In Atom I believe there is even a button that let's you pick "ours" or "theirs", which will keep one of the two versions and delete the other stuff.

After modifying the conflicted area to whatever it should be, you'll need to add the files again, and commit them.

You the conflict should now be resolved, and you can `git push` the resolved changes to GitHub

## Branching
So far we've been pushing each collaborator's change directly into the `main` branch. But as we saw this can create conflicts. To avoid running into merge conflicts all of the time, and separate out new features we are working on, we can using branching. Setting up a new branch let's us focus on a particular feature, or try out a new thing, and save changes to it, without affecting the `main` branch. When we are ready to incorporate that thing into our main branch, we can merge it back in. So let's try it out now. Let's add a new section of your choosing to the `colors.md` document.

1. In your terminal type `git checkout -b {branchname}` where `{branchname}` is some a descriptive name for your branch. What this command does is creates a new branch, with whatever name you chose, and switches over to that branch
2. In your terminal type `git branch` this will now show you all of the branches that currently exist and you can switch to. the "*" indicates the branch you are on.
3. Add a new section to the `colors.md` file
4. In the terminal stage and commit your changes (see above for instructions if you need a reminder on how to do this).
5. In your terminal type `git push -u origin {branchname}`. This will push your branch to the remote repo (on GitHub), so that other collaborators can see it, and so that you can create a `pull request` (more on that later). Note that this is different from the push we did before. This time we are pushing up a new branch, rather than pushing our changes to the `main` branch on the remote server.
5. In your terminal type `git checkout main`. This will switch you back to the `main` branch. Notice that your changes are no longer in `colors.md`? But don't worry, you can get back to them with `git checkout {branchname}`. This is to emphasize that you can switch back between different branches, working on different parts in different times, and discarding changes when you no longer want them.


## Pull Requests (PRs)
At this point we've worked on a new branch and made some changes, and now we are ready to incorporate those changes into the main branch. When working with other collaborators, the way we do this is creating a `Pull Request`, often abbreviated as "PR". This means we are asking someone to review our changes, and if everything looks good, to `pull` our changes into the the `main` branch, so they the changes get merged in. This is similar to how we pulled things locally earlier, but now we are asking for a pull to take place on the remote repository. It's also a better practice than pushing changes directly to the `main` branch when working with other collaborators (and you might not always have permissions to do that). Let's try it now:
1. Head over to our [repo on GitHub](https://github.com/igorkorenfeld/gitfun)
2.
 - If you just pushed up your branch recently you may see a yellow banner at the top of the your page that has your branch name and a green button that says "Compare & pull request". Click on that button

 - If it's been a little while since you pushed up your branch the banner might not be there. In which case click on the "Pull requests" link on in the repository's subnavigation menu (the 3rd link). This will bring you to a page that says "Compare changes". <br><br> This section is comparing the base branch, the one you want to merge into, with the changes in the branch you are trying to merge back in. So in our case `base:` should be `main` (as it is by default). And we want to change the `compare:` so that it is `{branchname}`, using the dropdown button. Then click on "Create pull request" on the right-hand side.


3. Give your pull request a title, and in the "Write" section, write a brief description of the changes your pull request is making. This would be a place to note any other thoughts you have, if this PR is fixing a particular issue, and any other information you feel might be useful.

4. On the right hand side of the page, under "Reviewers", tag me as a reviewer so that I can take a look at your pull request.

5. Click the "Create pull request" button on the bottom right.

At this point I'll take a look at your PR, review it, and merge it in to `main`
