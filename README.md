# Git Lecture Notes

# The Problem

* You've been working on a project for a while now, and it's mostly working. 
* You realize there may be a better way to do something.
* You want to try the new way, but don't want to lose the work you already have.

* Solution 1:
    * Continue working and hope you can `ctrl-z` back far enough
* Solution 2:
    * Create a backup of the file before you make any changes
* Solution 3:
    * Use a Version Control System


# Version Control System (VCS)



* A system for tracking changes to files in a project
    * Replaces saving multiple versions of files 
* Primarily Used for Collaboration
    * Either prevents two people from making changes to the same file
    * Or provides a way to merge the two versions of a file together


```mermaid
%%{
  init: {
    'theme': 'base',
    'themeVariables': {
      'primaryColor': '#586e75',
      'primaryTextColor': '#fff',
      'primaryBorderColor': '#000',
      'lineColor': 'saddlebrown',
      'secondaryColor': 'saddlebrown',
      'secondaryTextColor': '#000',
      'tertiaryTextColor': '#657b83',
      'tertiaryBorderColor': '#586e75',
      'tertiaryColor': 'transparent'
    }
  }
}%%
flowchart TD
    subgraph Distributed
        D-.Pull.->E
        E-.Push.->D
        E-.Checkout.->F
        F-.Commit.->E
        D-.Pull.->G
        G-.Push.->D
        G-.Checkout.->H
        H-.Commit.->G
        subgraph Server2
            D[Remote Repo]
        end
        subgraph Workstation3
            E[Local Repo]
            F[Working Copy]
        end
        subgraph Workstation4
            G[Local Repo]
            H[Working Copy]
        end
    end
    subgraph Centralized
        A-.Checkout.->B
        B-.Commit.->A
        A-.Checkout.->C
        C-.Commit.->A
        subgraph Server1
            A[Remote Repo]
        end
        subgraph Workstation1
            B[Working Copy]
        end
        subgraph Workstation2
            C[Working Copy]
        end
    end
```

## What is Git?


* Free and Open Source DVCS
* Developed for the Linux kernel
* Command-line utility


## Git is Not...

* The only Free and Open Source VCS
    * (CVCS) Subversion (SVN)
    * (DVCS) Mercurial (Hg)
* Synonymous with GitHub
    * GitLab
    * BitBucket
* Immune to Human Error

## Installation


