
### [Back to first page](./README.md)
## Part 1: Git-GitHub Connection and Basic Commands

## Table of contents

  - [Introduce yourself to Git](#introduce-yourself-to-git)
  - [Establish the Git-GitHub connection - Clone](#establish-the-git-github-connection---clone)
  - [Commit / Push / Pull](#commit--push--pull)
  - [Use RStudio VS Code or any other IDE](#use-rstudio--vs-code--any-other-ide)
  - [Going back to history](#going-back-to-history)

---


## Introduce yourself to Git

1. **Configuring Name and Email:** 
   ```bash
   git config --global user.name "<YOUR FULL NAME>"
   git config --global user.email "<YOUR EMAIL ADDRESS>"
   ```

   - If you are using vscode, make it the default code editor for git 
   ```bash 
   git config --global core.editor "code --wait"
   ```
   - If you are not using vscode, make nano the default code editor for git 

   ```bash 
   git config --global core.editor "nano"
   ```

2. **Check Configuration:**
   ```bash
   git config --global --list
   git config --global core.editor
   ```

## Establish the Git-GitHub connection - Clone

3. **Create a repo on GitHub** 
   - Create a **private** repo **with README** on GitHub and name it "vc-demo-basic" and stay logged in.

4. **Copy the HTTPS link**

   - Click on “code” and copy the “https” link.

5. **Clone the repo** 

   - Change into a directory where you want to clone the repo and clone:
   ```bash
   cd <selected directory>
   git clone <https of repo on github from step 4>
   ```

6. **Figure Out if authentication is needed:**
   - **Authentication exits**
     - If authentication is previously done, the cloning takes place successfully, jump to step [9](#commitpushpull)
   - **Authentication does not exist**
     - If the cloning did not take place and you get authentication error, proceed forward for different operating systems. 
   - **For Linux and Mac:**
     - If prompted for GitHub username and password, do not enter your username and password directly; you need to create a Personal Access Token (PAT).

   - **For Windows:**
     - Follow the browser login prompt to authenticate your GitHub credentials for Git. If it fails, proceed with creating a PAT.

7. **Creating a Personal Access Token (PAT)**:

   - On GitHub, navigate to `GitHub > Settings > Developer Settings > Personal Access Token > Tokens (classic) > Generate New Token (classic)`. Select:
     - `Repo`git 
     - `Workflow`
     - `User`

   - Generate a new PAT, copy, and paste it somewhere safe. You will not be able to see this after you refresh the page. 

8. **Use the PAT for Git authentication:**

   - When prompted asking for GitHub username, enter your GitHub username.

   - When prompted for GitHub password, paste the PAT instead of your GitHub password.

   - In this stage the repo should be cloned successfully

   - After this step Git should remember the GitHib credentials until the PAT is expired. Otherwise read more on https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git?platform=linux
   
   - If you are asked to authenticate when you push and not when you cloned, check if you repo is made private.
   
   - If git does not remember the authentication and asks for it every time, run
   
   ``` bash
    git config --show-origin --get-all credential.helper 
   ``` 
   
   - If no credential helper shows up run: 

   Windows (recommended)
   ```bash 
    git config --global credential.helper manager
   ```
    macOS
   ```bash 
    git config --global credential.helper osxkeychain
   ```
    Linux (easy but less secure)
   
   ```bash 
    git config --global credential.helper store
   ```
 
   Linux (better: cache in memory for a while)
   
   ```bash 
   git config --global credential.helper 'cache --timeout=3600'
   ```

## Commit / Push / Pull

9. **Verify the clone** 

   - After successful authentication, your repo should be cloned. 
   - Change into the repo directory and inspect the cloned files:
    ```bash
    cd <repo-name>
    ls
    ```

10. **Check the connection and status :**
    ```bash
    git remote show origin
    git status
    ```

    ❓1. Can you see the connection between remote and local branch? 

11. **Modify README and push back to GitHub:**

    - Edit README file and add: “Input from local repo to be pushed to remote repo.”
    - Use the following commands to commit and push the changes to GitHub:

    ```bash
    git status 
    git add README.md
    git status 
    git commit -m "Testing connection"
    git status 
    git push origin main 
    git status
    ```

    ❓ 2. Do you know what "your branch" and "origin/main" are referring to in the git status response? 

12. **Refresh GitHub to confirm changes.**

13. **Edit on GitHub and pull changes:**

    - On GitHub, edit README to add: "Input from remote repo to be pulled to local repo."
    - Commit message: “Connecting from GitHub”
    - Pull the changes on the command line:
    ```bash
    git status 
    git fetch origin main
    git status 
    git pull origin main
    git status
    ```
    ❓ 3. What is the difference between fetch and pull? 

14. **Check Commit Logs:**
    ```bash
    git log 
    git log --oneline
    ```

## Use RStudio / VS Code / any other IDE

15. **Start fresh in the IDE**

    - Delete the local repo cloned in Step 5.

16. **Clone using the IDE**

    - In RStudio: Go to `File > New Project > Version Control > Git`, paste the repo URL, choose a directory and create the project.
    - In VS Code:  `ctrl+shift+p >Clone > Clone from GitHub`, paste the repo URL and hit enter, navigate to the folder you want the repository to clone in  
    - Verify the clone (check if the file are there)

17. **Edit in IDE and push changes:**

    - Using IDE edit README to add: “Input from local repo to be pushed to remote repo using RStudio/VS code.”
    - Commit message: “Commit from IDE”
    - Add, commit, and push changes using the IDE.
    - Check the Git Graph 
    - Check the README content in the dual view

18. **Edit on GitHub and pull changes using IDE:**

    - On GitHub, edit README to add: "Input from remote repo to be pulled to local repo using IDE."
    - Commit message: “Editing from GitHub”
    - Fetch and pull the latest changes from GitHub using the IDE 

    ❓ 4. Can you fetch only using RStudio's Git interface? 

19. **Review commit history in IDE:**
    - In RSTudio: use git history 
    - In VS Code: use git graph 

## Going back to history

20. **Commit to be amended** 

    - Add another line to README file: “Input from local repo to be amended, the content is the same, only commit message is amended.”
    - Commit with:
    ```bash
    git commit -a -m "to be amended"
    ```
    - Look at the commit log 
     ```bash
    git log --oneline
    ```


21. **Amend a Commit:**
    ```bash
    git commit --amend 
    ```
    - Inside the code editor prompt insert this sentence as the new commit message: "It is amended now" save and close the file. 

    - Look at the commit log 
     ```bash
    git log --oneline
    ```

    ❓5. Compare the output of the two last git logs, has the commit message been amended? 

    ❓6. What happens if you already have pushed the commit and now you want to amend it? 

    ❓7. Can you force push the change to the remote branch? When should you avoid it? 

    ❓8. What is the difference between git push --force and git push --force-with-lease? 


22. **Commit to be uncommitted** 

    - Add another line to README file: “Input from local repo to be committed and uncommitted, the content is the same, only the commit is reversed.”
    - Commit with:
    ```bash
    git commit -a -m "to be uncommitted"
    ```
    - Look at the commit log 
     ```bash
    git log --oneline
    ```

23. **Un-commit a Commit:**
    ```bash
    git reset HEAD~1
    ```
    - Look at the commit log 
     ```bash
    git log --oneline
    ```
    ❓ 9. Has the last commit disappeared? 

    ❓ 10. Check the content of the README file, has the content changed as a result of last operation?  


24. **Commit to be reversed:**
    - Look at the Git status    
    ```bash
    git status
    ```

    ❓ 11. You see uncommitted changes, can you verify what changes are to be committed? Aren't these the changes that were left as a result of the previous uncommit action? 

    - commit: 
    ```bash
    git commit -a -m "to be reversed both the commit and content"
    ```
    - Look at the commit log 
     ```bash
    git log --oneline
    ```

25. **Reverse a commit:**
    - Now, we want to reverse the commit and the content. 

    ```bash
    git reset --hard HEAD~1
    ```
     - Look at the commit log 
     ```bash
    git log --oneline
    ```
    ❓12. Has the last commit disappeared? 


    ❓13. Check the content of the README file, can you explain what happened to the latest changes you committed in step 23? 


    ❓14. What happens if you already have pushed the commit?


    ❓15. Is there a better approach to reversing the history if the commit is already pushed to a share branch? 



26. **Commit to be reverted:**
    
    - Add another line to the README file: “Input from local repo to be reverted. The content will be gone but the commit stays in the history”
    - Commit with:
    ```bash
    git commit -a -m "to be reverted"
    ```
    - Look at the commit log 
     ```bash
    git log --oneline
    ```

27. **Revert a Commit:**
    - Copy the commit hash of the commit you want to revert from previous step
    - Revert by running this and pasting the commit hash: 
    ```bash
        git revert <commit hash>
    ```
    - This will be a new commit, save and close the commit prompt to complete the revert.

28. **Verify the revert** 
    - Look at the commit log 
     ```bash
    git log --oneline
    ```
    
    ❓16. Has the last commit disappeared? 


    ❓17. Check the content of the README file, can you explain what happened to the latest changes you committed in step 26? 
  
29. **Reflect**

    ❓18. Can you imagine different scenarios where "amend", "un-commit", "reverse" or "revert" can be used? 

### [Back to first page](./README.md)


