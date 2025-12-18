

### [Back to first page](./README.md)

## Part 2: Single-Branch Collaborative Development

## Table of Contents

- [Initiate a project from Git](#initiate-a-project-from-git)
- [Create a remote repository and connect](#create-a-remote-repository-and-connect)
- [Commit / Push / Pull](#commit--push--pull)
- [Create and resolve a merge conflict](#create-and-resolve-a-merge-conflict)
- [Detach the HEAD](#detach-the-head)

---

## Admin

## Initiate a project from Git


1. **Create a local demo project:**
    - Make a directory for a demo project on your local machine and initialize a local repository. **This directory should be different from the one you used for Part 1**:
   ```bash
   cd <into the folder that you want to place the workshop material in>
   mkdir vc-demo-collab
   cd vc-demo-collab
   git status 
   git init 
   git status 
   ```

    ❓1. What is the difference between the git status output before and after git init?  


2. **Create `demo.txt` and make initial commit:**
    - Generate a text file and name it `demo.txt`:
   ```bash
    touch demo.txt # Windows PowerShell alternative: New-Item demo.txt
   ```
    - Open the file in your IDE and add: "Input 1 to master branch by admin", then save the file.
   - Add and commit changes:
   ```bash
   git add . 
   git commit -m "commit 1 to master by admin"
   ```
    


## Create a remote repository and connect

3. **Create a repository on GitHub:**
    - Create a **private** repository named "vc-demo-collab" **without a README**.

    ❓2. What is the difference between this approach for initiating a repo and the one we did in part 1? 
4. **Rename branch:**
   - Rename the branch from master to main:
    ```bash
    git branch -M main
    ```
    ❓3. Why do we need to do this? 

5. **Connect local to remote:**
    - Add a remote repository:
   ```bash
   git remote show origin
   git remote add origin <https of repo on github>
   git remote show origin
   ```
     ❓4. Do you see the fetch and push URL there? 
     ❓5. Can you see the connection between remote and local branch? 

6. **Push to remote and set tracking:**
   - Push the first commit:
   ```bash
   git status
   git push 
   ```
   ❓6. You see an error, do you know why this happens? Follow along to fix it. 
   
    - Push with setting the upstream:
     ```bash
     git push -u origin main
     git status 
     git remote show origin
     ```
    
    ❓7. Compare the output of this step with output of step 5, what is the difference? 

7. **Add collaborator:**
    - Go to `Settings > Collaborators` and add a collaborator to the project.

## Collaborator

## Commit / Push / Pull



8. **Clone the repo:**
    - Find the repository created by the admin in your repository list, clone it, and `cd` into the cloned directory:
     ```bash
     git clone <https of repo on github> 
     cd <into the folder that was created by clone>
     ```

9. **Edit and commit:**
    - Open `demo.txt` and add: "Input 1 to main branch by collaborator", then save the file.
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
    ❓8. This time with pushing you did not get the same error as the admin did, do you know why? Run the following command and compare the output with step 5, this might give you a clue. 

     ```bash
     git remote show origin
     ```
## Admin

11. **Pull Latest Changes:**
    ```bash
    git pull 
    ```

12. **Edit and Commit:**
    - Open `demo.txt` and add: "Input 2 to main branch by admin", then save the file.
    - Add and commit:
      ```bash
      git add . 
      git commit -m "commit 2 to main by admin"
      ```

13. **Push Changes:**
    ```bash
    git push 
    ```

## Collaborator

## Create and Resolve a Merge Conflict



14. **Create Conflict:**
    - **Collaborator does not pull before applying changes**
    - Open `demo.txt` and add: "Input 2 to main branch by collaborator", then save the file.
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 2 to main by collaborator"
    ```

15. **Push fails:**
     ```bash
     git push 
     ```
     - Inspect the error 
    
    ❓9. Why can't we push?

16. **Pull the divergence:**
    - Push fails, so fetch and pull changes:
    ```bash
    git fetch
    git status 
    git pull 
    ```
    ❓10. Did you get a merge conflict? Why? 

    - If instead of a merge conflict you got the pull strategy options, you are using a newer version of Git that requires you to choose a default. Select the option that avoids rebase (e.g., `git config pull.rebase false`). Ask for help if not sure.

    ❓11. Why is it called a merge? 

17. **Resolve Conflict:**
    - Resolve in RStudio or VS Code. It means select which version to stay (keep both changes) in the file and save it. Ask for help if you are in doubt. 
    - In VS Code, avoid pressing the "Resolve in Merge Editor" button; at this point inline comparison is enough. 

    - Add file and commit:
    ```bash
    git add . 
    git commit -m "commit 3 to main by collaborator, conflict resolved"
    ```
    ❓12. Do you know why you needed to commit again?

18. **Push Resolved Conflicts:**
    ```bash
    git push 
    ```

## Admin

19. **Pull latest version:**
     ```bash
     git pull
     ```

## Both Admin & Collaborator

## Detach the HEAD


20. **Check Out Previous Commit:**
    - View git log 
    ```bash
    git log --oneline
    ```
    - Copy the hash of the commit you want to check out.
    - Checkout the commit and explore:
    ```bash
    git checkout <commit hash>
    git log --oneline --all 
    ```
    ❓13. Do you see the detached HEAD in the log and Git Graph?
    
    ❓14. Can you verify if the content of `demo.txt` matches the corresponding commit?

21. **Return to Main without change:**
    - If you want to go back to main without any commit or change simply attach the head back and switch to main:
    ```bash
    git switch - # if this does not work, run git switch main 
    git log --oneline --all
    ```
    ❓15. Did your checkout leave a trace? Did it change anything? 

22. **Create a Branch from the detached head state:**
    - Repeat step 20, now we want to make new branch from there 
    - Create a new branch from this detached HEAD state:
    ```bash
    git switch -c test-br
    ``` 
    Open `demo.txt` and add: "Input to test-br branch by admin from detached HEAD state", then save the file.
    
    ```bash
    git commit -a -m "commit from the detached head state" # add and commit with one command
    ```
    ❓16. Can you imagine a scenario where this functionality can be useful? 
23. **Switch Back to Main Branch:**
    ```bash
    git switch main 
    ```
    ❓17. Compare with step 21, did your checkout leave a trace? Did it change anything? 


### [Back to first page](./README.md)
