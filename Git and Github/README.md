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