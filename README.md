# Practical Git and Github : From Basics to Pro Workflows

### Topics

- Git basics
- Git branches
- Understanding git
- Git merge conflicts
- Github

## What is Git?

- version control
- manage code history
  - Creates snapshots (commits) you can revisit
- track changes to your code over time
- helps teams work together without conflicts

## Before you start

- Text editor: VS Code
- Git installed on your machine (if not)

## 📦 Git Installation and Configuration Essentials

When you install Git for the first time, it's important to configure your **username** and **email address**. These settings are attached to every commit you make and help identify the author of the code changes.

**Essential Git Config Commands**

Run these in your terminal or Git Bash:

```sh
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

- `--global`: Applies the settings to all Git projects on your system.
- there is aso a `--local` option that applies the settings to the current project only which we will cover later
- To set a different name/email for a specific project, remove `--global` and run the command inside that project folder.

**Why This Is Important**

- Commit Attribution: Each commit is tagged with your name and email.
- Collaboration: Platforms like GitHub use this information to track contributions.
- Verification: GitHub can verify commits based on your email.

To view your current global settings:

```sh
git config --global --list
```

To view all settings and their origin:

```sh
git config --list --show-origin
```

## 🚀 Common Git Commands (Quick Reference)

`git init`

Initializes a new Git repository in your current directory.  
Creates a hidden `.git/` folder to start tracking changes,and that's how you know it's a git repo.

`cd .git` and `ls` - will show you the contents of the .git directory. This is where git stores all the information about the repo, or `find .git`.

`git status`

-will show you the current state of your working directory and staging area, including what's staged, what's modified, and what's untracked.

`git add`

Adds files to the staging area (prepares them for commit).

- Add one file: `git add fileName.txt`
- Add all files: `git add .` or `git add -A` (subtle differences exist between these, will explain later)

later

`git commit -m "your message"`

Saves your staged changes to the repository with a message describing the update.
Best practices for commit messages:

- ✅ Use the imperative mood (like a command)
- ✅ Use the present tense
- ✅ This commit will "do this"

Examples:

```sh
git commit -m "add login validation"
git commit -m "create navbar layout"
```

````sh

- ❌ Avoid vague messages:

```sh
git commit -m "stuff"
git commit -m "update"
````

💡 Remember, commit messages are like a diary for your code. They help you and others understand the history of changes and they publicly visible on platforms like GitHub 😀

`git status`

Shows the current state of your working directory and staging area.

- What's staged
- What's modified
- What's untracked

`git log`

Shows the commit history (latest first).

- Includes commit hash, author, date, and message
- Hash: The hash is a unique identifier for each commit, allowing you to reference or revert to specific changes.
- Press `q` to exit the log view

`git log --oneline`

Shows the commit history in a simplified, one-line-per-commit format.

💡 Tracking

- before we add file to the staging area, it's in the "untracked" state
- after we add it to the staging area, it's in the "staged" state
- after we commit it, it's in the "tracked" state
- after we modify it, it's in the "modified" state

It will become important once you want to reset or revert changes.
If you delete the file while it's still untracked, it will be lost forever.

## First Git Project

For all of the "terminal command enthusiasts," I think you will find this useful 👇👇👇 😀😀😀

`echo "file-02.md" > file-02.md` - will create a new file called file-02.md and write the text "file-02.md" into it. The > operator is used to redirect the output of the echo command into the file. If the file already exists, this command will overwrite its contents. If you want to append to the file instead of overwriting it, you can use the >> operator.

**Practice Exercise**

- create a new folder `git-tutorial`
- open the folder in VSCode
- open the terminal in VSCode "View > Terminal" or "Ctrl + `"
- run `ls -la` to see hidden files (like `.git`)
- since this is a new folder, you won't see any hidden files
- run `git status` to see the current state of your project
- since this is not a Git repository yet, you will see an error message
- run `git init` to initialize a new Git repository
- run `git status` again to see the current state of your project
- create file `main-01.txt` and add some text to it
- run `git status` again to see the current state of your project
- run `git add main-01.txt` to stage the file
- run `git status` again to see the current state of your project
- run `git commit -m "add main-01.txt"` to commit the staged file
- run `git status` again to see the current state of your project
- run `git log` to see the commit history
- create files `main-02.txt` and `main-03.txt` and add some text to it
- run `git add .` to stage all files
- run `git status` again to see the current state of your project
- run `git commit -m "add main-02.txt and main-03.txt"` to commit the staged files
- run `git log --online` to see the commit history
- repeat the process one more time to add a new file `main-04.txt` and commit it
- run `git log --oneline` to see the commit history

## Modify a File

- open `main-04.txt` and change the text
- create a new folder `colors`
- create a new file `red.txt` inside the `colors` folder
- add some text to `red.txt`
- run `git status` to see the current state of your project
- run `git add .` to stage all files
- run `git status` again to see the current state of your project
- run `git commit -m "add red.txt and modify main-04.txt"` to commit the staged files
- run `git log --oneline` to see the commit history

## VSCode Git Integration

- create a new folder `vscode-gui`
- open the folder in VSCode
- repeat the steps but with VSCode GUI

## Navigating Commits with Hashes

- Run `git log --oneline` to see all commits.

- Copy the hash you want.
- Run `git checkout <hash>` to go there.
- You've time-traveled to that snapshot 😀
- Run `git log --oneline` to see fewer commits.
- Don't change files (detached HEAD).
- Will cover 'detached HEAD' later.
- Run `git checkout main` (or `master`) to return.
- Will discuss branches next.
- repeat steps with `VSCode GUI`

#### Alternative commands to git checkout

- git log --oneline (important to keep the hashes)
- git reset --hard HEAD~1
- to return back, git reset --hard [hash]

## ⚠️ Git Command Nuances and Repository Safety

**`git add .` vs `git add -A`**

- `git add .` adds all changes in the current directory and its subdirectories.
- `git add -A` adds all changes in the entire repository, regardless of your current directory.

**Demo:**

- create a new folder `big-project`
- create two folders `front-end` and `server`
- create `index.html` and `main.css` inside the `front-end` folder (add some code to them)
- in the `server` folder, create `app.js` and add console.log("Hello from server") to it
- run `git init` to initialize a new Git repository
- navigate to server folder and run `node app.js` to see the output
- run `git add .` to stage all files
- notice that `git add .` only stages the files in the current directory and its subdirectories
- notice that `git add -A` stages all files in the entire repository
- notice that VSCode GUI allows you to stage all files in the entire repository

