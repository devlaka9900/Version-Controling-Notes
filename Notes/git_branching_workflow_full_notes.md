# Git Branching Workflow and Pull Requests - Full Notes

## 1. Introduction

In software development, teams often need to work on different changes at the same time. One developer may be adding a new feature, another may be fixing a bug, and another may be updating documentation.

If everyone works directly on the `main` branch, the project can become messy and risky. A mistake can affect the main code immediately.

To avoid this, developers use branches.

A branch is a separate version of the project where you can safely make changes without affecting the main branch. After the work is complete, the branch can be reviewed and merged back into `main` using a pull request.

---

## 2. Main Idea of This Lesson

This lesson explains a common Git and GitHub workflow:

1. Check your current directory.
2. Check the Git status.
3. Create a new branch.
4. Add or change files in that branch.
5. Commit the changes.
6. Push the branch to GitHub.
7. Create a pull request.
8. Review and merge the pull request.
9. Pull the latest changes back into your local `main` branch.

This is a very common workflow when collaborating with other developers.

---

## 3. Important Terms

| Term | Simple Meaning |
|---|---|
| `repository` | A project folder tracked by Git. |
| `main branch` | The main version of the project. |
| `branch` | A separate working copy of the project. |
| `feature branch` | A branch created for a new feature or change. |
| `commit` | A saved snapshot of your changes. |
| `remote repository` | A repository stored online, such as on GitHub. |
| `origin` | The default name Git gives to the remote repository. |
| `push` | Send local commits to the remote repository. |
| `pull` | Download and apply changes from the remote repository. |
| `pull request` | A request to review and merge changes from one branch into another. |
| `merge` | Combine changes from one branch into another branch. |

---

## 4. Checking the Current Directory

Before making changes, it is good practice to check where you are in the terminal.

Use the `pwd` command.

```bash
pwd                         # Print the current working directory.
```

Example output:

```bash
/home/user/my-first-repo     # Shows that you are inside the my-first-repo directory.
```

This confirms that you are inside the correct project folder.

---

## 5. Checking Git Status

Before creating a new branch, check whether the working directory is clean.

```bash
git status                  # Show the current Git status of the repository.
```

If everything is clean, Git may show something like:

```bash
On branch main              # Shows that you are currently on the main branch.
Your branch is up to date   # Shows that local main matches the remote main branch.
nothing to commit           # Shows there are no uncommitted changes.
```

This is important because you usually want to start a new branch from a clean and updated `main` branch.

---

## 6. Creating a New Branch

A branch allows you to work separately from the `main` branch.

In the transcript, the branch name is:

```bash
feature/lesson              # Example branch name used for a lesson feature.
```

The word `feature` tells the team that this branch is for a new feature or new work.

The slash `/` helps organize branch names.

---

## 7. Method 1: Create and Switch to a Branch

The command below creates a new branch and immediately moves you into it.

```bash
git checkout -b feature/lesson      # Create a new branch and switch to it immediately.
```

This is useful because it performs two actions in one command:

1. Creates the branch.
2. Switches you from `main` to the new branch.

After running this command, any changes you make will happen inside `feature/lesson`, not directly on `main`.

---

## 8. Method 2: Create a Branch Without Switching

You can also create a branch using `git branch`.

```bash
git branch feature/lesson           # Create the branch but do not switch to it.
```

This only creates the branch. It does not move you into the branch.

To move into the branch, you need another command:

```bash
git checkout feature/lesson         # Switch from the current branch to feature/lesson.
```

So these two commands together do the same job as `git checkout -b feature/lesson`.

---

## 9. Modern Alternative: Using git switch

A newer Git command is `git switch`.

```bash
git switch -c feature/lesson        # Create a new branch and switch to it.
```

This is similar to:

```bash
git checkout -b feature/lesson      # Create a new branch and switch to it.
```

Both are commonly used, but many beginners still learn `git checkout` first because it appears in many tutorials.

---

## 10. Checking Which Branch You Are On

To see all local branches and confirm which branch is active, use:

```bash
git branch                          # List local branches and mark the current branch with an asterisk.
```

Example output:

```bash
  main                              # This is one available branch.
* feature/lesson                    # The asterisk shows this is the active branch.
```

The branch with the `*` symbol is the branch you are currently using.

---

## 11. Why Branches Are Important

