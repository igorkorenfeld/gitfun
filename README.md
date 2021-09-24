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
