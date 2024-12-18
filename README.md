# Version Control Workshop Materials

Welcome to the workshop materials page. This workshop is divided into four main parts. Each part contains several topics with explanations and command-line operations.

## Table of Contents

- [Part 1: Git-GitHub Connection and Basic Commands](#part-1-git-github-connection-and-basic-commands)
  - [Introduce Yourself to Git](#introduce-yourself-to-git)
  - [Establish the Git-GitHub Connection - Clone](#establish-the-git-github-connection---clone)
  - [Commit/Push/Pull](#commitpushpull)
  - [Use RStudio (VS Code or Any Other Code Editor)](#use-rstudio-vs-code-or-any-other-code-editor)
  - [Going Back to History](#going-back-to-history)

---

## Part 1: Git-GitHub Connection and Basic Commands

### Introduce Yourself to Git

1. **Configuring Name and Email:**
   ```bash
   git config --global user.name "<YOUR FULL NAME>"
   git config --global user.email "<YOUR EMAIL ADDRESS>"
   ```

2. **Check Configuration:**
   ```bash
   git config --global --list
   ```

### Establish the Git-GitHub Connection - Clone

3. **Create a repo on GitHub** 

    Create a private repo with README on GitHub and stay logged in.

4. **Copy the HTTPS link**

    Click on “code” and copy the “https” link.

5. **Clone the repo** 

    Change into a directory where you want to clone the repo and clone:
   ```bash
   cd <selected directory>
   git clone <https of repo on github from step 4>
   ```

6. **Figure Out if Authentication is Needed:**
   - **Authentication exits**
     - If authentication is previously done, the cloning takes place successfully, jump to step [9](#commitpushpull)
   - **Authentication does not exist**
     - If the cloning did not take place and you get authentication error follow along. 
   - **For Linux and Mac:**
     - If prompted, do not enter your username and password directly; you need to create a Personal Access Token (PAT).

   - **For Windows:**
     - Follow the browser login prompt to authenticate your GitHub credentials for Git. If it fails, proceed with creating a PAT.

7. **Creating a Personal Access Token (PAT)**:

   On GitHub, navigate to `GitHub > Settings > Developer Settings > Personal Access Token > Generate New Token`. Select:
   - `Repo`
   - `Workflow`
   - `User`

    Generate a new PAT, copy, and paste it somewhere safe. You will not be able to see this after you refresh the page. 

8. Use the PAT for Git Authentication:

   When prompted, enter your GitHub username.

   Paste the PAT instead of your GitHub password.

   In this stage the repo should be cloned successfully

   After this step Git should remember the GitHib credentials until the PAT is expired. Otherwise read more on https://docs.github.com/en/get-started/getting-started-with-git/caching-your-github-credentials-in-git?platform=linux


### Commit/Push/Pull

9. **Verify the clone** 

    After successful authentication, your repo should be cloned. Change into the repo directory and inspect the cloned files:
    ```bash
    cd <repo-name>
    ls
    ```

10. **Check the Connection Status:**
    ```bash
    git remote show origin
    ```

11. **Modify README and Sync with GitHub:**

    - Edit README file and add: “Input from local repo to be pushed to remote repo.”
    - Use the following commands:
      ```bash
      git status 
      git add README.md
      git status 
      git commit -m "Testing connection"
      git status 
      git push origin main 
      git status
      ```

12. **Refresh GitHub to confirm changes.**

13. **Edit on GitHub and pull changes:**

    - On GitHub, edit README to add: "Input from remote repo to be pulled to local repo."
    - Commit message: “Connecting from GitHub.”
    - On the command line:
    ```bash
    git status 
    git fetch origin main
    git status 
    git pull origin main
    ```

14. **Check Commit Logs:**
    ```bash
    git log 
    git log --oneline
    ```

### Use RStudio, VS Code or Any Other Code Editor

15. **Start fresh in the IDE**

    Delete the local repo cloned in Step 5.

16. **Clone using the IDE**

    - In RStudio: Go to File > New Project > Version Control > Git, paste the repo URL and create the project.
    - In VS Code: cnrtl+shift+p > Clone from GitHub, paste the repo URL and hit enter 
    - Verify the clone


17. **Edit in IDE and push changes:**

    - Using IDE edit README to add: “Input from local repo to be pushed to remote repo using RStudio/VS code.”
    - Commit message: “Commit from IDE.”
    - Add, commit, and push changes using the IDE.

18. **Edit on GitHub and pull changes using IDE:**

    - On GitHub, edit README to add: "Input from remote repo to be pulled to local repo using IDE."
    - Commit message: “Editing from GitHub.”
    - Fetch and pull the latest changes from github using RStudio 

19. **Review commit history in IDE:**
    - In RSTudio: use git history 
    - In VS Code: use git graph 

### Going Back to History

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
    - Modify the commit message to "Commit amended now" and save.

    - Look at the commit log 
     ```bash
    git log --oneline
    ```

22. **Commit to be uncommitted** 

    - Add another line to README file: “Input from local repo to be commited and uncommited, the content is the same, only the commit is reversed.”
    - Commit with:
    ```bash
    git commit -a -m "to be uncommited"
    ```
    - Look at the commit log 
     ```bash
    git log --oneline
    ```




22. **Uncommit a Commit:**
    ```bash
    git reset HEAD~1
    ```
    - Look at the commit log 
     ```bash
    git log --oneline
    ```
    - Check the content of the README file, you should still see this sentence: “Input from local repo to be commited and uncommited, the content is the same, only the commit is reversed.” 

23. **Commit to be reversed:**
    ```bash
    git commit -a -m "to be reversed both the commit and content"
    ```
    - Look at the commit log 
     ```bash
    git log --oneline
    ```

24. **Reverse a commit:**
    ```bash
    git reset --hard HEAD~1
    ```
     - Look at the commit log 
     ```bash
    git log --oneline
    ```
    - Check the content of the README file, you should not see this sentence anymore: “Input from local repo to be commited and uncommited, the content is the same, only the commit is reversed.” 

25. **Commit to be reverted:**
    
    - Add another line to the README file: “Input from local repo to be reverted. The content will be gone but the commit stays in the history”
    - Commit with:
    ```bash
    git commit -a -m "to be reverted"
    ```
    - Look at the commit log 
     ```bash
    git log --oneline
    ```

26. **Revert a Commit:**
    - Copy the commit hash of the commit you want to revert 
    ```bash
    git log --oneline 
    git revert <commit hash>
    ```
    - This changes the file content to the commit before the referred commit hash but does not remove the commit, instead it makes a new commit to show the reversion

33. Save and close the commit prompt to complete the revert.
    - Look at the commit log 
     ```bash
    git log --oneline
    ```
    - Check the content of the README file, you should not see this sentence anymore: "Add another line to the README file: “Input from local repo to be reverted. The content will be gone but the commit stays in the history"
---


