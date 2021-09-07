# README

This readme contains instructions for playing around with git and modifying our shared file. Commands are written with backticks (\`). Placeholder text will be written surronded by "{}"

## Cloning
1. On the upper right hand side of the repo, click the green `Code` button and copy the url

2. On your terminal navigate to where you want this directory to live and type `git clone https://github.com/igorkorenfeld/gitfun.git` (paste in the url)

## Staging and committing
1. Open up the `colors.md` file
2. On line 5 of the `color.md` file add in some text with your name and favorite color
4. In your terminal type `git status`, this will show you which files have been modified
3. In your terminal type `git add .` and hit enter. This will add all of the modified files, in this case just `colors.md` to the "Staging" area. That means they are ready to be committed.
4. In your terminal type `git status`, this will show you which files are ready to be committed.
4. In your terminal type `git commit -m "{message}"` replacing `{message}` with some descriptive message of the changes you made and are saving. Messages are typically short and written in the present tense, for example `git commit -m "Add Austin's favorite color"`. Once you hit enter, you have added a commit, which is like a snapshot or savepoint of this file. It is now a part of this projects history and we can always come back to the his point
4. In your terminal type `git status`, which will show where you are compared to the source (also known as remote) branch on GitHub.
5. In your terminal type `git push`. This will send your commits (i.e. anything you modified and then committed) to the remote repository on GitHub.
