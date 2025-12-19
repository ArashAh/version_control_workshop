### [Back to first page](./README.md)

## Part 4: Multi-branch collaborative development, best practices

## Table of Contents

- [Stash-checkout-switch-pop](#stash-checkout-switch-pop)
- [Merge from MAIN - merge back to MAIN](#merge-from-main---merge-back-to-main)
- [Merge from MAIN - pull request](#merge-from-main---pull-request)
- [Rebase from MAIN - pull request](#rebase-from-main---pull-request)
- [Pull request - without conflicts resolved](#pull-request---without-conflicts-resolved)

---

## Collaborator

1. **Ensure latest version of remote repo:**
   ```bash
   git fetch 
   git status 
   git pull # if needed
   ```

2. **Switch to a collab-br, update, commit and push:**
   
   ```bash
   git switch collab-br
   ```
   - Open `demo.txt` and add this sentence: "Input 4 to collab-br by collaborator, admin should take a look at this before going ahead"
   - Add, commit and push:
   ```bash
   git add . 
   git commit -m "Commit 4 to collab-br by collaborator"
   git push 
   ```

## Admin 

## Stash-checkout-switch-pop 


3. **Update but not commit:**
   
    - Update `demo.txt`: Add "Input 4 to main by admin. In the middle of his work, admin is asked to check latest version of collab-br. Admin's current changes need to be stashed once."

4. **Checkout a commit in the remote branch**
   - Fetch latest changes, get a list of remote branches and see a log of all commits:
   ```bash
   git fetch
   git branch -r 
   git log --oneline --all 
   ```
   - Copy the hash of the last commit in the collab-br 
     
   ```bash
   git checkout <commit hash>
   ```
   ❓1. You see an error, do you know why?  

   - Take a look at the content of `demo.txt` keep track of its last sentence.
   - Stash changes and now checkout the branch:
   
   ```bash
   git stash 
   ```
   ❓2. Take a look at the content of `demo.txt`, what did stash do to the content?  
   ```bash
   git checkout <commit hash>
   ```
   ❓3. Take a look at the content of `demo.txt` do you see what collaborator wanted you to check (Input 4 to collab-br by collaborator, admin should take a look at this before going ahead)? 

5. **Retrieve stashed Work after switching back:**
    - Switch back to your branch:
    ```bash
    git switch - 
    ```
   
    - Take a look at the content of `demo.txt`, keep track of its last sentence.
    ```bash
    git stash pop 
    ```
    ❓4. Take a look at the content of `demo.txt`, do you see your work from before stash (Input 4 to main by admin)? 

6. **Update, commit to main and push:**
    - Open `demo.txt` and add this sentence: "Continue input 4 to main by admin, the sentence above was popped from the work before stash. Collaborator needs to integrate this before going forward and merging back to main."
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 4 to main by admin"
    git push
    ```

## Collaborator

## Merge from MAIN - merge back to MAIN

7. **Merge from main branch:**
    ```bash
    git switch main
    git fetch
    git status
    git pull 
    git switch collab-br
    git merge main 
    ```
    

8. **Resolve conflicts and continue:**
    - Resolve by accepting both versions.
    - Add and commit:
    ```bash
    git add . 
    git commit -m "conflict 1 resolved to collab-br by collab"
    ```

    ❓5. Is it a good practice to merge from main to your branch? Why?   

9. **Further Update, commit and push to branch:**
    - Open `demo.txt` and add: "Input 5 to collab-br by collaborator, development continues after integrating latest version of main, then it will be merged to main"
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 5 to collab-br by collaborator"
    ```
10. **Switch to main and get the latest updates:** 
    ```bash
    git switch main 
    git fetch 
    git status
    ```
    ❓6. Is it safe to merge to main now, after you updated collab-br again? 

11. **Merge collab-br into main:**
    ```bash
    git merge collab-br
    ```
    ❓7. Is there any conflict? Why or why not? 

    ❓8. What happens if main branch is shared or owned by others? Is there a better practice? 

    ```bash
    git push 
    ``` 
    ❓9. Didn't you need to add and commit after merge this time? Why not? 

---

## Merge from Main - pull request 

## Admin

12. **Update and commit to main:**
    - Get the latest version of main 
    ```bash
    git switch main # if needed
    git fetch 
    git status 
    git pull 
    ```

    - Open `demo.txt` and add: "Input 5 to main by admin, to be integrated by collaborator before any pull request - merge this one into the feature branch."
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 5 to main by admin"
    git push 
    ```

## Collaborator

13. **Switch to collab-br, update, commit and push:**
    ```bash
    git switch collab-br
    ```
    - Open `demo.txt` and add this sentence: "Input 6 to collab-br by collaborator - this is going to be merged with another commit from main"

    - Add and commit:
    ```bash
    git add . 
    git commit -m "Commit 6 to collab-br by collaborator"
    git push
    ```

14. **Merge the feature branch with main**
    - Get the latest version of main 
    ```bash
    git switch main
    git pull
    ```
    - Check the Git Graph first 
    - Switch to collab-br and merge main into it 
    ```bash
    git switch collab-br
    git merge main
    ```
    - Resolve the conflict by accepting both versions and save.
    ```bash
    git add .
    git commit # keep the default merge commit message
    git push
    ```
    ❓10. Did you see an error or conflict with `git push`? Why or why not?

15. **Initiate a pull request on GitHub:**
    - Send a pull request to merge `collab-br` into `main`.

## Admin

16. **Review and pull request:**
    - Check pull request on GitHub.
    - Optionally, fetch and checkout branch before accepting:
    ```bash
    git fetch
    git switch collab-br
    ```

17. **Accept the pull request and pull locally**
    - Follow GitHub instructions to accept the changes. Ask for help if in doubt. 

    ❓11. Was there any conflict? Why yes or why not?
    
    - Pull latest changes locally:
    ```bash
    git switch main
    git fetch
    git status
    git pull
    ```
    ❓12. What is the point of updating main? Can't we just merge from `origin/main`? 


18. **Update and commit to main:**
    - Get the latest version of main 
    ```bash
    git fetch 
    git status 
    git pull 
    ```

    - Open `demo.txt` and add: "Input 6 to main by admin, to be integrated by collaborator before any pull request - rebase the feature branch with this one."
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 6 to main by admin"
    git push 
    ```

## Collaborator

## Rebase from Main - pull request

19. **Switch to collab-br, Update, Commit and push:**
    ```bash
    git switch collab-br
    ```
    - Open `demo.txt` and add this sentence: "Input 7 to collab-br by collaborator - this is going to be rebased by another commit from main"

    - Add and commit:
    ```bash
    git add . 
    git commit -m "Commit 7 to collab-br by collaborator"
    ```

20. **Rebase the feature branch with main**
    - Get the latest version of main 
    ```bash
    git switch main
    git pull
    ```
    - Check the Git Graph first 
    - **Switch** to collab-br and rebase the branch with main 
    ```bash
    git switch collab-br
    git rebase main
    ``` 
    - Resolve the conflict by accepting both versions and save. 
    ```bash
    git add . 
    git rebase --continue # do not change the original commit message 
    git push 
    ```
    ❓13. Did `git push` fail? Do you know why? 
    - Check the content of `demo.txt` on collab-br and the history of commits on GitHub, take a screenshot 

    - force push after rebase 

    ```bash
    git push --force # to be safer you can use --force-with-lease
    ``` 

    ❓14. Check the content of `demo.txt` on collab-br and history of commits on GitHub again, can you explain how rebase changed the things there? 

    ❓15. Check the Git Graph again, what is the difference between merge (step 14) and rebase (step 20)? 


21. **Initiate a pull request on GitHub:**
    - Send a pull request to merge `collab-br` into `main`.

## Admin

22. **Review and pull request:**
    - Check pull request on GitHub.
    - Optionally, fetch and checkout branch before accepting:
    ```bash
    git fetch
    git switch collab-br
    ```

23. **Accept the pull request and pull locally**
    - Follow GitHub instructions to accept the changes.

    
    - Pull latest changes locally:
    ```bash
    git switch main
    git fetch
    git status
    git pull
    ```
    ❓16. Can you pinpoint the similarities and differences of rebase and merge when it comes to the outcome of the pull request? 


24. **Update, add, commit and push to main:**
    - Open `demo.txt` and add: "Input 7 to main by admin, to be ignored by collaborator before a pull request. If you don't resolve your conflicts, others might."
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 7 to main by admin"
    git push
    ```

## Collaborator

## Pull request - without conflicts resolved


25. **Update and commit to the branch:**
    - Make sure you are in your branch 
    ```bash
    git switch collab-br
    ```
    - Open `demo.txt` and add: "Input 8 to collab-br by collaborator, development continues regardless of the main's status."
    
    - Add, commit and push:
    ```bash
    git add . 
    git commit -m "commit 8 to collab-br by collaborator"
    git push
    ```

26. **Initiate a pull request on GitHub:**
    - Send a pull request to merge `collab-br` into `main`.

## Admin

27. **Resolve conflicts on GitHub:**

    ❓17. What is the difference between this and the previous pull request?

     - Check the pull request and follow the instructions to resolve the conflict on GitHub.

    ❓18. Do you know where you resolved the conflict? Why?     

28. **Pull Latest Changes Locally:**
    ```bash
    git fetch
    git status
    git pull
    ```

## Collaborator

29. **Get the latest changes**

    ```bash
    git switch main
    git fetch
    git status
    git pull
    git switch collab-br
    git fetch
    git status
    git pull
    ```
    
    ❓19. Did your Input 8 to collab-br by collaborator (from step 25) get integrated into main? 

    ❓20. Do you see Input 8 to collab-br by collaborator in your branch? What happened?    

    ❓21. Is there a scenario where sending a pull request without resolving the conflict makes sense? Or a scenario where it can be problematic? 

### [Back to first page](./README.md)
