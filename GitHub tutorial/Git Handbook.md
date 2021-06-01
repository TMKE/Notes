# Git Handbook

### Version control system

A version control system (VCS) ***tracks the history of changes*** as people and teams collaborate on projects together. As the project evolves, teams can run tests, fix bugs, and contribute new code with the confidence that any version can be recovered at any time.

Developers can review project history to find out:

- Which changes were made?
- Who made the changes?
- When were the changes made?
- Why were changes needed?

### Distributed version control system

DVCSs allow full access to every file, branch, and iteration of a project, and allows every user access to a full and self-contained history of all changes.

Unlike once popular centralized version control systems, DVCSs like Git don’t need a constant connection to a central repository. Developers can ***work anywhere and collaborate asynchronously from any time zone***.

Git and other VCSs give each contributor a unified and consistent view of a project, surfacing work that’s already in progress. Seeing a transparent history of changes, who made them, and how they contribute to the development of a project helps team members stay aligned while working independently.

### Git

- +70% of developers use Git *(according to the latest Stack Overflow developer survey)*.
- Git lets developers see the entire timeline of their ***changes, decisions, and progression*** of any project in one place.
- Developers work in every time zone. Using branches, developers can safely propose changes to production code.
- Git makes it possible to align experts across a business to collaborate on major projects.

### Git repository

A Git repository *(or project)* encompasses the entire collection of files and folders associated with a project, along with each file’s revision history. The file history appears as ***snapshots in time called commits***, and the commits exist as a ***linked-list relationship***, and can be ***organized*** into multiple ***lines of development*** called ***branches***.

Because Git is a DVCS, repositories are self-contained units and anyone who owns a copy of the repository can access the entire codebase and its history. Developers are encouraged to fix bugs, or create fresh features, without fear of derailing mainline development efforts. Git facilitates this through the use of topic branches: lightweight pointers to commits in history that can be easily created and deprecated when no longer needed.

### Basic Git commands

You can think of the HEAD as the "current branch". When you switch branches with git checkout, the HEAD revision changes to point to the tip of the new branch (`cat .git/HEAD` shows what HEAD point to).

To use Git, developers use specific commands to copy, create, change, and combine code. These commands can be executed directly from the command line or by using an application like GitHub Desktop or Git Kraken.

- `git init`: initializes a brand new Git repository and begins tracking an existing directory

    It adds a hidden subfolder within the existing directory that houses the internal data structure required for version control

- `git clone`: creates a local copy of a project that already exists remotely (fetch code from a remote repository)

    The clone includes all the project's files, history, and branches

