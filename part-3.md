### [Back to first page](./README.md)
## Part 3: Multi-branch collaborative development


## Table of Contents

- [Create a branch](#create-a-branch)
- [Create .gitignore](#create-gitignore)
- [Untracked files in the directory](#untracked-files-in-the-directory)
- [Fast forward merge](#fast-forward-merge)
- [Conflicted merge](#conflicted-merge)
- [Bad practice](#bad-practice)


---

## Admin

## Create a branch

1. **Ensure latest version of remote repo:**
    
    Here is the continuation of the part-2, if you are joining in the workshop at this point, go to part-2 and perform step 1-10 and come back here. 
   ```bash
   git fetch 
   git status 
   git pull # if needed
   ```

2. **Create and switch to admin branch:**
   ```bash
   git branch admin-br
   git switch admin-br
   ```

3. **Create new files and folders:**
   ```bash
   touch admin-test.txt
   mkdir raw-data
   cd raw-data
   touch admin-data.txt
   cd ..
   git status
   ```

## Create .gitignore

4. **Generate and update .gitignore:**
    - These files and folders you added are some experimentation and raw data and you don't need to include them in your Git history, so we want to ignore them. 
   ```bash
   touch .gitignore 
   echo "admin-test.txt" >> .gitignore
   echo "raw-data/" >> .gitignore
   git status 
   ```
   ❓1. Compare the result of git status with the one in step 3, what is the difference? 

   ❓2. Can you think of potential things to ignore in a repo? 

5. **Update and commit while ignoring:**
   - Open `demo.txt` and add this sentence: “Input 1 to admin-br by admin”
   - Add and commit:
   ```bash
   git add . 
   git commit -m "commit 1 to admin-br by admin"
   ```

6. **Continue updating:**
   - You continue your work and track your version in your branch. 
   - Open `demo.txt` and add this sentence: “Input 2 to admin-br by admin”.
   - Add and commit in one command:
   ```bash
   git commit -a -m "commit 2 to admin-br by admin"
   ```

7. **Push the branch to remote:**
   ```bash
   git branch
   git branch -r
   git push
   ```

   ❓3. You get an error, why? Run the following command, it might give you some clue: 

   ```bash
   git remote show origin
   ```
   
   - To fix the error, push with setting an upstream:  

   ```Bash
   git push -u origin admin-br # Set upstream
   git branch -r
   ```

   ```bash
   git remote show origin
   ```
   ❓4. What has changed now? 


## Collaborator

8. **Ensure latest version of remote repo:**
   ```bash
   git fetch 
   git status 
   git pull # if needed
   ```

9. **Create and switch to collaborator branch:**
   ```bash
   git branch collab-br
   git switch collab-br
   ```

10. **Create new files and folders:**

    ```bash
    touch collab-test.txt
    mkdir raw-data
    cd raw-data
    touch collab-data.txt
    cd ..
    git status
    ```

## Create .gitignore


11. **Generate and Update .gitignore:**
    ```bash
    touch .gitignore 
    echo "collab-test.txt" >> .gitignore
    echo "raw-data/" >> .gitignore
    git status
    ```
    ❓5. Compare the result of git status with the one in step 10, what is the difference? 

12. **Update and Commit:**
    - Open `demo.txt` and add this sentence: “Input 1 to collab-br by collaborator”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "Commit 1 to collab-br by collaborator"
    ```

13. **Continue Updating:**
     - You continue your work and track your version in your branch. 
     - Open `demo.txt` and add this sentence: “Input 2 to collab-br by collaborator”.
     - Add and commit in one command:
      ```bash
      git commit -a -m "Commit 2 to collab-br by collaborator"
      ```
      
14. **Push Changes to Remote:**
    ```Bash
    git branch
    git branch -r
    git push
    ```
    ❓6. You get an error, do you know why? This is similar to step 7, if you still struggle with it, ask for help. 

    - Push with setting an upstream:  
     ```Bash
     git push -u origin collab-br # Set upstream
     ```
    ❓7. What is the difference of this approach with part 2? Why can we push without merge conflict? 

## Admin
## Untracked files in the directory



15. **Switch to main and update:**
    ```bash
    git switch main
    git fetch
    git status
    git pull # if needed
    ```

16. **Inspect untracked files:**
    ```bash
    git status
    ```
    ❓ 8. Check that you have 1 file and 1 folder to add when you are in main branch, these are the same files that you added when your HEAD was in your branch, do you know why they show up here? 

## Fast forward merge


17. **Merge admin-br to main:**
    - Ensure you are in main branch:
     ```bash
    git merge admin-br
    ```
    ❓9. Do you know fast forward means in this case?  

    - Inspect what is left to be added: 
    ```bash
    git status
    ```
    ❓10. Why the file and folder that was shown in step 16 are not there anymore? 

18. **Push merged changes to remote:**
    ```bash
    git push
    ```

## Collaborator

## Conflicted merge



19. **Switch to main and update:**
    ```bash
    git switch main
    git fetch
    git status
    git pull # if needed
    ```
20. **Inspect untracked files:**
    ```bash
    git status
    ```
    ❓11. Check if you have 1 file to add when you are in main branch. This is the same files that you added when your HEAD was in your branch. Do you know why this end up here? 
    
    ❓12. By the way, the folder that you added as 'raw-data' does not show up here, do you know why?  

21. **Merge collab-br into main:**
    ```bash
    git merge collab-br
    ```
    ❓13. Why do you have conflict even if you worked in separate branches? What is the point with branches if you get the merge conflict when you merge to main anyway? 

    - Resolve conflicts in your code editor and save.
    - Inspect what is left to be added: 
    ```bash
    git status
    ```
    ❓14. Why the file that was shown in step 20 is not there anymore? 

22. **Commit, and push:**
    ```bash
    git add . 
    git commit -m "merge commit 1 to main by collaborator"
    git push 
    ```
## Bad practice

## Admin

23. **Pull the latest changes:**
    ```bash
    git pull
    ```
24. **Update, commit and push to main branch:** 
    - Open `demo.txt` and add this sentence: “Input 3 to main by admin - this is a critical point, but it is going to be overwritten by collaborator by merging to main”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "Commit 3 to main by admin"
    git push
    ```

## Collaborator 

25. **Switch to collbar-br, Update, Commit and push:**
    ```bash
    git switch collab-br
    ```
    - Open `demo.txt` and add this sentence: “Input 3 to collab-br by collaborator - this is going to mess with the main branch”

    - Add and commit:
    ```bash
    git add . 
    git commit -m "Commit 3 to collab-br by collaborator"
    ```

26. **Switch to main and update:**
    ```bash
    git switch main
    git fetch
    git status
    git pull # if needed
    ```
27. **Merge collab-br into main:**
    ```bash
    git merge collab-br
    ```
    - Resolve conflicts in your code editor, this time accept incoming changes and save.
    
28. **Commit, and push:**
    ```bash
    git add . 
    git commit -m "merge commit 2 to main by collaborator"
    git push 
    ```
    ❓ 15. Check the content of the main, Do you see the critical sentence that was added in step 24?   
    ❓ 16. Do you have any idea how to avoid such critical mistakes? 
### [Back to first page](./README.md)

