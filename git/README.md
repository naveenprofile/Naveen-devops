Configure Git 
-------------
Set your username and email, which will be attached to your commits.

#git config --global user.name "naveenprofile"

#git config --global user.email "naveenprofile.fis@gmail.com"


Working with GitHub 
-------------------
Once you have a local repository and some commits, you'll want to share your work on GitHub.

Create a Repository on GitHub: Go to github.com and create a new repository. Don't initialize it with a README, as you already have a local project.

Link Your Local Repository to GitHub: Tell your local repository about the remote GitHub repository.

#git remote add origin https://github.com/naveenprofile/Naveen-devops


The name origin is a convention for the primary remote repository.

Push Your Code: Send your local commits to the remote repository on GitHub.

#git push -u origin main

git push sends commits. The -u origin main flag sets the upstream, so future pushes can just be git push.

Pull Changes: Download the latest changes from the remote repository to your local machine.


Correct the remote URL
----------------------

Now that you have the correct URL, you can update your local repository's remote.

If the remote named origin already exists but is incorrect, use this command to change it:

#git remote set-url origin https://github.com/naveenprofile/Naveen-devocd

-----------------------------------

SSH Authentication

1. Generate a new SSH key
   #ssh-keygen -t
2. Copy your public key
   #cat ~/.ssh/id_ed25519.pub
3. Now:
       GitHub → Settings
       SSH and GPG keys
       New SSH key
       Paste the key → Add SSH key
4. Test SSH connection to GitHub
   #ssh -T git@github.com
5. Set Git remote URL to SSH
   #cd /path/to/your/project
   #git remote -v
 NOte: If your remote is HTTPS like:   https://github.com/user/repo.git
   #git remote set-url origin git@github.com:<username>/<repo>.git
6. Verify:
       #git remote -v -  You should see:
        git@github.com:<username>/<repo>.git (fetch)
        git@github.com:<username>/<repo>.git (push)
7. Push your code to GitHub
    git status
    git add .
    git commit -m "Initial commit"
8. push 
    #git push -u origin main
    #git push -u origin master

----------------------------------------------------------

HTTPS + Personal Access Token (PAT) ✅ (Most common alternative)

Steps
A) Create a PAT in GitHub

GitHub → Settings
Developer settings
Personal access tokens
Choose:

Fine-grained token (recommended)
OR Classic token



Required permissions (minimum):

repo (for private repos)
contents: read/write

Copy the token (you won’t see it again).

git remote -v

Push:
git push origin test

When prompted:
Username: your-github-username
Password: <PASTE PAT HERE>

----------------------------------

GIT:

Git is a distributed version control system (VCS) used to track changes in source code and files over time.

Why Git?

Keeps history of changes
Enables collaboration (multiple people work safely)
Allows rollback to earlier versions
Works offline (local repository)

Git was created by Linus Torvalds in 2005 for Linux kernel development.

Git Repository (Repo)

 repository is a Git-managed project folder that tracks files and their history.
Types of repositories

Local repository – on your machine
Remote repository – hosted on servers like:

GitHub
GitLab
Bitbucket

Create a repository

git init - This creates a hidden folder: 

.git/ - This .git directory stores all Git data (history, commits, objects).

Git File States

Every file in Git can be in one of these states:

State                Meaning
Untracked            Git doesn’t know about the file
Modified             File changed but not staged
Staged               Ready to be committed
Committed            Saved permanetly in Git history


Staging Area (Index)

The staging area is a preparation zone where you choose what changes will go into the next commit.
Why staging?

Commit only selected changes
Better control over commits
Cleaner commit history

Add files to staging

#git add file.txt

#git add . -  Add everything 

Note: Staging just marks changes for the next commit.

Commit

A commit is a snapshot of the project at a specific point in time.

#git commit -m "Added login feature"


Each commit contains:

Unique commit hash (SHA-1)
Author name & email
Date and time
Commit message
Snapshot of staged files

Commits are immutable (cannot be changed easily).

Push

Push sends your local commits to a remote repository.

#git push origin main

Where:

origin → remote name
main → branch name

Push is needed so others can see your changes.

Git Internals (Blobs, Trees, Snapshots)

Git doesn’t store files the way you might expect.
It stores objects.

Git Object Types
1️⃣ Blob (Binary Large Object)

Stores file content only
Does NOT store:

Filename
Permissions

Identified by a SHA-1 hash

hello.txt → Blob