* [https://git-scm.com/downloads](https://git-scm.com/downloads)
* Select your OS
* Defaults are usually fine
* Test in Terminal, Powershell, or Commandline

```bash
git --version
```

* Setup a default username and email

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

**Note:** enter these commands one line at a time, changing `Your Name` and `your-email@example.com`.

# Terminology

* **Repository:** Database of files and changes to those files
* **Commit:** A snapshot of changes made since the last commit
    * Requires a Message
* **Branch:** Divergence from the main development stack
    * **HEAD:** pointer to current branch
* **Remote:** Repository hosted on the Internet or a Network Server
    * **Default:** `origin`
* **Clone:** Create a local copy of a Remote Repository
* **Fork:** Split in the development of a project
    * Primarily a social convention in Git



# Common Git Commands

## First Open Folder

First open the folder that contains the repository or a new folder

```bash
cd "C:\path\to\folder"
```

## Example: Terminal

![](./img/cmd-check-folder.png)

## Example: Visual Studio Code

![](./img/code-open-folder.png)

# Git Init

Initializes a new Git repository in the current directory

```bash
git init
```

## Example: Terminal

![](./img/cmd-git-init.png)

## Example: Visual Studio Code

![](./img/code-git-init.png)


# Git Remote Add


Add a remote repository to push and pull from

```bash
git remote add <shortname> <url>
```

* **shortname** - name the remote (default: `origin`)

## Example: Terminal

![](./img/cmd-git-remote-add.png)

## Example: Visual Studio Code

![](./img/code-add-remote-1.png)
![](./img/code-add-remote-2.png)
![](./img/code-add-remote-3.png)
![](./img/code-add-remote-4.png)
![](./img/code-add-remote-5.png)
![](./img/code-add-remote-6.png)

# Git Clone

Clone a remote repository to a local folder

```bash
git clone <url> [<destination>]
```

## Example: Terminal

![](./img/cmd-git-clone.png)

## Example: Visual Studio Code

![](./img/code-git-clone-1.png)
![](./img/code-git-clone-2.png)
![](./img/code-git-clone-3.png)
![](./img/code-git-clone-4.png)


# Git Commit

Creating a commit is a multi-step process.

1. View which files have changed
2. New and Updated/Changed files must be **Staged**
3. Staged files can then be **Committed**
    1. Every commit requires a commit **Message**
4. **Pull** and **Push** new commits to the remote repository

## Git Status

Lists all new or modified files to be committed

```bash
git status  
```

## Example: Terminal

![](./img/cmd-git-status.png)

## Example: Visual Studio Code

![](./img/code-git-status.png)

## Git Add

Adds new or modified files to the Staging Area

```bash
git add
```

## Example: Terminal

![](./img/cmd-git-commit-1-stage-changes.png)

## Example: Visual Studio Code

![](./img/code-git-commit-1-stage-changes.png)
![](./img/code-git-commit-2-stage-changes.png)

## Git Commit

Commit files in the Staging Area to the Local Repo

```bash
git commit
# Commit with message
git commit -m "Message"
```

## Example: Terminal

![](./img/cmd-git-commit-2.png)

## Example: Visual Studio Code

![](./img/code-git-commit-3-message.png)
![](./img/code-git-clone-4.png)

## Git Pull and Git Push

**Push** changes in the Local Repo to the Remote Repo

**Pull** changes to the current branch in the Remote Repo to the Local Repo and merge them with the Working Copy

```bash
git push
git pull
```

## Example: Terminal

![](./img/cmd-git-pull-push.png)

## Example: Visual Studio Code

![](./img/code-git-push.png)



```mermaid
%%{
  init: {
    'theme': 'base',
    'themeVariables': {
      'primaryColor': '#586e75',
      'primaryTextColor': '#fff',
      'primaryBorderColor': '#000',
      'lineColor': 'saddlebrown',
      'signalColor': 'saddlebrown',
      'signalTextColor': 'saddlebrown',
      'loopTextColor': '#657b83',
      'tertiaryBorderColor': '#586e75',
      'tertiaryColor': 'transparent'
    }
  }
}%%

sequenceDiagram
    loop Doing Work
        Working Copy ->> Staging Area: git add
        Staging Area ->> Local Repo: git commit
    end
    Local Repo ->> Remote Repo: git push
    Remote Repo ->> Local Repo: git fetch
    Local Repo ->> Working Copy: git merge
    Remote Repo ->> Working Copy: git pull
```

# Branching



* Divisions in Commit History
* Reasons
    * Separate Development code from Release code
    * Different Developers
    * Separate Features
    * Experimentation



## Branching Commands



```bash
# Create new branch
git branch branch_name

# Switch to branch
git checkout branch_name

# Create and switch to new branch
git checkout -b branch_name

# Merge branch_name into current branch
git merge branch_name
# Fix unrelated histories
git merge branch_name --allow-unrelated-histories

# Delete branch_name
git branch -d branch_name
```




```mermaid
%%{
  init: {
    'theme': 'forest',
    'themeVariables': {
        'git0': '#586e75',
        'git1': '#586e75',
        'git2': '#586e75',
        'gitBranchLabel1': 'white',
        'gitBranchLabel2': 'white',
        'commitLabelBackground': 'saddlebrown',
        'commitLabelColor': 'white'
    }
  }
}%%

gitGraph
    commit id: "git init; git commit;"
    commit
    branch dev order: 3
    checkout dev
    commit id: "git checkout -b dev; git commit;"
    commit id: " "
    checkout main
    merge dev id: "git checkout main; git merge dev;"
    branch hotfix order: 1
    checkout hotfix
    commit id: "git checkout -b hotfix; git commit;"
    commit id: "  "
    checkout dev
    merge hotfix id: "git checkout dev; git merge hotfix;"
    checkout main
    merge hotfix id: "git checkout main; git merge hotfix;"
    checkout dev
    commit
    checkout dev
    commit
    commit
    checkout main
    merge dev id: "git checkout main; git merge dev"
```

## Example

```bash
git log --oneline --graph
* eb7c5e8 (HEAD -> main) Sixth Commit
*   3ec1f3f Merge branch 'dev'
|\
| * 4cf3b81 (dev) Fifth Commit
| * 680f0d5 Fourth Commit
* | 51ab31b Third Commit
|/
* daac988 Second Commit
* 46091e9 Initial Commit
```



# Quick Check

What Git command creates a snapshot of the repository?

<ul>

<li>`git add`</li>
<li>`git commit`</li>
<li>`git pull`</li>
<li>`git push`</li>

</ul>


# Conflicts



If Git cannot easily merge the files two branches, you will get conflicts that look like this:

```bash
 <<<<<<< HEAD
 Commit On Main
 =======
 Commit On Dev
 >>>>>>> dev
```

* Everything between `<<<<<<< HEAD` and the `=======` is what is in the current branch
* Everything between the `=======` and the `>>>>>>> <branch-name>` is what is being merged into the current branch.


## Conflicts

* To resolve a conflict, 
    * replace the entire section with the version you want (or combine the two), 
    * `git add` the file
    * `git commit` to continue the merge.
* Now, `git log --oneline --graph` looks like this:


```bash
*   4caadd6 (HEAD -> main) Merge branch 'dev'
|\
| * ce4109b (dev) Dev Commit
* | 3021407 Main Commit
|/
* 79e0f1c (hotfix) Hotfix Commit
* eb7c5e8 Sixth Commit
*   3ec1f3f Merge branch 'dev'
|\
| * 4cf3b81 Fifth Commit
| * 680f0d5 Fourth Commit
* | 51ab31b Third Commit
|/
* daac988 Second Commit
* 46091e9 Initial Commit
```



# Fixing Things



## Commits



```bash
# Change commit message
git commit --amend

# Change commit content
git add <files>
git commit --amend
```

Make changes to previous commit

## Unstage File



```bash
git reset HEAD <file>
```

Remove files after using **git add**

## Reset Modified File


```bash
git checkout -- <file>
```

Undo changes since last commit

**Note: Be careful!** All changes to the file will be erased.

**Note:** notice the space after the `--`.



# Remotes



## Basic Commands



```bash
# Show all remotes
git remote

# Add a remote
git remote add <shortname> <url>

# Copies all changes in the Remote Repo to the Local Repo
git fetch <remote>
# Fetch the default "origin"
git fetch

# Pushes changes in the Local Repo to the Remote Repo
git push

# Pulls changes to the current branch in the Remote Repo to the Local Repo and merges them with the Working Copy
git pull

# Fix unrelated histories
git pull --allow-unrelated-histories
```


# Reading and Tutorials


* Free eBook: [https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)
