### [Back to first page](./README.md)

## Part 4: Multi-branch collaborative development, best practices

## Table of Contents

- [Stash-checkout-switch-pop ](#stash-checkout-switch-pop)
- [Merge from MAIN](#merge-from-main)
- [Pull request - after conflicts resolved](#pull-request---after-conflicts-resolved)
- [Pull request - without conflicts resolved](#pull-request---without-conflicts-resolved)
- [Merge to MAIN without pull request](#merge-to-main-without-pull-request)

---

## Collaborator

1. **Ensure latest version of remote repo:**
   ```bash
   git fetch 
   git status 
   git pull 
   ```

2. **Switch to a collab-br, update, commit and push:**
   
   ```bash
   git switch collab-br
   ```
   - Open `demo.txt` and add this sentence: “Input 4 to collab-br by collaborator, admin should take a look at this before going ahead”
   - Add and commit:
   ```bash
   git add . 
   git commit -m "Commit 4 to collab-br by collaborator"
   git push 
   ```
   
   ```
## Admin 

## Stash-checkout-switch-pop 


3. **Update but not commit:**
   
   - Update `demo.txt`: Add “Input 4 to main by admin. In the middle of his work, admin is asked ot check latest version of collab-br. Admin's current changes need to be stashed once.”

4. **Checkout a remote branch**
   - Fetch latest changes:
   ```bash
   git fetch
   git branch -r 
   git log --oneline --all 
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
   git checkout <commit hash>
   ```
    ❓ Take a look at the content of `demo.txt` do you see what collaborator wanted you to check (Input 4 to collab-br by collaborator)? 

5. **Retrieve stashed Work after switching back:**
    - Switch back to your branch:
    ```bash
    git switch - 
    ```
   
    - Take a look at the content of `demo.txt` keep track of its last sentence.
    ```bash
    git stash pop 
    ```
    ❓ Take a look at the content of `demo.txt`, do you see your work from before stash (Input 4 to main by admin)? 

6. **Update, commit to main and push:**
    - Open `demo.txt` and add this sentence: “Continue input 4 to main by admin, the sentence above was popped from the work before stash. Collaborator needs to integrate this before going forward, and merging back to main.”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 4 to main by admin"
    git push
    ```

## Collaborator

## Merge from MAIN

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
    ❓ Is it a good practice to merge from main to your branch? Why?   
9. **Further Update, commit and push to branch:**
    - Open `demo.txt` and add: “Input 5 to collab-br by collaborator, development continues after integrating latest version of main, then it will merged to main”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 5 to collab-br by collaborator"
    ```
10. **Switch to main and get the latest updates:** 
    ``` bash 
    git switch main 
    git fetch 
    git pull # if needed
    ```
    ❓ Is it a safe to merge to main now? After you updated collab-br again? 

11. **Merge collab-br into main:**
    ```bash
    git merge collab-br
    ```
    ❓ Is there any conflict? why or why not? 
    ❓ Is there any better practice? 


## Admin

12. **Update and commit to main:**
    - Open `demo.txt` and add: “Input 5 to main by admin, to be integrated by collaborator before any pull request - rebase the feature branch with this one.”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 5 to main by admin"
    git push 
    ```

## Collaborator

## Pull request - after conflicts resolved

13. **Switch to collbar-br, Update, Commit and push:**
    ```bash
    git switch collab-br
    ```
    - Open `demo.txt` and add this sentence: “Input 6 to collab-br by collaborator - this is going to rebased by another commit from main”

    - Add and commit:
    ```bash
    git add . 
    git commit -m "Commit 6 to collab-br by collaborator"
    ```

14. **Rebase the feature branch with main**
    - Check the Git Graph first 
    - Switch to collab-br and rebase the branch with main 
    ```bash
    git log --oneline --all 
    git switch collab-br
    git rebase main
    git log --oneline --all
    ``` 
    - Resolve the conflict by accepting both versions.
    ❓ Do you still need to commit and push? 
    - Add and commit:
    ```bash
    git add . 
    git commit -m "conflict 2 resolved to collab-br by collab"
    git push
    - Check the Git Graph again 
    ❓ what is the difference between merge from step 7 and rebase? 



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
    - Follow GitHub instructions to accept the changes.
    ❓ Was there any conflict? Why yes or not? 
    - Pull latest changes locally:
    ```bash
    git switch main
    git fetch
    git status
    git pull
    ```

18. **Update and commit to main:**
    - Open `demo.txt` and add: “Input 6 to main by admin, to be ignored by collaborator before a pull request. If you don't resolve you conflict, other might.”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 6 to main by admin"
    ```
19. **Push Changes to Remote:**
    ```bash
    git push
    ```

## Collaborator

## Pull request - without conflicts resolved


20. **Update and commit to the branch:**
    - Make sure you are in your branch 
    ```bash 
    git switch collab-br
    ```
    - Open `demo.txt` and add: “Input 7 to collab-br by collaborator, development continues regardless of the main’s status.”
    - Add and commit:
    ```bash
    git add . 
    git commit -m "commit 7 to collab-br by collaborator"
    ```

21. **Push changes:**
    ```bash
    git push
    ```

22. **Initiate a pull request on GitHub:**
    - Send a pull request to merge `collab-br` into `main`.

## Admin

23. **Resolve conflicts on GitHub:**

     ❓ What is the difference between this and the previous pull request?

     - Check the pull request and follow the instructions to resolve conflict on GitHub.

     ❓ Do you know where you resolved the conflict?    

24. **Pull Latest Changes Locally:**
    ```bash
    git fetch
    git status
    git pull
    ```

## Collaborator

25. **Get the latest changes**

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
    ❓ Did your input 7 (from step 20) get integrate into the main? 
    ❓ Do you see input 7 in your branch? What happened?    

### [Back to first page](./README.md)