- `git remote`

    ```bash
    # Add remote repo to local repo config
    git remote add new-remote-repo https://bitbucket.com/user/repo.git

    # pushes the crazy-experiment branch to new-remote-repo
    git push <new-remote-repo> crazy-experiment~
    ```

    [https://www.atlassian.com/git/tutorials/syncing#git-fetch](https://www.atlassian.com/git/tutorials/syncing#git-fetch)

- `git remote -v`: this especially comes into play if you are working with fork. If you forked a repository, then cloned your own fork of that repository locally, you might want to add another remote so you can pull out changes from that upstream parent fork
- `git checkout`

    A "checkout" is the act of switching between different versions of a target entity. The git checkout command operates upon three distinct entities: files, commits, and branches. In addition to the definition of "checkout", the phrase "checking out" is commonly used to imply the act of executing the `git checkout` command.

    `git checkout` lets you navigate between the branches created by `git branch`. Checking out a branch updates the files in the working directory to match the version stored in that branch, and it tells Git to record all new commits on that branch.

    ```bash
    # View a list of available branches
    git branch

    # Switch to a specified branch
    git checkout feature-inprogress-branch

    # Create a new branch and immediately switch to it
    git checkout -b
    ```

    Git tracks a history of checkout operations in the reflog. You can exeucte `git reflog` to view the history.

    In order to checkout a remote branch, you have to first fetch the contents of the branch with `git fetch --all`.

    ***Detached `HEAD`:***

    The `HEAD` is Git's way of referring to the current snapshot. Internally, the `git checkout` command simply updates the `HEAD` to point to either the specified branch or commit. When it points to a branch, Git doesn't complain, but when you check out a commit, it switches to a "detached `HEAD`" state.

    This is a warning telling you that everything you’re doing is “detached” from the rest of your project’s development. If you were to start developing a feature while in a detached HEAD state, there would be no branch allowing you to get back to it. When you inevitably check out another branch (e.g., to merge your feature in), there would be no way to reference your feature.

    Your development should always take place on a branch—never on a detached HEAD. This makes sure you always have a reference to your new commits.

- `git add`: stages a change. It's necessary to stage and take a snapshot of the changes to include them in the project's history. Any changes that are staged will become a part of the next snapshot and a part of the project’s history.
- `git commit`: saves the snapshot to the project history and completes the change-tracking process. Anything that’s been staged with `git add` will become a part of the snapshot with `git commit`.
- `git status` (inspecting a repository)

    Shows the status of changes as untracked, modified, or staged *(lets you see which changes have been staged, which haven't, and which files aren't being tracked by Git)*. 

    Status output does not show you any information regarding the committed project history. For this you need to use `git log`.

    ```bash
    # On branch master
    # Changes to be committed:
    # (use "git reset HEAD <file>..." to unstage)
    #
    #modified: hello.py
    #
    # Changes not staged for commit:
    # (use "git add <file>..." to update what will be committed)
    # (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #modified: main.py
    #
    # Untracked files:
    # (use "git add <file>..." to include in what will be committed)
    #
    #hello.pyc
    ```

    ***Ignoring files:*** Git lets you completely ignore some files by placing paths in a special file called `.gitignore`. Any files that you'de like to ignore should be included on a separate line, and the `*` symbol can be used as a wildcard.

    Untracked files typically fall into two categories. They're either files that have just been added to the project and haven't been committed yet, or they're compiled binaries like .`pyc`, `.obj`, `.exe`, etc. While it's definitely beneficial to include the former in the `git status` output, the latter can make it hard to see what’s actually going on in your repository.

    ```bash
    *.pyc
    ```

    It's a good practice to check the state of your repository before committing changes so that you don't accidentally commit something you don't mean to.

    ```bash
    # Edit hello.py
    git status
    # hello.py is listed under "Changes not staged for commit"
    git add hello.py
    git status
    # hello.py is listed under "Changes to be committed"
    git commit
    git status
    # nothing to commit (working directory clean)
    ```

    Some git commands (e.g., `git merge`) require the working directory to be clean so that you don't accidentally overwrite changes

- `git log`

    Displays committed snapshots. It lets you list the project history, filter it, and search for specific changes.

    While `git status` lets you inspect the working directory and the staging area, `git log` only operates on the committed history

    ```bash
# Display the entire commit history using the default formatting
    git log
    
    # Limit the number of commits by <limit>. For example, "git log -n 3" will display only 3 commits
git log -n <limit>
    
    # Condense each commit to a single line (useful for getting a high-level overview of the project history)
git log --oneline
    
    # Include which files were altered and the relative number of lines that were added or deleted from each of them
git log --stat
    
    # Display the patch representing each commit (show the full diff of each commit)
git log -p
    
    # Search for commits by a particular author (the argument can be plain string or a regular expression)
git log --author="<pattern>"
    
    # Search for commits with a commit message that matches (can be plain string or regular expression)
git log --grep="<pattern>"
    
    # Show only commits that occur between "<since>" and "<until>"
# Both arguments can be:
    # a commit ID "git log 3157e..5ab91"
    # a branch name
    # HEAD
    # or any other kind of revision reference
    # https://mirrors.edge.kernel.org/pub/software/scm/git/docs/gitrevisions.html
    git log <since>..<until>
    
    # Show only commits that include the specified file
git log <file>
    
    # A few options to consider
git log --graph --decorate --oneline
    ```
    
    Branch names and the `HEAD` keyword are other common methods for referring to individual commits. `HEAD` always refers to the current commit, be it a branch or a specific commit.

    The `~` character is useful for making relative references to the parent of a commit. For example, `3157e~1` refers to the commit before `3157e`, and `HEAD~3` is the great-grandparent of the current commit.

    ***Example:***

    ```bash
git log --author="John Smith" -p hello.py
    ```
    
    ```bash
git log --oneline master..some-feature
    ```
    
- `git branch`

    It lets you create, list, rename, and delete branches *(It doesn't let you switch between branches or put a forked history back together again. For this check `git checkout` and `git merge`)*.

    Git branches are effectively a pointer to a snapshot of your changes. When you create a branch, all Git needs to do is create a new pointer, it doesn’t change the repository in any other way.

    Branching in other VCS can be expensive operations in both time and disk space. The implementation behind Git branches is much more lightweight than other VCS modes. Instead of copying files from directory to directory, Git stores a branch as a reference to a commit. In this sense, a branch represents the tip of a series of commits—it's not a container for commits. The history for a branch is extrapolated through the commit relationships.

    ```bash
# List all of the branches in the repository
    git branch
    
    # Create a new branch
git branch <branch>
    
    # Delete the specified branch 
# (safe operation, Git prevents you from deleting the branch if it has unmerged changes)
    git branch -d <branch>
    
    # Force delete the specified branch, even if it has unmerged changes
git branch -D <branch>
    
    # Rename the current branch
git branch -m <branch>
    
    # List all remote branches
git branch -a
    ```
    
    ***Creating branches:***

    If you start with a repository like this:

    Then you creat a branch using the following command:

    ```bash
git branch crazy-experiment
    ```

    The repository history remains unchanged. All you get is a new pointer to the current commit:
    
    This only creates the new branch. To start adding commits to it, you need to select it with `git checkout`, and then use `git add` and `git commit` commands.

- `git merge`

    Merges lines of development together into a single branch.

    `git merge` is often used in conjunction with `git checkout` for selecting the current branch and `git branch -d` for deleting the obsolete target branch

    This command is typically used to combine changes made on two distinct branches. For example, a developer would merge when they want to combine changes from a feature branch into the main branch for deployment.

    When creating a merge commit Git will attempt to auto magically merge the separate histories for you. If Git encounters a piece of data that is changed in both histories it will be unable to automatically combine them. This scenario is a version control conflict and Git will need user intervention to continue.

    ***Preparing to merge:***

    1. `git status` to confirm that `HEAD` is pointing to the correct merge-receiving branch (`git checkout` if needed).
    2. `git fetch` to pull the latest remote commits (make sure the receiving branch is up-to-date).
    3. `git pull` to ensure the `master` branch has the latest updates.

    ***Fast forward merge:***

    A fast-forward merge can occur when there is a linear path from the current branch tip to the target branch. Instead of “actually” merging the branches, all Git has to do to integrate the histories is move (i.e., “fast forward”) the current branch tip up to the target branch tip.

    However, a fast-forward merge is not possible if the branches have diverged. When there is not a linear path to the target branch, Git has no choice but to combine them via a 3-way merge.

    ```bash
# Start a new feature
    git checkout -b new-feature master
    
    # Edit some files
git add <file>
    git commit -m "Start a feature"
    
    # Edit some files
git add <file>
    git commit -m "Finish a feature"
    
    # Merge in the new-feature branch
git checkout master
    git merge new-feature
    git branch -d new-feature
    
    # You can use "git merge --no-ff new-feature" for record keeping purposes (documenting all merges that occur)
```
    
    ***3-way merge:***

    3-way merges use a dedicated commit to tie together the two histories. The nomenclature comes from the fact that Git uses three commits to generate the merge commit: the two branch tips and their common ancestor.

    ```bash
# Start a new feature
    git checkout -b new-feature master

    # Edit some files
    git add <file>
    git commit -m "Start a feature"

    # Edit some files
    git add <file>
    git commit -m "Finish a feature"

    # Develop the master branch
    git checkout master
    
# Edit some files
    git add <file>
    git commit -m "Make some super-stable changes to master"

    # Merge in the new-feature branch
    git merge new-feature
    git branch -d new-feature
```
    
    Developers like to use fast-forward merges for small features or bug fixes, while reserving 3-way merges for the integration of longer-running features.
    
    ***Resolving conflict:***

    If the two branches you're trying to merge both changed the same part of the same file, Git won't be able to figure out which version to use. When such a situation occurs, it stops right before the merge commit so that you can resolve the conflicts manually.

    Git's merging process uses the edit/stage/commit workflow to resolve merge conflicts. When you encounter a merge conflict, running the `git status` command shows you which files need to be resolved.

    ```bash
here is some content not affected by the conflict
    <<<<<<< master
this is conflicted text from master
    =======
    this is conflicted text from feature branch
    >>>>>>> feature branch;
    ```
    
    Once you've identified conflicting sections, you can go in and fix up the merge to your liking. When you're ready to finish the merge, all you have to do is run git add on the conflicted file(s) to tell Git they're resolved. Then, you run a normal git commit to generate the merge commit.
    
    Merge conflicts will only occur in the event of a 3-way merge. It’s not possible to have conflicting changes in a fast-forward merge.

    ***When Git fails to start a merge:***

    A merge will fail to start when Git sees there are changes in either the working directory or staging area of the current project. Git fails to start the merge because these pending changes could be written over by the commits that are being merged in.

    ```bash
# Checkout can be used for undoing changes to files or for changing branches
    git checkout

    # Reset can be used to undo changes to the working directory and staging area
    git reset --mixed
    ```

    ***When Git conflicts arise during a merge:***
    
    A failure DURING a merge indicates a conflict between the current local branch and the branch being merged. This indicates a conflict with another developers code.

    ```bash
# Exit from the merge process and return the branch to the state before the merge again
    git merge --abort

    # Reset can be used to reset conflicted files to a know good state
    git reset
    ```

- `git pull`: updates the local line of development with updates from its remote counterpart

    Developers use this command if a teammate has made commits to a branch on a remote, and they would like to reflect those changes in their local environment

- `git push`

    Updates the remote repository with any commits made locally to a branch.

    To delete a remote branch execute:

    ```bash
    git push origin --delete crazy-experiment
    ```

    or

    ```bash
    git push origin :crazy-experiment
    ```

- `git diff`: helps find differences between states of a repository/files (usefuld in predicting and preventing merge conflicts).
- `git tag`

    [https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-tag](https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-tag)

- `git blame`

    [https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-blame](https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-blame)

- `git rebase`

    [https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase](https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase)

- `git reflog`

    [https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog](https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog)

[Undoing commits & changes](Git%20Handbook%2002fafc730ef048c38daf78b156331a58/Undoing%20commits%20&%20changes%20f515aa5938014fb0b9c9cc8901411ca3.md)

[Pull requests](Git%20Handbook%2002fafc730ef048c38daf78b156331a58/Pull%20requests%207e96e5e40bd347a197ac3111df4917e8.md)

[Git merge strategy options and examples](Git%20Handbook%2002fafc730ef048c38daf78b156331a58/Git%20merge%20strategy%20options%20and%20examples%20ed357b2a44f747f8989d96441005160b.md)

[Comparing workflows](Git%20Handbook%2002fafc730ef048c38daf78b156331a58/Comparing%20workflows%20cad17e9bbbb74542995b665731e7c2ea.md)

[Git feature branch workflow](Git%20Handbook%2002fafc730ef048c38daf78b156331a58/Git%20feature%20branch%20workflow%20c1eb650e758a45518d737f9d3ddf6005.md)

[Gitflow Workflow](Git%20Handbook%2002fafc730ef048c38daf78b156331a58/Gitflow%20Workflow%2073ac5c575c3548b0951f383bb7e5f804.md)

[Forking flow](Git%20Handbook%2002fafc730ef048c38daf78b156331a58/Forking%20flow%205237db29041e45f1b165200217938b66.md)

### GitHub and the command line

```bash
# download a repository on GitHub.com to our machine
git clone https://github.com/me/repo.git

# change into the `repo` directory
cd repo

# create a new branch to store any new changes
git branch my-branch

# switch to that branch (line of development)
git checkout my-branch

# make changes, for example, edit `file1.md` and `file2.md` using the text editor

# stage the changed files
git add file1.md file2.md

# take a snapshot of the staging area (anything that's been added)
git commit -m "my snapshot"

# push changes to github
git push --set-upstream origin my-branch
```

```bash
# create a new directory, and initialize it with git-specific functions
git init my-repo

# change into the `my-repo` directory
cd my-repo

# create the first file in the project
touch README.md

# git isn't aware of the file, stage it
git add README.md

# take a snapshot of the staging area
git commit -m "add README to initial commit"

# provide the path for the repository you created on github
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git

# push changes to github
git push --set-upstream origin main
```

```bash
# assumption: a project called `repo` already exists on the machine, and a new branch has been pushed to GitHub.com since the last time changes were made locally

# change into the `repo` directory
cd repo

# update all remote tracking branches, and the currently checked out branch
git pull

# change into the existing branch called `feature-a`
git checkout feature-a

# make changes, for example, edit `file1.md` using the text editor

# stage the changed file
git add file1.md

# take a snapshot of the staging area
git commit -m "edit file1"

# push changes to github
git push
```

### Models for collaborative development

1. Shared repository

    With a shared repository, individuals and teams are explicitly designated as contributors with read, write, or administrator access. This simple permission structure, combined with features like protected branches and Marketplace, helps teams progress quickly when they adopt GitHub.

2. Fork and pull

    Fork and pull model allows anyone who can view the project to contribute. A fork is a copy of a project under an developer’s personal account. Every developer has full control of their fork and is free to implement a fix or new feature. Work completed in forks is either kept separate, or is surfaced back to the original project via a pull request. There, maintainers can review the suggested changes before they’re merged.