### Protecting Your .git Directory

⚠️ The `.git` directory contains Git's internal database and configuration files. You should **never**:

- create subdirectories inside the `.git` directory
- manually modify the contents of the `.git` directory
- initialize a Git repository inside another repository's `.git` directory

**Why this is dangerous:**

- it can corrupt your Git repository
- it may cause Git commands to fail or behave unpredictably
- it can lead to loss of commit history
- it breaks Git's internal structure and references

**⚠️ BAD EXAMPLES — NEVER DO THIS IN REAL PROJECTS! ⚠️**
**⚠️ DEMO PURPOSES ONLY ⚠️**

- navigate to `front-end` folder and run `git init` to initialize a new Git repository inside an existing repository
- run `cd .git` followed by `git init` to initialize a new Git repository inside the `.git` directory

Next, we'll cover branches, merging, and rebasing. For now, we'll stick to the "happy path" — a smooth workflow without errors or conflicts. Don't worry, we'll dive into handling those issues later.

## 🧠 Git Challenge: First Project

- Create a new folder called `my-git-project`
- Open the folder in VSCode
- Open the terminal in VSCode (`View > Terminal` or `Ctrl + ``)
- Look for hidden files (you shouldn't see any at this point)
- Check the current Git status — you'll likely get an error
- Turn this folder into a Git repository
- Check the Git status again — notice the difference
- Create a file `main.txt` and write some content inside
- Check the Git status — see which state the file is in
- Stage the file for commit
- Commit the file with a descriptive message
- Review the commit history in a simplified format
- Modify the content of `main.txt`
- Create a folder named `notes` and a file `notes/todo.txt` with some text
- Stage all current changes
- Commit again with a clear message
- Review the commit history in a simplified format

## Branches

- `git branch` — List all branches.
- `git branch <name>` — Create a new branch.
- `git checkout <name>` — Switch to a branch.
- `git switch <name>` — Switch to a branch (since Git 2.23).
- `git checkout -b <name>` — Create and switch to a new branch.
- `git switch -c <name>` — Create and switch to a new branch (since Git 2.23).

## Example: Working with Branches

- Create a new project `git-branches`
- Initialize Git.
- Create `main-01.txt`.
- Add `main-01.txt` to the staging area and commit.
- Repeat the steps for `main-02.txt`.
- Create a new branch called "feature": `git branch feature`
- Switch to the "feature" branch: `git checkout feature`
- Run `git branch` to see the current branch.
- Create a new file `features/feature-01.txt`.
- Add `features/feature-01.txt` to the staging area and commit.
- Switch back to the "main" branch: `git checkout main`
- Notice that `feature-01.txt` is not present in the "main" branch.
- Each branch can have its own set of files and changes, so switching branches can feel like switching between different versions of your project.

## Practice: Creating and Using a New Branch with a Shortcut

- Open the terminal and run: `git checkout -b bugfix` to create and switch to the `bugfix` branch.
- Create a new file called `bugfix/file-01.txt` and add some text.
- Stage and commit `bugfix/file-01.txt`.
- Switch back to the `main` branch.
- Notice that `file-01.txt` is not present in the `main` branch.
- Each branch can have its own files and changes, so switching branches lets you work on different features or versions independently.

## Merging Branches

Merging combines changes from one branch into another, allowing you to bring together different lines of development. There are two types of merges:

- **Fast-Forward (FF)**: Happens when the target branch has no new commits since the source branch diverged. Git simply moves the target branch pointer forward to the source branch's latest commit, creating a linear history.

- **Three-Way Merge**: Occurs when both branches have new commits. Git creates a new merge commit that combines the changes from both branches, preserving the divergent history.

- The main command is: `git merge <branch-name>`
- To merge the `main` branch into your current branch (e.g., `feature`):  
  `git merge main`
- Since main has no new changes, we are already up to date and the merge will be a fast-forward (no merge commit needed).
- To merge your feature branch back into `main`:
  - Switch to `main`: `git checkout/switch main`
  - Run `git branch` to verify that we are on `main`
  - Run `git merge feature`
- Run `git log --oneline`
- Notice `(HEAD -> main, feature)`

  When both branches point to the same commit, HEAD points to the branch you have checked out (e.g., main), and both branches reference the same spot in the commit history. This happens because no new commits have been made on either branch since they were last synchronized.

- To merge the `main` branch into `bugfix`:
- Switch to `bugfix`: `git checkout/switch bugfix`
- Since we just merged `feature` into `main`, main has new changes, so the branches have diverged, which means it won't be a fast-forward merge.
- Run `git merge main`
- Provide a commit message for the merge commit.
- Run `git log --oneline` to see the commit history.
- Switch back to `main`: `git checkout/switch main`
- Run `git merge bugfix` to merge the `bugfix` branch into `main`.
- Run `git log --oneline` to see the commit history.
- Run `git status` to check the current state of the repository.

**How to Edit the Merge Commit Message:**

**1. In VSCode GUI:**

- The commit message will appear in the Source Control panel at the top.
- Click into the message box, edit the text as you like, and then click the **"Continue"** or **"Commit"** button to finish the merge.

**2. In the Terminal Editor (like Vim or Nano):**

- If Git opens a terminal editor (like Vim), you can edit the message directly in the editor window.

  **For Vim:**
  - Press `i` to enter insert mode.
  - Edit the message as you wish.
  - Press `Esc` to exit insert mode.
  - Type `:wq` and press `Enter` to save and quit.

  **For Nano:**
  - Edit the message as you wish.
  - Press `Ctrl+O` to save, then `Enter`.
  - Press `Ctrl+X` to exit.

## Deleting Branches

To delete a branch, you can use the `git branch -d <branch-name>` command. This will delete the specified branch if it has been fully merged into your current branch. If the branch has not been merged, Git will prevent the deletion to avoid losing unmerged changes.

- To delete the `feature` branch, first switch to the `main` branch: `git checkout main`
- Then run `git branch -d feature` to delete the `feature` branch.
- Repeat the process for the `bugfix` branch.
- Create a new branch called `test`, create a new file `test.txt`, and add some text to it.
- Stage and commit `test.txt`.
- Switch to the `main` branch and run `git branch -d test` to delete the `test` branch.
- Since the `test` branch has unmerged changes, Git will prevent the deletion.
- To force delete the `test` branch, run `git branch -D test`.
- Run `git branch` to see the current branches.

**Why merge into the feature branch first?**  
 Merging `main` into your feature branch lets you update your feature with the latest changes from `main` and resolve any conflicts early. This makes the final merge back into `main` smoother and helps prevent surprises or conflicts later.

## Rebase

Rebase rewrites commit history by moving a branch's commits onto a new base, creating new commits with different hashes. It results in a cleaner, linear history but should be used carefully, especially on shared branches, to avoid conflicts and confusion.

⛔️ Don't use rebase on public branches, as it rewrites commit history and can cause confusion for collaborators. In our case, it's the main branch, so we won't use rebase here, since we would not do that in production.

Repeat the steps above but with rebasing instead of merging.

- so in both cases, when we merge `main` into `feature` and `bugfix`, we will use rebase instead of merge.
- create new project `git-rebase`
- initialize Git repository: `git init`
- rest of the steps are the same as above
- compare VSCode GUI for `git-branches` and `git-rebase`
- notice that the commit history (hashes) is different

While working on personal projects, the choice is entirely up to you; however, for work projects, team standards are typically followed. For example, in my case, we are required to use rebase, so it's important to understand both merging and rebasing.

## Using VSCode's Git Interface

Repeat the steps above using the VSCode GUI. You can use the Source Control panel to create branches and merge changes without needing to type commands in the terminal.

💡 When you use the merge option in the VSCode Source Control GUI, it often auto-generates and auto-commits the default merge message for you, so you don't have to manually confirm or edit it. This makes the process faster and more user-friendly.

## 🧠 Git Challenge: Branching & Merging

- Create a new folder called `my-branch-project`
- Open the folder in VSCode
- Open the terminal in VSCode (`View > Terminal` or `Ctrl + ``)
- Initialize a Git repository
- Create a file `main-01.txt`, add some text, stage, and commit it
- Create another file `main-02.txt`, add content, stage, and commit again
- Create two branches `feature` and `bugfix`
- Switch to `main` and create another file `main-02.txt`, add content, stage, and commit again
- Switch to `feature` branch
- In the `feature` branch, create a file `features/feature-01.txt`, add content, stage, and commit
- Switch back to the `main` branch — notice the `feature-01.txt` file is not there
- Switch back to `feature`
- Merge the `main` branch into `feature`
- Merge the `feature` branch into `main`
- Review the commit history in a simplified format
- Switch to `bugfix` branch
- In the `bugfix` branch, create a file `server/bugfix-01.txt`, add content, stage, and commit
- Repeat the same steps for `server/bugfix-02.txt`
- Rebase `bugfix` onto main
- Merge `bugfix` back into `main`
- Check the commit history again
- Try deleting the `feature` and `bugfix` branches from the `main` branch
- Create a new branch `test`, add a file `test.txt`, and commit it
- Switch to `main` and try to delete the `test` branch — you should see a warning
- Force-delete the `test` branch