Branches keep work isolated.

If you create a branch called `feature/lesson`, changes made inside that branch do not automatically appear in `main`.

This means:

- The `main` branch stays clean.
- Your work can be reviewed before it is merged.
- Team members can work on different features at the same time.
- Mistakes are easier to fix because they are isolated in a branch.

A branch is like a safe workspace for your changes.

---

## 12. Creating a New File

Inside the new branch, the lesson creates a file called `test2.txt`.

```bash
touch test2.txt                     # Create an empty file named test2.txt.
```

The `touch` command creates a file if it does not already exist.

You can confirm the file was created with:

```bash
ls                                  # List the files in the current directory.
```

Example output:

```bash
README.md test.txt test2.txt        # Shows that test2.txt now exists.
```

---

## 13. Adding the File to the Staging Area

After creating or editing a file, Git does not automatically include it in a commit.

You must first stage the file using `git add`.

```bash
git add test2.txt                   # Add test2.txt to the staging area.
```

The staging area is a preparation area for your next commit.

You can check the status again:

```bash
git status                          # Show staged and unstaged changes.
```

Git should show that `test2.txt` is ready to be committed.

---

## 14. Committing the File

A commit saves your staged changes into Git history.

```bash
git commit -m "Add test2 file"      # Save the staged file with a clear commit message.
```

The `-m` flag lets you write a commit message directly in the command.

A good commit message should be short and clear. It should explain what changed.

Good examples:

```bash
git commit -m "Add test2 file"      # Clearly says a new test2 file was added.
git commit -m "Fix login button"    # Clearly says a login button bug was fixed.
git commit -m "Update README"       # Clearly says the README file was updated.
```

---

## 15. Pushing the Branch to GitHub

After committing locally, the changes are still only on your computer.

To send the branch and commits to GitHub, use `git push`.

```bash
git push -u origin feature/lesson   # Push the branch to GitHub and set upstream tracking.
```

Simple explanation:

- `git push` sends commits to the remote repository.
- `origin` is the remote repository name.
- `feature/lesson` is the branch being pushed.
- `-u` connects the local branch to the remote branch.

After using `-u` once, future pushes from that branch can usually be done with:

```bash
git push                            # Push changes to the already connected remote branch.
```

Important note: `-u` sets the upstream tracking branch. In simple terms, it links your local `feature/lesson` branch with the remote `origin/feature/lesson` branch.

---

## 16. Login Prompt When Using HTTPS

If the repository uses HTTPS, Git may ask for login details.

This can happen when pushing changes to GitHub.

Modern GitHub authentication usually uses a personal access token instead of a normal account password.

So if Git asks for a password, you may need to use a token depending on your setup.

---

## 17. Creating a Pull Request on GitHub

After pushing the branch, GitHub usually detects the new branch.

GitHub may show a button like:

```text
Compare & pull request              # Button used to start creating a pull request.
```

A pull request means:

> I have made changes in this branch. Please review them and merge them into the main branch if they are correct.

A pull request is often shortened to PR.

---

## 18. Comparing Branches in a Pull Request

When creating a pull request, GitHub compares two branches.

Usually:

```text
base branch: main                   # The branch you want to merge into.
compare branch: feature/lesson      # The branch containing your new changes.
```

This means GitHub checks what is different between `main` and `feature/lesson`.

In the transcript example, the main difference is that `test2.txt` exists in `feature/lesson` but not yet in `main`.

---

## 19. Reviewing the Pull Request

Before merging, the team can review the changes.

They may check:

- Whether the code is correct.
- Whether the code follows team standards.
- Whether the tests pass.
- Whether there are any bugs or mistakes.
- Whether the change should be approved or updated.

This helps protect the `main` branch from bad or unfinished code.

---

## 20. Why Pull Requests Are Useful

Pull requests are useful because they allow teamwork and review.

They help teams:

- Review code before it enters `main`.
- Discuss changes in one place.
- Request improvements.
- Run automated tests.
- Keep a history of decisions.
- Reduce mistakes in shared projects.

A pull request is not just a GitHub button. It is a collaboration process.

---

## 21. Merging the Pull Request

If the pull request is approved, it can be merged into `main`.

Merging means the changes from the feature branch are added to the main branch.

After merging, `test2.txt` becomes part of the `main` branch.

GitHub may also ask whether you want to delete the branch.

