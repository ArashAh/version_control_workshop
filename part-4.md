# Part 4: Multi-branch collaborative development, best practices

## Table of Contents

- [Stash-checkout-checkin-pop ](#stash-checkout-checkin-pop)
- [Merge from main](#merge-from-main)
- [Pull request - after conflicts resolved](#pull-request---after-conflicts-resolved)
- [Pull request - without conflicts resolved](#pull-request---without-conflicts-resolved)
- [Merge to main without pull request](#merge-to-main-without-pull-request)

---

## Admin

1. **Ensure latest version of remote repo:**
   ```bash
   git fetch 
   git status 
   git pull # if needed
   ```

2. **Update and commit:**
   - Open `demo.txt` and add this sentence: “Input 1 to main by admin, collaborator can start with this commit and continue on a new branch”
   - Add and commit:
   ```bash
   git add . 
   git commit -m "commit 1 to main by admin"
   ```

3. **Push changes to remote:**
   ```bash
   git push
   ```

## Collaborator

4. **Ensure latest version of remote repo:**
   ```bash
   git fetch 
   git status 
   git pull 
   ```

5. **Create and switch to a new branch:**
   ```bash
   git branch collab-br2
   git switch collab-br2
   ```

6. **Update and commit:**
   - Open `demo.txt` and add this sentence: “Input 1 to collab-br2 by collaborator, admin should take a look at this before going ahead”
   - Add and commit:
   ```bash
   git add . 
   git commit -m "Commit 1 to collab-br2 by collaborator"
   ```

7. **Push the new branch to Remote:**
   ```bash
   git push -u origin collab-br2
   ```

## Stash-checkout-checkin-pop 

### Admin

8. **Update but not commit:**
   
   - Update `demo.txt`: Add “Input 2 to main by admin, to be stashed once”

9. **Checkout a remote branch**
   - Fetch latest changes:
   ```bash
   git fetch
   git branch -r 
   git log --online --all 
   ```
   - Copy the hash of the commit you want to checkout to 
     
   ```bash
   git checkout <commit hash>
   ```
    ❓ You see an error, do you know why?   
   - Take a look at the content of `demo.txt` keep track of its last sentence.
   - Stash changes and now checkout the branch:
   ```bash
   git stash 
   git checkout origin/collab-br2
   ```
    ❓ Take a look at the content of `demo.txt` do you see the content of the last commit by te collaborator from step 6? 

10. **Retrieve stashed Work after "checkin":**
    - Switch back to your branch:
    ```bash
    git switch - 
    ```
   
    - Take a look at the content of `demo.txt` keep track of its last sentence.
    ```bash
    git stash pop 
    ```
    ❓ Take a look at the content of `demo.txt`, do you see your latest edition from step 8? 

11. **Update and commit to main:**
    - Open `demo.txt` and add this sentence: “Continue with input 2 to main by admin, collaborator needs to integrate this before going forward”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 2 to main by admin"
    ```

12. **Push changes to remote:**
    ```bash
    git push
    ```

## Merge from main

### Collaborator

13. **Update and merge main branch:**
    ```bash
    git switch main
    git fetch
    git status
    git pull 
    git switch collab-br2
    git merge main 
    ```

14. **Resolve conflicts and continue:**
    - Resolve by accepting both versions.
    - Add and commit:
    ```bash
    git add . 
    git commit -m "conflict 1 resolved to collab-br by collab"
    ```
    ❓ Is it a good practice to merge from main to your branch? Why?   
15. **Further Update and commit to branch:**
    - Open `demo.txt` and add: “Input 2 to collab-br2 by collaborator, development continues after integrating latest version of main”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 2 to collab-br2 by collaborator"
    ```
## Admin

16. **Update and commit to main:**
    - Open `demo.txt` and add: “Input 3 to main by admin, to be integrated by collaborator before any pull request”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 3 to main by admin"
    ```

17. **Push changes to remote:**
    ```bash
    git push
    ```

## Pull request - after conflicts resolved

### Collaborator

18. **Merge main into branch and resolved the conflict**
    ```bash
    git switch main
    git fetch
    git status
    git pull 
    git switch collab-br2
    git merge main 
    ```
    - Resolve conflicts in `demo.txt` and save the file.
   ❓ Is it a good practice to merge from main to your branch before pull request? Why?
19. **Commit and push:**
      - Add and commit:
      ```bash
      git add . 
      git commit -m "conflict 2 resolved to collab-br by collab, merging main into collab-br2 before pull request"
      ```
     - Push changes:
     ```bash
     git push
     ```

20. **Initiate a pull request on GitHub:**
   - Send a pull request to merge `collab-br2` into `main`.

### Admin

21. **Review and pull request:**
    - Check pull request on GitHub.
    - Optionally, fetch and checkout branch before accepting:
    ```bash
    git fetch
    git switch collab-br2
    ```

22. **Accept the pull request and pull locally**
    - Follow GitHub instructions to accept the changes.
    ❓ Was there any conflict? Why yes or not? 
    - Pull latest changes locally:
    ```bash
    git switch main
    git fetch
    git status
    git pull
    ```

23. **Update and commit to main:**
    - Open `demo.txt` and add: “Input 4 to main by admin, to be ignored by collaborator before a pull request”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 4 to main by admin"
    ```
24. **Push Changes to Remote:**
    ```bash
    git push
    ```

## Pull request - without conflicts resolved

### Collaborator

25. **Update and commit to the branch:**
    - Make sure you are in your branch 
    ```bash 
    git switch collab-br2
    ```
    - Open `demo.txt` and add: “Input 3 to collab-br2 by collaborator, development continues regardless of the main’s status”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 3 to collab-br2 by collaborator"
    ```

26. **Push changes:**
    ```bash
    git push
    ```

27. **Initiate a pull request on GitHub:**
    - Send a pull request to merge `collab-br2` into `main`.

## Admin

28. **Resolve conflicts on GitHub:**
    ❓ What is the difference between this and the previous pull request?
     - Check the pull request and follow the instructions to resolve conflict on GitHub.

     ❓ Do you know where you resolved the conflict?    

29. **Pull Latest Changes Locally:**
    ```bash
    git fetch
    git status
    git pull
    ```

30. **Update and commit to main:**
   - Open `demo.txt` and add: “Input 5 to main by admin, to be ruined by collaborator without a pull request”
   - Add and commit:
     ```bash
     git add . 
     git commit -m "commit 5 to main by admin"
     ```

31. **Push changes to remote:**
    ```bash
    git push
    ```

## Merge to main without pull request

### Collaborator

32. **Get the latest version of main and the branch from GitHub:**
    ```bash
    git switch main
    git fetch
    git status
    git pull 
    git switch collab-br2
    git status
    git pull
    ```
    ❓ Did you have any update into your branch? Why? 

33. **Update and commit to the branch:**
    - Open `demo.txt` and add: “Input 4 to collab-br2 by collaborator, this is going to make a mess in the main branch by merge”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 4 to collab-br2 by collaborator"
    ```

34. **Merge Collab Branch to Main:**
    - Switch and merge:
    ```bash
    git switch main
    git merge collab-br2
    ```
    - Resolve conflicts by accepting incoming changes.

35. **Commit and Push:**
   
   - Add and commit:
     ```bash
     git add .
     git commit -m "conflict 3 resolved in main, resulted in collapse of main"
     ```
   - Push final changes:
     ```bash
     git push 
     ```
     - Check the content of the `demo.text` on GitHub. 

     ❓ What happened to the content that admin added in step 30? 

     ❓ Is it a good practice to merge to main without pull request 

     ❓ Do you have any solution for fix this? 

### [Back to Table of Contents](./README.md)