## Git Config

Global Git configuration is useful because it sets up your default identity (name and email) for all Git projects on your computer, allowing you to configure these settings once and have them apply everywhere. This is perfect for personal settings that should remain consistent across all your projects. On the other hand, local Git configuration is valuable because it lets you override global settings for specific projects, giving you the flexibility to use different settings (like different email addresses) for different projects. Local settings take priority over global ones, making it ideal for project-specific configurations that shouldn't apply to other repositories.

The local config file is located in the `.git/config` directory of your repository. This file contains settings that are specific to that repository and override the global settings.
You can view the local config file by running `git config --local --list` or by opening the `.git/config` file in a text editor.
It works the same for the global

- `git config --local --add user.name "Your Name"` - Adds a new user.name setting to the local repository configuration, allowing multiple values for the same setting. Remove the `--add` flag to overrider previous value.

- `git config --local --unset user.name` - Removes the user.name setting from the local repository configuration.

- `git config --global --unset-all user.name` - Removes all user.name settings from the global Git configuration.

In Git, you can customize the default branch name used when initializing a new repository by setting the init.defaultBranch configuration. While main is the current standard and master was the legacy default, you can choose any name you like — even something fun like shakeAndBake. To set this globally, run git config `--global init.defaultBranch shakeAndBake`, and Git will use that as the initial branch name in all newly created repositories. This flexibility is especially useful for aligning with team conventions or personal preferences.

## .gitignore

`.gitignore` is a special file in Git that specifies which files and directories should be ignored by Git. When you list files or patterns in .gitignore, Git will not track changes to those files, even if they exist in your working directory. This is particularly useful for excluding temporary files, build outputs, environment-specific configurations, and sensitive information from being committed to your repository.

**Practice Exercise**

- Create a new project directory
- Initialize a new Git repository (`git init`)
- Create a file named `main-01.txt`
- Stage and commit the file (`git add main-01.txt` && `git commit -m "initial commit"`)
- Create a `.gitignore` file
- Add `.env` to the `.gitignore` file
- Create a `.env` file in your project, add some sensitive information (e.g., SECRET_KEY="mysecret")
- Notice that Git doesn't track the `.env` file (verify with `git status`)

## Git Stash

- `git stash` - Temporarily saves your uncommitted changes (both staged and unstaged) and reverts your working directory to the last commit. This command only works for tracked files and requires at least one commit in the repository.
- `git stash list` - Shows all stashed changes with their unique identifiers (stash@{0}, stash@{1}, etc.)
- `git stash pop` - Applies the most recent stash and removes it from the stash list
- `git stash apply` - Applies the most recent stash while keeping it in the stash list
- `git stash push -m "message"` - Creates a new stash with a descriptive message to help identify its contents
- `git stash pop stash@{n}` - Applies the specified stash and removes it from the stash list

  `git stash` is a command that temporarily saves your uncommitted changes in a "stash" so you can work on something else without losing your progress. It's useful when you need to switch branches or pull changes from a remote repository but don't want to commit your current work yet.
  When you run `git stash`, Git takes your uncommitted changes (both staged and unstaged) and saves them in a special stash area. This allows you to revert your working directory to the last commit, making it clean and ready for other tasks.
  You can later apply the stashed changes back to your working directory using `git stash apply` or `git stash pop`. The difference is that `git stash pop` removes the stash after applying it, while `git stash apply` keeps the stash for future use.
  You can also view your stashes with `git stash list`, which shows a list of all stashed changes. Each stash is identified by a unique name, like `stash@{0}`, `stash@{1}`, etc. You can apply or drop specific stashes using their names.