You can either:

- Keep the branch for reference.
- Delete the branch to keep the repository clean.

Many teams delete branches after merging, especially if the work is finished.

---

## 22. Returning to the Local Terminal

After the pull request is merged on GitHub, your local computer may not know about the new changes yet.

You need to switch back to the main branch.

```bash
git checkout main                   # Switch from the feature branch back to the main branch.
```

Then pull the latest changes from GitHub.

```bash
git pull                            # Download and apply the latest changes for the current branch.
```

Or more explicitly:

```bash
git pull origin main                # Pull the latest changes from the remote main branch.
```

After this, your local `main` branch should include the file that was merged from the pull request.

---

## 23. Confirming the Merged File Exists

Use `ls` to check the files in the directory.

```bash
ls                                  # List files in the current directory.
```

Example output:

```bash
README.md test.txt test2.txt        # Shows that test2.txt is now available in main.
```

This confirms that the file from the feature branch has been merged into `main` and pulled locally.

---

## 24. Complete Workflow Example

This is the complete workflow from the lesson.

```bash
pwd                                 # Check that you are inside the correct project directory.
git status                          # Check that your working directory is clean.
git checkout -b feature/lesson      # Create a new branch and switch to it.
git branch                          # Confirm that you are now on feature/lesson.
touch test2.txt                     # Create a new file called test2.txt.
git add test2.txt                   # Stage the new file for commit.
git commit -m "Add test2 file"      # Commit the staged file with a message.
git push -u origin feature/lesson   # Push the branch to GitHub and set upstream tracking.
```

After this, open GitHub and create a pull request from `feature/lesson` into `main`.

After the pull request is merged, return to the terminal:

```bash
git checkout main                   # Switch back to the main branch.
git pull origin main                # Pull the latest merged changes from GitHub.
ls                                  # Confirm that test2.txt exists in the main branch.
```

---

## 25. Example 1: Creating a Feature Branch and Adding a File

### Goal

Create a new feature branch, add a file, commit it, and push it to GitHub.

### Commands

```bash
pwd                                 # Confirm the current folder is the project repository.
git status                          # Make sure there are no unfinished changes.
git checkout -b feature/profile     # Create and switch to a branch called feature/profile.
touch profile.txt                   # Create a new file called profile.txt.
git add profile.txt                 # Stage the profile.txt file.
git commit -m "Add profile file"    # Commit the new file with a clear message.
git push -u origin feature/profile  # Push the new branch to GitHub.
```

### Explanation

This example creates a branch for profile-related work. The new file is added only inside the `feature/profile` branch. The main branch is not changed until the branch is reviewed and merged.

---

## 26. Example 2: Creating a Branch Using git branch

### Goal

Create a branch using `git branch`, then switch to it manually.

### Commands

```bash
git status                          # Check the current state of the repository.
git branch feature/contact          # Create a new branch called feature/contact.
git checkout feature/contact        # Switch into the feature/contact branch.
git branch                          # Confirm that feature/contact is the active branch.
touch contact.txt                   # Create a new file for contact-related work.
git add contact.txt                 # Stage the new file.
git commit -m "Add contact file"    # Commit the file to the branch.
git push -u origin feature/contact  # Push the branch to GitHub.
```

### Explanation

This method uses two steps to create and enter the branch. First, `git branch feature/contact` creates the branch. Then, `git checkout feature/contact` switches into it.

---

## 27. Example 3: Updating Local Main After a Pull Request Merge

### Goal

After merging a pull request on GitHub, update the local `main` branch.

### Commands

```bash
git checkout main                   # Move back to the main branch.
git status                          # Check whether the main branch has a clean working tree.
git pull origin main                # Download and apply the latest changes from GitHub main.
ls                                  # List files to confirm the merged changes are present.
```

### Explanation

When a pull request is merged on GitHub, your local repository does not update automatically. You must use `git pull` to bring the latest remote changes into your local branch.

---

## 28. Branch Naming Conventions

Teams often follow naming rules for branches.

Common examples:

| Branch Type | Example | Meaning |
|---|---|---|
| Feature branch | `feature/lesson` | Used for new features or new work. |
| Fix branch | `fix/login-error` | Used for bug fixes. |
| Hotfix branch | `hotfix/payment-crash` | Used for urgent production fixes. |
| Chore branch | `chore/update-dependencies` | Used for maintenance tasks. |
| Docs branch | `docs/readme-update` | Used for documentation updates. |

