### [Back to Table of Contents](./README.md)

## Part 2: Single-Branch Collaborative Development

## Table of Contents

- [Initiate a project from Git](#initiate-a-project-from-git)
- [Create a remote repository and connect](#create-a-remote-repository-and-connect)
- [Clone / Push / Pull](#clone--push--pull)
- [Create and resolve a merge conflict](#create-and-resolve-a-merge-conflict)
- [Detach your head](#detach-your-head)

---

## Initiate a project from Git

### Admin

1. **Create a local demo project:**
   - Make a directory for a demo project on your local machine and initialize a local repo:
     ```bash
     cd <into the folder that to place the workshop material>
     mkdir vc-demo-local
     cd vc-demo-local
     git status 
     git init 
     git status 
     ```

2. **Create `demo.txt` and make initial commit:**
   - Generate a text file and name it “demo.txt”:
     ```bash
     touch demo.txt 
     ```
   - Open the file in your IDE and add: “Input 1 to master branch by admin”, save the file.
   - Add and commit changes:
     ```bash
     git add . 
     git commit -m "commit 1 to master by admin"
     ```

## Create a remote repository and connect

3. **Create a repo On GitHub:**
   - Create a repo named “vc-demo” without README.

4. **Rename branch:**
   - Rename the branch from master to main:
    ```bash
    git branch -M main
    ```
5. **Connect local to remote:**
   - Add a remote repository:
   ```bash
   git remote show origin
   git remote add origin <https of repo on github>
   git remote show origin
   ```

6. **Push to remote and set tracking:**
   - Push the first commit and track main branch on remote:
   ```bash
   git status
   git push 
   ```
   - You see the error, we'll fix it now by setting current branch to track the main branch on the remote repo: 
    ```Bash 
     git push -u origin main
     git status 
     git remote show origin
     ```

7. **Add collaborator:**
   - Go to `settings > collaborators` and add a collaborator to the project.

## Clone / Push / Pull

### Collaborator

8. **Clone the repo:**
   - Find the repo by the admin in your repository list and clone it:
     ```bash
     git clone <https of repo on github> 
     ```

9. **Edit `demo.txt` and commit:**
   - Open `demo.txt` and add: “Input 1 to main branch by collaborator”, save the file.
   - Add and commit changes:
     ```bash
     git add . 
     git commit -m "commit 1 to main by collaborator"
     ```

10. **Push Changes to Remote:**
   - Push changes:
     ```bash
     git push 
     ```

### Admin

11. **Pull Latest Changes:**
    ```bash
    git pull 
    ```

12. **Edit and Commit:**
    - Open `demo.txt` and add: “Input 2 to main branch by admin”, save the file.
    - Add and commit:
      ```bash
      git add . 
      git commit -m "commit 2 to main by admin"
      ```

13. **Push Changes:**
    ```bash
    git push 
    ```

## Create and Resolve a Merge Conflict

### Collaborator

14. **Create Conflict:**
    - Collaborator does not pull before applying changes
    - Open `demo.txt` and add: “Input 2 to main branch by collaborator”, save the file.
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 2 to main by collaborator"
    ```

15. **Push fails**
     ```bash
     git push 
     ```
     - Inspect the error 

16. **Pull the diverence:**
    - Push fails, so fetch and pull changes:
      ```bash
      git fetch
      git status 
      git pull 
      ```

17. **Resolve Conflict:**
    - Resolve in RStudio or VS Code.
    - Add file and commit:
      ```bash
      git add . 
      git commit -m "commit 3 to main by collaborator, conflict resolved"
      ```

18. **Push Resolved Conflicts:**
    ```bash
    git push 
    ```

### Admin

19. **Pull Latest Version:**
    ```bash
    git pull
    ```

## Detach Your Head

### Both Admin & Collaborator

   - View git log:
    ```bash
    git log --oneline
    ```

20. **Check Out Previous Commit:**
    - Switch to specific commit to explore, copy the commit hash:
      ```bash
      git checkout <commit hash>
      git log --oneline --all 
      ```
    - Do you see the detachted head?


21. **Create a Branch from the detached head state:**
    - If retaining changes, commit and create new branch:
      ```bash
      git switch -c <branch name>
      git commit -a -m "commit from the detached head state"
      ```

22. **Switch Back to Main Branch:**
    ```bash
    git switch main 
    ```

23. **Return to Main without change:**
    - If you want to go back to main without any commit or change simply attach the head back and switch to main:
      ```bash
      git switch - 
      ```
### [Back to Table of Contents](./README.md)
