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