Good branch names help the team understand the purpose of the work quickly.

---

## 29. Pull Request Review Process

A typical pull request process looks like this:

1. Developer creates a branch.
2. Developer makes changes.
3. Developer commits the changes.
4. Developer pushes the branch to GitHub.
5. Developer opens a pull request.
6. Team reviews the pull request.
7. Team may approve or request changes.
8. Developer updates the branch if needed.
9. Pull request is merged into `main`.
10. Local `main` is updated with `git pull`.

This process helps teams avoid mistakes and keep the main branch stable.

---

## 30. Common Mistakes and Fixes

### Mistake 1: Creating a branch in the wrong folder

Problem:

```bash
git status                          # Shows an error because you are not inside a Git repository.
```

Fix:

```bash
pwd                                 # Check your current directory.
cd my-first-repo                    # Move into the correct repository folder.
git status                          # Check Git status again.
```

---

### Mistake 2: Forgetting to switch branches

Problem:

You create a branch using `git branch`, but you are still on `main`.

Fix:

```bash
git branch                          # Check which branch is active.
git checkout feature/lesson         # Switch to the feature branch.
```

---

### Mistake 3: Forgetting to add files before committing

Problem:

```bash
git commit -m "Add file"            # Git says there is nothing to commit.
```

Fix:

```bash
git status                          # Check which files are untracked or modified.
git add test2.txt                   # Stage the file.
git commit -m "Add test2 file"      # Commit the staged file.
```

---

### Mistake 4: Push asks for upstream branch

Problem:

```bash
git push                            # Git says the current branch has no upstream branch.
```

Fix:

```bash
git push -u origin feature/lesson   # Push the branch and set upstream tracking.
```

---

### Mistake 5: Merged file is not visible locally

Problem:

The pull request was merged on GitHub, but the file is missing on your local computer.

Fix:

```bash
git checkout main                   # Switch to the local main branch.
git pull origin main                # Pull the latest changes from GitHub.
ls                                  # Confirm the merged file is now visible.
```

---

## 31. Command Summary Table

| Command | Purpose |
|---|---|
| `pwd` | Shows the current directory. |
| `git status` | Shows the current state of the repository. |
| `git branch` | Lists local branches. |
| `git branch branch-name` | Creates a branch but does not switch to it. |
| `git checkout branch-name` | Switches to an existing branch. |
| `git checkout -b branch-name` | Creates a new branch and switches to it. |
| `git switch -c branch-name` | Modern way to create and switch to a branch. |
| `touch file.txt` | Creates a new empty file. |
| `git add file.txt` | Stages a file for commit. |
| `git commit -m "message"` | Saves staged changes with a message. |
| `git push -u origin branch-name` | Pushes a branch to GitHub and sets upstream tracking. |
| `git pull origin main` | Pulls the latest changes from the remote main branch. |
| `ls` | Lists files in the current directory. |

---

## 32. Simple Visual Workflow

```text
main branch
    |
    | create branch
    v
feature/lesson branch
    |
    | make changes
    v
commit changes
    |
    | push branch
    v
GitHub remote branch
    |
    | create pull request
    v
review changes
    |
    | merge pull request
    v
main branch updated
    |
    | git pull locally
    v
local main branch updated
```

---

## 33. Key Points to Remember

- Always check `pwd` to make sure you are in the correct folder.
- Always run `git status` before starting new work.
- A branch lets you work safely without changing `main` directly.
- `git checkout -b branch-name` creates and switches to a new branch.
- `git branch branch-name` only creates the branch.
- `git add` stages changes.
- `git commit` saves changes locally.
- `git push` sends commits to GitHub.
- A pull request is used to review and merge branch changes into `main`.
- After merging on GitHub, run `git pull` on local `main` to get the latest changes.

---

## 34. Final Summary

The Git branching workflow is one of the most important habits in software development. Instead of working directly on the `main` branch, developers create separate branches for features, fixes, or experiments.

In this lesson, a branch called `feature/lesson` was created. A file named `test2.txt` was added, staged, committed, and pushed to GitHub. Then a pull request was created so the changes could be reviewed and merged into `main`.

This workflow keeps the project organized, protects the main branch, and makes teamwork much easier.
