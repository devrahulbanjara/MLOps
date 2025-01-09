# Git and GitHub

## Introduction

Git is a **Version Control System (VCS)** or **Source Code Management (SCM)** tool that helps developers manage changes to their codebase efficiently.

### Key Features of Git:

- **Version Control for Bug Fixing**: Git allows rolling back to previous versions if the new one is unsatisfactory or contains bugs.
- **Collaboration**: Facilitates teamwork by synchronizing progress among team members.
- **Non-linear Development**: Enables multiple developers to work on the same task simultaneously using branches that can be merged later.

## Git End-to-End Workflow

Git's workflow involves:
1. Adding changes to the **staging area**.
2. Committing the changes to the **local repository**.
3. Pushing the changes to a **remote repository** (e.g., GitHub).

### Example Workflow:
- Suppose today's work is complete:
  1. Add the changes to the staging area.
  2. Commit the changes to the local repository.
  3. Push the changes to the remote repository.
- Tomorrow, you can continue from where you left off by following the same process.

### Non-linear Development:
- Developers can create new branches to work on specific features or tasks without risking the main codebase.
- Once the feature is ready, it can be merged into the main branch.

## Git Hands-On

1. **Creating a New File**:
   - Create a file `first.py` and add some content.
   - Run `git status` to see that the file is untracked.

2. **Tracking a File**:
   - Use `git add first.py` to add the file to the staging area. Now the file will be tracked.
   - Modify `first.py` and run `git status` again to see that it shows as modified.

3. **Adding Another File**:
   - Create a new file `second.py`.
   - Run `git status` to see:
     - `first.py` as modified.
     - `second.py` as untracked.

4. **Progression**:
   - Repeat the `git add`, `git commit`, and `git push` steps to manage changes and maintain version control effectively.


basic commands

git init, initializes a folder as a git repo

git status - tells me the current status of my repo

git add. adds to staging area, starts tracking files 

git commit - with a commit message you can rollback to a previous version by looking at the commit message where you left like a checkpoint, without commit message it is diffucult to figure out

git ignore - adding a file inside this file will make sure that file is not trakcked, useful in such cases when i have stored some important credentails



git log --oneline , shows my commits history , which looks like this in my case
(base) rahul@Rahul:/mnt/c/Users/Rahul/Desktop/MLOps$ git log --oneline
081a152 (HEAD -> main) 🚀 [Add] .gitignore
e344153 (origin/main, origin/HEAD, secondary) 🚀[Update] README.md
247eb93 Structure the folders
4f0b634 Complete the Introduction
0c54161 Update README.md
4465cf4 Update README.md
e6c6f90 Start with the intro
6c055a7 Initial commit


git log --stat shows the changes in file with the number of insertions and deletions in each file, this shows a detailed approach than git log --oneline


git log -p shows changes on commit level, changes in the lines of code


lets suppose i want to rollback to the first commit, assuming things went wrong after that time, so how do i go to that commit ?
copy the SHA Id from git log --online of the commit, and do git checkout SHA ID,
examples git checkout 6c055a7 in my case (this is the SHA ID of the first commit in mine)


branch concepts

let us suppose i am currently in the commit "3rd commit"
i create a new branch from my main,
git branch helper
we can do git branch helper <sha id> , to create a branch from previous commit

do git branch to see which branch we are in, shows * infront of the branch