If two files have same content → Git stores only one blob ✅

Tree

Represents a directory
Stores:

File names
Directory structure
References to blobs and other trees



Tree
 ├── hello.txt (blob)
 └── src/ (tree)


Trees define folder hierarchy

Commit (Snapshot)
A commit is a snapshot, not a diff.
Each commit points to:

A tree (project structure)
Parent commit(s)
Metadata (author, message)


Complete Git Workflow


Working Directory
      ↓ git add
Staging Area
      ↓ git commit
Local Repository
      ↓ git push
Remote Repository


Git Branching
What is a Branch in Git?
A branch is a lightweight movable pointer to a commit.
👉 Instead of copying files, Git creates a new pointer to a commit.

Default branch: main (or master)
Branches allow parallel development
Safe experimentation without breaking main code


Why Branching is Important
✅ Develop features independently
✅ Fix bugs without affecting production
✅ Support multiple versions
✅ Enable team collaboration


How Branching Works Internally

A branch points to a commit
HEAD points to the current branch
New commits move the branch pointer forward

#git branch - list  branchs
#git branch feature-login - Create a new branch
#git checkout feature-login - Switch to a branch (git switch master)
#git checkout -b feature-login (git switch -c test) - Create & switch in one command


Making Changes in a Branch

git checkout feature-login
# edit files
git add .
git commit -m "Added login feature"

Merging Branches
Merge feature branch into main

#git checkout main
#git merge feature-login

Merge Conflicts
Happen when:

Same file
Same lines
Modified differently

Git marks conflicts:

<<<<<<< HEAD
code from main
=======
code from feature
>>>>>>> feature-login

Deleting a Branch
Delete local branch

git branch -d feature-login

Delete remote branch

git push origin --delete feature-login

Git Diff

What is git diff?
git diff shows differences between changes.

Staging Area vs Last Commit
git diff --staged or git diff --cached - Shows what will go into next commit.


#git diff commit1 commit2 - Between Two Commits
#git diff main feature-login - Between Branches - Shows what feature-login has that main doesn’t.
#git diff main feature-login -- app.py - Compare a File

Understanding git diff Output
- old line
+ new line


Git Merge & Rebase

Both merge and rebase are used to integrate changes from one branch into another.
The key difference is how they treat commit history.

Git Merge

git merge combines branches by creating a new merge commit (when needed) that has two parents.
👉 History is preserved exactly as it happened.

M = merge commit
Both branch histories remain intact


Git Rebase

git rebase moves or replays commits from one branch onto another.
👉 It rewrites commit history.

Before rebase
main ── A ── B ── C
               \
feature ── D ── E


After rebase
main ── A ── B ── C ── D' ── E'

D' and E' are new commits
Feature branch appears as if it started from latest main

git rebase -i HEAD~3  - Used to clean commit history.


You can:

squash commits
edit messages
reorder commits
drop commits

Real‑World Workflow (Best Practice)

git checkout feature
git rebase main
git checkout main
git merge feature


Interview‑Ready Answer

Git merge preserves commit history and creates a merge commit, making it safer for shared branches.

Git rebase rewrites history by replaying commits on top of another branch, creating a clean, linear history.

Rebase should be used only on local or private branches, while merge is preferred for integrating changes into main branches.


Git Stash & Pop

What is git stash?
git stash is used to temporarily save (stash) uncommitted changes 

so you can:

Switch branches
Pull latest code
Fix something urgent
without committing unfinished work
👉 Think of it as a clipboard for your working directory.

When Do You Need Git Stash?
✅ You’re working on a feature
✅ Suddenly need to switch branches
✅ Your changes are incomplete
✅ You don’t want to commit yet


Working on feature-login
Boss: "Fix prod issue NOW"


➡️ Use git stash



How git stash Works Internally
When you stash:

Git saves:

Modified tracked files
Staged changes (by default)


Working directory becomes clean
Changes are stored in a stash stack

# git stash - Stash Current Changes

# git stash push -m "message" - Stash with a Message 

# git stash list - list stashs

Git Stash Pop

What is git stash pop?
git stash pop:

Applies the latest stash
Removes it from the stash list

#git stash pop stash@{1}  - Apply Specific Stash

git stash apply   -  Applies stash but keeps it
git stash pop     -  Applies stash and deletes it

#git stash -u - Stash Untracked Files

#git stash -a - Stash Everything (Including Ignored)