**Practice Exercise**

- create a new folder named "git-stash"
- create a file name "main-01.txt" and add some content. commit changes to main branch.
- create "main-02.txt" and "main-03.txt". Don't commit. Try to stash them. You can't stash them as they are still untracked and still no modification made.
- commit the changes.
- now modify content of main-02.txt and main-03.txt. don't commit these modified changes. stash the changes instead.
- create main-04.txt and commit.
- run `git stash pop` to get the saved uncommited changes back.
- again stash the uncommited changes.
- modify content of main-04.txt. stash this changes. now we have two stashes. run `git stash list` to see them.
- run `git stash pop <stash_id>` to get one saved stash back. next get the othe stashed changes back.
- finally commit all changes.

**Practical example of stash**

- create a new branch 'feature'
- create 'feature/feature-01.txt' in the previous project directory. commit changes.
- add/modify content of 'feature-01.txt'.
- suppose, now we want to look at our `main` branch but don't want to commit the last changes in the `feature` branch. try to switch to `main` branch. notice that you can't switch normally and you are asked to stash or commit changes. In this situation it is very helpful to stash the changes. So, run `git stash`. now you can switch to other branch.
- finally come back to the feature branch. run `git stash pop` to get back the changes and commit changes.
- merge feature with main.

## HEAD and Detached HEAD

**HEAD**

HEAD in Git is a special pointer that represents your current position in the repository's history. It typically points to the tip of the current branch you're working on, indicating which commit you're currently viewing or working with. When you make new commits, HEAD moves forward with your branch, keeping track of your latest work. Think of it as your current "view" of the repository.

**detached HEAD**

A detached HEAD occurs when HEAD points directly to a commit instead of a branch. This happens when you check out a specific commit, tag, or remote branch. In this state, any new commits you make won't be associated with any branch, creating what's called "orphaned" commits. While you can still make changes and commit them in a detached HEAD state, these commits can be lost if you switch branches without creating a new branch to save them.

**Working with Detached HEAD**

When you checkout a specific commit using `git checkout <commit-hash>`, you enter a detached HEAD state where your HEAD points directly to a commit instead of a branch. In this state, any changes you make and commit create new commits that aren't associated with any branch. These commits become "orphaned" and may be lost when you switch branches (they'll eventually be removed during Git's garbage collection).
To preserve work done in a detached HEAD state, you have several options:

- Create a new branch from the detached HEAD state using `git checkout -b <new-branch-name>`. This will save your changes and allow you to continue working on them.
- If you already switch to another branch, you can use `git checkout -b <new-branch-name> commitHash` to create a new branch from the commit you were working on.

You can avoid entering a detached HEAD state by always checking out branches instead of specific commits. `git checkout -b branch-name commitHash` creates a new branch from the specified commit, allowing you to work on it without detaching HEAD. This way, you can make changes and commit them to the new branch, keeping your work organized and preventing orphaned commits.

💡 If you need to view a specific commit, consider using `git log` or `git show <commit-hash>` (exit with q) instead of checking it out directly. This way, you can explore the commit history without affecting your current branch or creating orphaned commits.

## Using `git reflog`

