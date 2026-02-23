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