#git stash show - show stash content 

#git stash clear - clear all stashs (Dangerous) -  No recovery after this.

Real‑World Workflow Example

# working on feature
git status

# stash changes
git stash push -m "WIP: payment logic"

# switch branch
git checkout main
git pull

# come back
git checkout feature-payment
git stash pop

Interview‑Ready Answer

Git stash temporarily saves uncommitted changes so you can work on something else without committing.
Git stash pop restores the stashed changes and removes them from the stash list.
It’s commonly used when switching branches or pulling changes with a dirty working directory.


Git Cherry‑Pick

What is git cherry-pick?
git cherry-pick is used to apply a specific commit (or commits) from one branch onto another branch.

👉 Instead of merging an entire branch, you pick only the required commit(s).


Why Use Cherry‑Pick?
✅ You need one bug fix from another branch
✅ You don’t want to merge all changes
✅ Hotfix needs to go to main only
✅ Backporting fixes to older versions

#git cherry-pick a1b2c3d

This:

Copies changes from commit a1b2c3d
Creates a new commit on the current branch

Diagram: Cherry‑Pick vs Merge

Before
main ── A ── B
feature ── C ── D

Cherry‑pick commit C onto main
main ── A ── B ── C'

✅ Only C is copied
❌ D is ignored

git checkout main
git cherry-pick <commit-hash>

git cherry-pick commit1^..commit3 - Cherry‑Pick a Range of Commits
git cherry-pick commit1 commit2 commit3 - Cherry‑Pick Multiple Commits


Real‑World Example (Hotfix)

# Bug fixed in develop
git log develop

# Cherry-pick fix to main
git checkout main
git cherry-pick f9e8d7c
git push origin main

Interview‑Ready Answer

Git cherry‑pick is used to apply a specific commit from one branch to another.
It creates a new commit with the same changes but a different hash, making it ideal for hotfixes or backporting changes without merging the entire branch.

Git Tag

What is a Git Tag?
A Git tag is a named reference to a specific commit, usually used to mark:

Releases
Versions
Important milestones

👉 Unlike branches, tags do not move.

Why Use Git Tags?
✅ Mark production releases (v1.0.0)
✅ Easy rollback to a known version
✅ CI/CD release triggers
✅ Versioning & auditing

git tag v1.0.0 -  Lightweight Tag - Just a pointer to a commit and  No metadata

git tag -a v1.0.0 -m "Release version 1.0.0" - Annotated Tag 

Stored as full Git object
Contains:

Tagger name
Date
Message


git show v1.0.0 - View Tag Details

git tag -a v1.0.1 <commit-hash> -m "Hotfix release"- Tag a Specific Commit


git push origin v1.0.0 - Push Tags to Remote

git push origin --tags - Push all tags

git tag -d v1.0.0 - Delete local tag

git push origin --delete v1.0.0 - Delete remote tag


Git Squash (Squashing Commits)

What is Squash?
Squashing means combining multiple commits into a single commit.
👉 Used to keep clean and readable history.

Why Squash Commits?
✅ Clean up noisy commit history
✅ Combine WIP commits
✅ Improve code review clarity
✅ Follow Trunk‑Based or PR‑based workflows

Common Squash Scenarios

Feature branch has many small commits
You want 1 clean commit before merging
Squash during Pull Request merge

git rebase -i HEAD~3 - Squash last 3 commits

Editor opens:
pick a1b2c3 Add login UI
pick d4e5f6 Fix validation
pick g7h8i9 Fix typo

Change to:
pick a1b2c3 Add login UI
squash d4e5f6 Fix validation
squash g7h8i9 Fix typo

✅ Commits combined into one
✅ Edit final commit message

Squash and Keep Commit Message

fixup <commit>

git merge --squash feature-login
git commit -m "Add login feature"

✅ All feature commits → 1 commit
❌ Feature branch history not preserved


Real‑World Workflow Example

# Feature work
git checkout -b feature-payment
# many commits...

# Clean history
git rebase -i main

# Merge
git checkout main
git merge feature-payment

# Tag release
git tag -a v2.0.0 -m "Payment feature release"
git push origin main --tags


Interview‑Ready Answers
Git Tag

Git tag is used to mark a specific commit, usually for releases. Annotated tags store metadata and are preferred for production versions.

Squash

Squashing combines multiple commits into a single commit to maintain a clean history. It is commonly done using interactive rebase or squash merge before merging feature branches.