`git reflog` is a command that allows you to view the reference log of your Git repository. The reference log is a record of all the changes made to the HEAD pointer, including commits, checkouts, merges, and other operations. It provides a way to recover lost commits or branches by showing you the history of where HEAD has pointed in the past.
`git reflog` is particularly useful when you accidentally delete a branch or commit, or when you want to find the commit hash of a previous state in your repository. The reflog is stored in the `.git/logs` directory and is automatically updated by Git whenever you make a change to the repository.`

The key differences between `git reflog` and `git log` are:

1. `git log` shows your formal commit history, displaying the commit hash and message for each commit in your current branch's history.

2. `git reflog` shows a complete history of all HEAD movements, including:
   - Commits
   - Checkouts
   - Merges
   - Resets
   - Rebases
   - Branch deletions
   - Any other operations that change where HEAD points

Think of `git log` as your official commit history, while `git reflog` is like a detailed activity log that records every movement of HEAD, making it particularly useful for recovering lost commits or branches after operations like hard resets or branch deletions.

#### practice HEAD

- create a project folder 'head-reflog'
- create main-01.txt. put content and commit changes.
- run `git log --oneline` to see the `HEAD` position. It is pointing to the main branch's latest commit.
- repeat step for 'main-02.txt'.
- create and switch to a new branch 'feature'.
- create feature/feature-01.txt. put content and commit changes.
- repeat step for feature-02.txt.
- run `git log --oneline` to see the `HEAD` position. It is now pointing to the `feature` branch's latest commit.
- switch to the main branch and repeat steps for 'main-03.txt'.
- switch to feature branch and merge `feature` with `main`.
- check the HEAD position (pointing to feature branch with the merge-commit).
- switch to main branch and merge `main` with `feature`.
- again check the HEAD position. now the HEAD should be pointing to both main and feature branch on the latest commit.

#### practice detached HEAD

- continue with the previous project.
- checkout to an old commit (run `git checkout <commit_hash>`). now we are in detached HEAD mode. now if we change anything to the project it won't be associated with any branch.
- Solution: instead of running `git checkout <commit_hash>`, run `git checkout -b <branch_name> <commit_hash>`. This will not only move to the specific commit, associate new changes (if any) to that new branch (not detached).
- for example, checkout to an old commit with a new branch named 'bugfix'.
- create 'bugfix/bugfix-01.txt' and commit changes. this will associated with branch 'bugfix'.
- finally merge main and bugfix branches.

**practice reflog**

- continue with the previous project.
- while in the main branch, run `git reflog`.
- This will show all the HEAD movements history with hashe ids.
- In the 'Git Reset' section we'll practice some practical scenarios.

## Git Reset

Git reset is a powerful command that allows you to undo changes in your Git repository. It can be used to unstage files, discard changes, or even remove commits from your history.We will only cover the most common use cases of `git reset` here, since I don't want to overwhelm you with too much information at once. The most common use cases are:

- `git reset --soft HEAD~1` - undo the last commit but keep the changes staged
- `git reset --hard HEAD~1` - undo the last commit and discard all changes
- `git reset --hard commitHash` - undo all changes and reset to a specific commit
- `git reset` - Unstages changes by moving them from the staging area back to the working directory.

💡 In this case, HEAD~1 refers to the commit history from git log, not the reference log from git reflog.

**Soft Reset**

The `git reset --soft HEAD~1` command is used to undo the last commit while keeping all the changes staged. The `--soft` flag means that Git will move the HEAD pointer back one commit (`HEAD~1`), but it will keep all the changes from that commit in the staging area. This is useful when you want to:

- Modify the commit message
- Add more files to the commit
- Split a commit into multiple smaller commits
- Combine the changes with other staged changes before making a new commit

If you use `HEAD~2` instead of `HEAD~1`, Git will move back two commits and keep all changes from both commits in the staging area. This allows you to combine the last two commits into one or modify them together. Unlike a hard reset, a soft reset is safe as it preserves all your changes in the staging area, allowing you to make a new commit with the same changes.

## Hard Reset

The `git reset --hard HEAD~1` command is a powerful and potentially dangerous command that completely removes the last commit and all its changes. The `--hard` flag tells Git to:

1. Move the HEAD pointer back one commit (`HEAD~1`)
2. Reset the staging area to match the previous commit
3. Reset the working directory to match the previous commit

If you use `HEAD~2` instead of `HEAD~1`, Git will move back two commits and permanently remove both the last commit and the one before it, along with all their changes. This means all changes from the last two commits will be permanently lost. Use this command with extreme caution, as there's no way to recover the changes once they're discarded. It's recommended to create a backup branch or stash your changes before using a hard reset if you're unsure about the consequences.

#### practice reset

- crate a project folder 'reset'
- create 'main-01.txt'. commit changes. repeat steps for 'main-02.txt' and 'main-03.txt'.
- run `git log --oneline` to see the commit hashes.
- run `git reset --soft <commit_hash>` to reset the project back to that specific commit. the soft reset will keep changes after that commit to the staged area.
- make some changes to the staged files and make a new commit. Now we have two commits.
- run `git reset --hard HEAD~1` to reset the project back to the old commit again. This time all changes after the commit will be lost.
- if we want to come back to the latest commit (and can't see the commit hash), we need to run `git reflog`. This will show all the HEAD movements history with the commit hashes. Now we can run `git reset --hard <commit_hash>` to restore back to the latest commit.

## Undoing Staged Changes

To unstage changes that have been added to the staging area, you have several options. The most common way is to use `git reset filename` to unstage a specific file, or `git reset .` to unstage all files. Alternatively, you can use the newer `git restore --staged filename` command to unstage a specific file, or `git restore --staged .` to unstage all files. Both methods will move the changes from the staging area back to the working directory. If you want to completely discard the staged changes, first unstage them using one of the above commands, then use either `git checkout -- filename` or `git restore filename` to discard changes in a specific file, or `git checkout .` or `git restore .` to discard all changes in the working directory.

## Reverting Unstaged Changes

To discard changes in your working directory, you can use `git checkout`. Running `git checkout .` will revert all unstaged changes in the current directory and its subdirectories. To revert changes in a specific file, use `git checkout -- filename`. This command will restore the file to its state in the last commit, effectively discarding any unstaged changes you've made to that file.

Alternatively, you can use the newer `git restore` command, which was introduced in Git 2.23 as a more intuitive alternative to `git checkout`. To discard all unstaged changes, use `git restore .`, and to discard changes in a specific file, use `git restore filename`. The `git restore` command is considered more explicit in its purpose and is the recommended way to revert changes in newer versions of Git.

## Cleaning Untracked Files

To remove untracked files from your working directory, you can use `git clean`. The `git clean -dn` command shows a dry-run of what files would be removed without actually deleting them, which is useful for safety checks. To actually remove the untracked files, use `git clean -df`. The `-d` flag includes directories, and the `-f` flag forces the removal. Be cautious with these commands as they permanently delete files that aren't tracked by Git, and the changes cannot be undone.

## Deleting Unmerged Branches

When you delete a branch that has unmerged commits (commits that exist only in that branch and haven't been merged into another branch), Git will warn you and prevent the deletion by default. This is a safety feature to prevent accidental loss of work. To force delete an unmerged branch, you need to use the `-D` flag instead of `-d` (`git branch -D branch_name`).

However, even after deleting the branch, the commits still exist in Git's object database until they are garbage collected. You can recover a deleted branch if you know its last commit hash. To permanently remove the commits, you would need to use commands like `git gc` or wait for Git's automatic garbage collection to run.

When you delete a branch that has uncommitted changes (either staged or unstaged), Git will allow the deletion, but the changes will remain in your working directory and staging area, now associated with your main/master branch. At this point, you need to decide what to do with these changes:

1. Commit the changes to main/master if they're meant to be there
2. Stash the changes using `git stash` if you want to save them for later
3. Discard the changes using `git reset . ` or `git checkout .` if they're no longer needed, or if the files are untracked follow the steps discussed above

It's generally recommended to:

1. Merge important changes before deleting a branch
2. Create a backup branch if you're unsure about deleting
3. Use `git branch -d` first to see if there are any unmerged changes
4. Only use `-D` when you're absolutely sure you want to delete the unmerged commits
5. Be aware that uncommitted changes will stay in your working directory after branch deletion

## 🧠 Git Challenge: Config, Ignore, Stash & Recovery

- Create a new folder called `my-git-tools`
- Open the folder in VSCode
- Open the terminal in VSCode (`View > Terminal` or `Ctrl + ``)
- Initialize a Git repository
- Set your name and email locally for this specific project
- In three separate commits, create files ,`main-01.txt`,`main-02.txt`,`main-03.txt` add content, stage, and commit it
- Create a `.gitignore` file and add all markdown files that start with `temp` to it
- Create files `.temp-1.md` and `.temp-99.md`, and write some content
- Check the Git status to confirm files are ignored
- Modify `main-01.txt` without committing the change
- Stash the change with a short message
- Check the list of stashes
- Apply the stash and remove it from the stash list
- Confirm that your changes are restored
- View the commit log and copy a random commit hash
- Checkout that commit directly (entering a detached HEAD state)
- Make a change to `main-01.txt` and commit it
- Realize you're not on a branch — create a new branch from this state to save your work
- Switch back to the main branch
- Use reflog to view your recent HEAD movements
- Make two more commits to `main-01.txt`
- Use a soft reset to undo the last commit but keep the changes staged
- Amend the content and recommit with a new message
- Use a hard reset to go back one more commit and fully discard changes
- Confirm that changes are gone
- Stage a new change to `main-01.txt`
- Unstage it using a command of your choice
- Make additional changes and discard them completely (unstaged)
- Create a file `temp.txt` (don't stage or commit it)
- Use a dry-run command to preview what untracked files would be deleted
- Then, permanently remove the untracked file

-`temp*.md`

- `**/node_modules`

## Merge Conflicts

A merge conflict occurs when Git cannot automatically resolve differences between two branches during a merge operation. This typically happens when two branches have made changes to the same line of code or when one branch has deleted a file that another branch has modified. When a merge conflict occurs, Git will pause the merge process and mark the conflicting files, allowing you to manually resolve the conflicts before completing the merge.

**Major Types of Merge Conflicts**

1. **Content Conflict**: Occurs when two branches modify the same line in a file differently, or when one branch modifies a line that the other branch deletes.

2. **File Add/Delete Conflict**: Happens when one branch deletes a file while the other branch modifies it.

3. **File Rename Conflict**: Arises when a file is renamed differently in two branches.

4. **Directory/File Conflict**: Occurs when one branch creates a file and the other branch creates a directory with the same name.

5. **Binary File Conflict**: Happens when two branches modify a binary file differently, and Git cannot automatically merge the changes.

#### practice merge conflicts

- create a new project directory 'merge-conflicts'
- create app.js with content "console.log("App is running on main")"
- create hello.js with content "console.log("hello from main")"
- commit changes with message "create two files app and hello"
- create and switch to a new branch 'payment'.
- edit app.js content as "console.log("App is running on payment")"
- edit hello.js content as:

```js
console.log("hello from main")
console.log("hello from payment")
```

- commit changes with message "create payment"
- switch to main branch and create and switch to a new branch 'feature'
- edit the app.js content as "console.log("App is running on feature-1")"
- edit the hello.js content as:

```js
console.log("hello from main")
console.log("hello from feature-1")
```

- commit with message "create feature-1"
- again edit app.js as "console.log("App is running on feature-2")"
- edit the hello.js content as:

```js
console.log("hello from main")
console.log("hello from feature-1")
console.log("hello from feature-2")
```

- commit changes with message "create feature-2"
- switch to main branch and create and switch to a new branch 'bugfix'
- edit the app.js content as "console.log("App is running on bugfix-1")"
- edit the hello.js content as:

```js
console.log("hello from main")
console.log("hello from bugfix-1")
```

- commit with message "create bugfix-1"
- repeat the steps for bugfix-2, bugfix-3 and bugfix-4
- switch to payment branch and merge with main (and then vice versa). we won't face any conflicts during this merge.
- now switch to feature brance and try to merge with main (use commands instead of gui). you'll face conflicts. resolve the conflicts, stage changes and commit with gui (press `continue` button).
- now switch to main and merge with feature. this time merge will be done with 'Fast-forward' and no conflicts.

- now switch to bugfix branch.
- this time instead of merging, run `git rebase main`.
- the difference is that now we have to accept incoming changes instead of current. the next steps are similar.

## 🔄 Git Rebase vs Git Merge (Behind the Scenes)

**👉 `git rebase main` (from `feature-branch`)**

1. Git finds your unique commits (not in `main`).
2. Temporarily saves them (like a patch).
3. Resets `feature-branch` to `main`, then re-applies your commits one by one.
   - 🚫 Rewrites history (no merge commit).
   - ✅ Cleaner, linear history.

**👉 `git merge main` (from `feature-branch`)**

1. Git finds the common ancestor between `feature-branch` and `main`.
2. Applies `main`'s changes onto `feature-branch`.
3. Creates a new **merge commit** combining both histories.
   - ✅ Preserves original history.
   - 📦 Keeps full branch context.

## Merge Conflicts with Rebase

When you rebase a branch onto another branch, Git tries to apply the commits from the source branch onto the target branch. If there are conflicting changes between the two branches, Git will pause the rebase process and mark the conflicting files. You will need to manually resolve these conflicts before continuing with the rebase.

## Squash Commits Merge and Rebase

- cleaner commit history.
- combine commits into one.

**`git merge --squash feature`** - for combining commits during merge.

**`git rebase -i HEAD~n`** - combine commits during rebase

The `git rebase -i HEAD~n` command allows you to interactively rebase the last n commits. This means you can choose which commits to keep, edit, squash (combine), or drop (remove) during the rebase process. The interactive rebase opens an editor where you can modify the commit history as needed.

## Cherry-Pick

cherry-pick is a Git command that allows you to apply the changes introduced by a specific commit from one branch to another. This is useful when you want to incorporate a particular change without merging the entire branch. Cherry-picking creates a new commit in the target branch with the same changes as the original commit, but it does not affect the commit history of the source branch.
To cherry-pick a commit, you need to know its commit hash. You can find the commit hash by running `git log` or `git log --oneline`. Once you have the hash, switch to the target branch where you want to apply the changes and run `git cherry-pick <commit-hash>`. This will create a new commit in the target branch with the changes from the specified commit.
To cherry-pick multiple commits, you can specify a range of commits using the `..` notation, like `git cherry-pick <start-commit>..<end-commit>`. This will apply all commits in that range to the current branch. If there are conflicts during the cherry-pick process, Git will pause and allow you to resolve them before continuing.

#### practice cherry-pick

- create a new project folder 'cherry-pick'
- create main-01.txt and commit.
- create two new branches 'feature' and 'feature-test'
- switch to feature.
- create 'feature-01.txt' and commit.
- switch to feature-test branch.
- create two commits here.
- now see the git logs for commit hashes in feature-test branch.
- suppose you want to only merge one specific comit of feature-test branch into feature branch. copy that comit hash.
- switch to feature branch and run `git cherry-pick <commit_hash>`. now only that commit will be merged into this feature branch.

## 🧠 Git Challenge: Conflicts, Rebase, Squash & Cherry-Pick

- Create a new folder called `git-merge-rebase-practice`
- Open the folder in VSCode
- Open the terminal in VSCode (`View > Terminal` or `Ctrl + ``)
- Initialize a Git repository
- Create a file `main.txt`, add content, stage, and commit
- Create a new branch `feature`, switch to it
- Modify the same line in `main.txt`, commit the change
- Switch back to `main`, edit the same line differently, and commit
- Switch to `feature` create new file `feature-1.txt` and make a commit
- Try merging `main` into `feature` — resolve the merge conflict manually
- Stage the resolved file and complete the merge
- Try merging `feature` into `main`, squash commits
- Reset the repo to an earlier state (before feature branch) and repeat the scenario using rebase instead
- Create a few more commits with small changes
- During rebase, resolve conflicts and continue the process
- Use interactive rebase to squash multiple commits into one
- Verify the new, clean history
- Create a new branch `cherry-target`
- Switch back to `feature`, create and commit a unique change
- Use `git log` to find the commit hash of this change
- Switch to `cherry-target` and cherry-pick the commit using its hash
- Verify that the changes appear on `cherry-target`
- If conflicts appear, resolve and continue the process

## Github

- largest development platform
- cloud hosting & collaboration provider
- git repository hosting

- `git remote add origin URL` - Adds a remote repository to your local Git repository
- `git push` - Uploads your local commits to the remote repository
- `git fetch` - Downloads changes from remote without merging them
- `git pull` - Downloads and integrates remote changes into your local repository
- `git clone` - Creates a local copy of a remote repository

1. `git remote add origin URL`
   - Adds a remote repository (like GitHub) to your local Git repository
   - you're essentially creating a connection between your local project and a copy of that project hosted on a remote server (like GitHub). Think of it like setting up a two-way street between your computer and the serve
   - `origin` is the default name for the remote repository that serves as an alias for later use
   - The URL is typically the HTTPS or SSH link to your GitHub repository
   - Example: `git remote add origin https://github.com/username/repo.git`

2. `git push`
   - Uploads your local commits to the remote repository
   - Syncs your local changes with the remote repository
   - Common usage: `git push origin main` (pushes to main branch, typically for personal projects)
   - First time push: `git push -u origin main` (sets up tracking)
   - For production projects: `git push origin feature` (pushes to feature branch)
   - For production projects: `git push -u origin feature` (pushes to feature branch)
   - `git push -u origin main` - shorthand for the command below
   - `git push --set-upstream origin main`

3. `git fetch`
   - Downloads changes from the remote repository without merging them
   - Updates your remote-tracking branches
   - Common usage: `git fetch origin` (fetches all branches)
   - For specific branch: `git fetch origin feature` (fetches only feature branch)
   - Safer than pull as it doesn't automatically merge changes

4. `git pull`
   - Downloads and integrates changes from the remote repository
   - Combines `git fetch` and `git merge` in one command
   - Updates your local repository with remote changes
   - Common usage: `git pull origin main` (for main branch)
   - For feature branches: `git pull origin feature` (pulls changes from remote feature branch)

5. `git clone`
   - Creates a copy of a remote repository on your local machine
   - Downloads the entire repository history
   - Sets up remote tracking automatically
   - Example: `git clone https://github.com/username/repo.git`

`git fetch` downloads new changes from the remote repository but doesn't apply them to your work. It's like getting updates but keeping them separate until you're ready to use them. `git pull` does both downloading and applying the changes in one step - it fetches the updates and immediately merges them into your current work. While `git pull` is more convenient, `git fetch` gives you more control as you can review changes before deciding to merge them.

## Create Github Account

## Setup SSH key

- [Setup SSH Key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
- [Check For Existing SSH Key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys)
- [Generate New SSH Key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

- `ls -al ~/.ssh` - Lists all files (including hidden) in the SSH directory
- `ls -la` - Lists all files in current directory with details
- find `.ssh`
- `cd .ssh` - Changes directory to .ssh folder
- `ssh-keygen -t ed25519 -C "yourgithubemail@email.com"` - Generates new SSH key with your email
- `ls -la` -Lists all files in current directory with details
- `pbcopy < ~/.ssh/your_key.pub` - Copies public key to clipboard (macOS)
- add public key to Github (Settings/SSH and GPG Keys)
- `ssh -T git@github.com` - Tests SSH connection to GitHub
- `ssh -T git@github.com -v` - Tests SSH connection with verbose output

This should work. If it doesn't, try the steps below:

- `touch ~/.ssh/config` - Creates SSH config file
- `vim config` - Opens config file in vim editor

```
Host github.com
  AddKeysToAgent yes
  IdentityFile ~/.ssh/your_file
```

- `ssh-add ~/.ssh/your_file` - Adds SSH key to SSH agent
- `ssh-add -l` - Lists all keys in SSH agent
- `git config --global url."git@github.com:".insteadOf "https://github.com/"` - Configures Git to use SSH instead of HTTPS

## First GitHub Repository

- create project locally, make one commit
- create new project on Github
- choose ssh option
- explore commands
- run commands on your machine, push the project up to Github

- `git remote add origin yourValue.git`
- `git branch -M main`
- `git push -u origin main`

- make second commit, push up to Github
- `git push`

## Clone Remote Repository

- clone repo
- make another commit, push up to Github

## Create Github Repo with VSCode

- create another project
- make a commit
- publish a branch from VSCode

## Extra - Publish Site on Netlify

[Netlify](https://www.netlify.com/)

## First PR

A Pull Request (PR) is like a formal request to merge your changes into someone else's project. It's the main way to contribute to open-source projects or collaborate with team members. When you create a PR:

1. You're telling the project maintainers "I've made some changes, please review them"
2. They can review your code, suggest improvements, or approve it
3. If approved, your changes get merged into the main project

Think of it like submitting a draft for review before it gets published in a book. The maintainers can review your work, request changes, or accept it as is.

- create a temporary local project and push it to github. then delete the local one.
- clone the github repo into local machine again.
- create a branch (`TICKET-11`)
- add some changes
- merge main into TICKET-11. (skip merging TICKET-11 into main locally).
- push it up to Github using `git push -u origin TICKET-11`
- go to github repo and press on `Compare & pull request`
- select and click on `draft pull request` for now.
- before making `Ready for review`, make some more changes and push again.
- new commits will be automatically added to the previous pull request.
- press `Ready for review` button and review changes.
- usually select `Merge pull request` or `Squash and merge` and press. Squash combines commit messages.

## Challenge - Second PR with `TICKET-22` Branch

- checkout to a new branch `TICKET-22`
- create file ticket-22.txt with some text
- add "hello people" to main-01.txt
- change text to "hello from ticket-22" in `hello.js`
- make a commit "TICKET-22 make changes"
- create app.js
- add text to "app is running..." in app.js
- make a second commit "TICKET-22 change text in app.js"
- merge `main` into `TICKET-22`
- hmm. strange it's up to date ⚠️ (because local main is not latest like the remote main)
- push the changes up to Github
- see if you can merge `TICKET-22` into `main` ⚠️
- don't force it, keep watching and I will provide solution ⚠️

## How Git Remotes and Remote-Tracking Branches Work

- checkout main branch
- see all branches (including remote) with VSCode GUI
- "sync changes" button and "branch" in the left bottom corner
- `git branch -a` - Lists all branches (both local and remote) in the repository

In Git, a remote is like a link to a version of your project stored on another computer, usually a server like GitHub. It lets your local Git talk to that remote copy, so you can download updates (git fetch, git pull) or send your changes (git push).

To help manage this, Git creates remote-tracking branches like remotes/origin/main. These are local snapshots that show what the remote branch looked like the last time you connected. They're read-only references that help Git keep track of the state of the remote repository, so you can compare, sync, or update your local branches without immediately changing them.

These references get updated in three main ways:

1. **`git fetch`**
   - `git fetch` or `git fetch origin`
   - Contacts the remote.
   - Downloads new commits and branch updates.
   - Updates ALL `remotes/origin/*` branches to reflect the latest state of the remote.
   - Does **not** change your local working files or branches.
   - `git status` - to check status

2. **`git pull`**
   - Performs a `git fetch` followed by a merge (or rebase) ONLY into your current branch.
   - Updates the `remotes/origin/*` references, since we run `git fetch`
   - Also updates your current branch if there are new changes.

3. **`git push`**
   - Sends your local commits to the remote repository.
   - After a successful push, updates the corresponding `remotes/origin/<branch>` in your local repo.
   - Only updates the tracking branch for the branch you pushed.

In summary:

- Use `fetch` or `pull` to get updates **from** the remote.
- Use `push` to send your work **to** the remote.
- Remote-tracking branches only update when one of these commands is run.

**`remotes/origin/HEAD -> origin/main`**
to indicate which remote branch is the default (usually main or master).

## Complete Challenge

- run `git pull` in `main` branch
- switch to `ticket-22` branch
- squash commits, with interactive rebase
- rebase on top of `main`
- try to push to Github

After a rebase, Git rewrites your branch's commit history, creating new commit hashes. Because your local history no longer matches the remote, a regular git push will fail with a "non-fast-forward" error. To update the remote with your rebased changes, you need to use git push -f (force), which tells Git to overwrite the remote branch with your new history. This should be done carefully, especially on shared branches, as it can overwrite others' work.

- `git push -f`

I know my history changed — overwrite the remote branch with my local version anyway.
⚠️ Be careful:
Force-pushing can overwrite others' work if you're not the only one working on the branch.

- leave comments
- merge `TICKET-22` branch back into the `main` branch on Github.

**`git push -u origin branch`**

The `-u` flag in `git push` stands for `--set-upstream` and is used to link your local branch with a remote branch. When you push a new branch for the first time using `git push origin feature-xyz`, Git will push the code but won't remember which remote branch it should track. This means future `git pull` or `git push` commands will require you to specify the remote and branch name again. However, if you use `git push -u origin feature-xyz`, Git not only pushes the branch but also sets it to track `origin/feature-xyz`. This makes future pushes and pulls simpler, as Git now knows which branch to use by default. You only need to use the `-u` flag once when creating and pushing a new branch.

In short it's useful since we need to run only `git pull` or `git push` after.

**Pushing a Local Branch to a Remote with a Different Name**

When you run `git push -u origin payment` but don't have a local branch named `payment`, Git throws an error: `src refspec payment does not match any`. This is because Git assumes you're trying to push a local branch called `payment`, which doesn't exist. If you're on a local branch named `feature` and want to push it to the remote as `payment`, you need to explicitly tell Git by using: `git push -u origin feature:payment`. This pushes your local `feature` branch to a remote branch named `payment` and sets up tracking between them.

## 🧠 Github Challenge

- Create a folder named `temp-github-challenge` and initialize a Git repository.
- Create a file `app.js` with a simple `console.log()` statement.
- Stage and commit the file as the initial commit on the `main` branch.
- Create a new GitHub repository and push the project to `main`.

- Clone the GitHub repository into three separate folders: `dev1`, `dev2`, and `dev3`.

- In the `dev1` folder:
  - Create a branch named `TICKET-11`.
  - Modify `app.js` by changing the console message.
  - Commit the change with a short message.
  - run `git pull` in main to check everything is up to date with remote main.
  - Fetch and merge the latest `main` into `TICKET-11`.
  - Push the branch to GitHub (`git push -u origin TICKET-11`)
  - Create a pull request and merge `TICKET-11` into `main` using the **merge** strategy.

- In the `dev2` folder:
  - Create a branch named `TICKET-22`.
  - Make two separate changes to `app.js`, committing after each change.
  - Fetch and merge the latest `main` into `TICKET-22`.
  - Push the branch to GitHub.
  - Create a pull request and merge `TICKET-22` into `main` using the **merge** strategy.

- In the `dev3` folder:
  - Create a branch named `TICKET-33`.
  - Make three separate changes to `app.js`, committing after each.
  - Use interactive rebase to squash all three commits into one.
  - Fetch the latest `main` and rebase `TICKET-33` on top of it.
  - Force push the rebased branch to GitHub.
  - Create a pull request and merge `TICKET-33` into `main` using the **rebase** strategy.

**🍒 Cherry-Pick Across Branches with Remote Fetch**

- create new project `temp-production`
- add new file `main-01.txt` with some content, make a commit, push it up to Github
- clone two projects `dev1` and `dev2`

- In `dev1` project:
  - Create a branch named `FEATURE`.
  - Create a new file `feature-01.txt` and add some content, commit the change, push it up to Github
  - repeat with files `feature-02.txt` and `feature-03.txt`

- Switch to the `dev2` folder:
  - Create a branch named `CHECKOUT`.
  - Create a file `checkout.txt` and add some content.
  - Commit the change.

- Navigate to the GitHub repo in your browser:
  - Open the `FEATURE` branch and copy the commit hash for the `feature-03.txt` commit.

- Back in `dev2` on the `checkout` branch:
  - Try to cherry-pick the `feature-03.txt` commit using the copied hash.
  - Notice the error (Git can't find the commit because it doesn't exist locally).

- Fix the error by running `git fetch`:
  - This updates the remote-tracking branches (e.g., `origin/FEATURE`) without changing any local branches.

- Retry the cherry-pick:
  - Now it works because the commit is known locally via the updated remote reference.
