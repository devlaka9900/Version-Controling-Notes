# Git Push and Git Pull - Full Notes

## 1. Introduction

In Git, you already use commands like `git add` and `git commit` to save changes in your local repository.

The next important step is learning how to share those local commits with a remote repository, such as GitHub. This is done using:

- `git push` to upload local commits to the remote repository.
- `git pull` to download the latest changes from the remote repository to your local repository.

This is a very important part of Git because Git is a distributed version control system. That means you can work on your own machine first, save your commits locally, and only connect to GitHub when you need to send or receive changes.

---

## 2. Local Repository vs Remote Repository

A **local repository** is the Git project stored on your own computer.

A **remote repository** is the Git project stored on another server, usually GitHub.

Example:

```text
Local repository  -> Your laptop or computer
Remote repository -> GitHub server
```

When you commit changes, those changes are saved locally first. They do not automatically appear on GitHub.

To send your local commits to GitHub, you must use:

```bash
# Upload local commits to the remote repository.
git push
```

To get the latest changes from GitHub, you must use:

```bash
# Download and apply remote changes to your local repository.
git pull
```

---

## 3. Checking the Repository Status

Before pushing or pulling, it is good practice to check the current state of your repository.

Use:

```bash
# Show the current branch and repository status.
git status
```

This command can tell you important information such as:

- Which branch you are currently using.
- Whether files are modified.
- Whether files are staged.
- Whether there are commits waiting to be pushed.
- Whether your local branch is ahead of or behind the remote branch.

---

## 4. Meaning of "Your branch is ahead of origin/main by one commit"

Sometimes `git status` may show a message like this:

```text
Your branch is ahead of 'origin/main' by 1 commit.
```

This means your local repository has one commit that does not exist yet in the remote repository on GitHub.

In simple words:

```text
Local main has new work.
GitHub main does not have that work yet.
```

So your local branch is ahead of the remote branch.

To send that commit to GitHub, you need to use `git push`.

---

## 5. Checking the Current Branch

Before pushing, always check which branch you are currently on.

You can use:

```bash
# Show the current repository status, including the current branch.
git status
```

Or:

```bash
# List all local branches and show the active branch with an asterisk.
git branch
```

This is important because you should know exactly which branch you are pushing to GitHub.

For example, if you are on the `main` branch, you usually push to the remote `main` branch.

---

## 6. What is `origin`?

In Git, `origin` is the default name for the remote repository.

When your local repository is connected to GitHub, Git often calls that connection `origin`.

You can think of it like this:

```text
origin = the GitHub repository connected to this local project
```

To check your remote connection, use:

```bash
# Show the remote repository URLs connected to this local repository.
git remote -v
```

Example output:

```text
origin  https://github.com/user/my-repo.git (fetch)
origin  https://github.com/user/my-repo.git (push)
```

This means your local repository is connected to a GitHub repository.

---

## 7. What is `git push`?

The `git push` command uploads commits from your local repository to the remote repository.

Basic command:

```bash
# Push local commits to the remote repository.
git push
```

More specific command:

```bash
# Push the local main branch to the main branch on the origin remote.
git push origin main
```

Here is what each part means:

| Part | Meaning |
|---|---|
| `git` | Runs Git. |
| `push` | Sends local commits to the remote repository. |
| `origin` | The remote repository name. |
| `main` | The branch you want to push to. |

So this command means:

```text
Send my local main branch commits to the main branch on GitHub.
```

---

## 8. What happens during `git push`?

When you run `git push origin main`, Git does these steps:

1. Checks your local commits.
2. Connects to the remote repository on GitHub.
3. Compares your local branch with the remote branch.
4. Uploads commits that the remote repository does not have.
5. Updates the remote branch if there are no conflicts or blocking issues.

If your push is successful, your changes will appear on GitHub.

If the remote repository has newer changes that your local repository does not have, the push may be rejected. In that case, you usually need to run `git pull` first.

---

## 9. Why should you pull before pushing?

It is a good habit to run `git pull` before `git push`, especially when working with a team.

This helps you get the latest changes from GitHub before uploading your own changes.

Recommended workflow:

```bash
# Check the current state of your repository.
git status

# Download and merge the latest changes from the remote main branch.
git pull origin main

# Push your local commits to the remote main branch.
git push origin main
```

This reduces the chance of conflicts because your local branch is updated before you push.

---

## 10. What is `git pull`?

The `git pull` command downloads changes from the remote repository and applies them to your local repository.

Basic command:

```bash
# Pull the latest changes from the current remote tracking branch.
git pull
```

More specific command:

```bash
# Pull the latest changes from the main branch on origin.
git pull origin main
```

Here is what each part means:

| Part | Meaning |
|---|---|
| `git` | Runs Git. |
| `pull` | Downloads and applies remote changes. |
| `origin` | The remote repository name. |
| `main` | The branch you want to pull from. |

So this command means:

```text
Get the latest changes from the main branch on GitHub and apply them to my local main branch.
```

---

## 11. What happens during `git pull`?

When you run `git pull`, Git normally performs two actions:

1. **Fetch**: Downloads the latest commits from the remote repository.
2. **Merge**: Applies those changes to your current local branch.

In simple words:

```text
git pull = git fetch + git merge
```

If there are no conflicts, Git automatically applies the changes.

If there are conflicts, Git asks you to fix them manually before completing the merge.

---

## 12. Example scenario from the lesson

The lesson demonstrates this situation:

1. A local repository has a commit that GitHub does not have yet.
2. `git status` shows that the local branch is ahead of `origin/main` by one commit.
3. The user runs `git push origin main`.
4. The commit is uploaded to GitHub.
5. The GitHub page is refreshed.
6. The new file, such as `test.txt`, appears on GitHub.

Then the lesson demonstrates pulling:

1. A change is made directly on GitHub using the GitHub website.
2. The change is committed to the remote `main` branch.
3. The local machine does not have that change yet.
4. The user runs `git pull`.
5. Git downloads the change and updates the local file.
6. The user checks the file and sees the new content locally.

---

## 13. Viewing file content with `cat`

To check the content of a file in the terminal, use the `cat` command.

Example:

```bash
# Display the contents of test.txt in the terminal.
cat test.txt
```

If the file is empty, no text will appear.

If the file contains text, the text will be printed in the terminal.

For example, after pulling from GitHub, the file might show:

```text
this is my change
```

This confirms that the remote change has been downloaded to the local repository.

---

# Complete Example 1: Push local commits to GitHub

## Goal

Send a local commit from your computer to GitHub.

## Steps

```bash
# Check the current branch and repository status.
git status

# Add the file test.txt to the staging area.
git add test.txt

# Commit the staged file with a clear message.
git commit -m "Add test.txt"

# Push the local main branch to the remote main branch on origin.
git push origin main
```

## Explanation

The `git status` command checks the current state of the repository.

The `git add test.txt` command places the file into the staging area.

The `git commit -m "Add test.txt"` command saves a snapshot of the staged file in the local repository.

The `git push origin main` command uploads the local commit to the remote `main` branch on GitHub.

## Result

After the push is complete, the file `test.txt` should appear in the GitHub repository.

---

# Complete Example 2: Pull remote changes to the local machine

## Goal

Download changes from GitHub to your local repository.

## Scenario

Someone edited `test.txt` on GitHub and committed the change directly to the `main` branch.

Your local repository does not have that change yet.

## Steps

```bash
# Check the current local repository status.
git status

# Display the current contents of test.txt before pulling.
cat test.txt

# Pull the latest changes from the remote main branch.
git pull origin main

# Display the contents of test.txt again after pulling.
cat test.txt
```

## Explanation

Before running `git pull`, the local file may be empty or outdated.

The `git pull origin main` command connects to GitHub, downloads the latest commits from the remote `main` branch, and applies them to the local `main` branch.

After pulling, running `cat test.txt` again should show the new content from GitHub.

## Result

The local file is updated with the latest remote changes.

Example output after pulling:

```text
this is my change
```

---

# Complete Example 3: Safe daily Git workflow

## Goal

Use a clean workflow when working on a shared GitHub project.

## Steps

```bash
# Check which branch you are currently on and whether files have changed.
git status

# Confirm the current branch list and active branch.
git branch

# Pull the latest changes from GitHub before starting or pushing work.
git pull origin main

# Add all changed files to the staging area.
git add .

# Commit the staged changes with a useful message.
git commit -m "Update project files"

# Push your local commits to the remote main branch.
git push origin main
```

## Explanation

This workflow is useful because it makes sure your local repository is updated before you push changes.

The `git pull origin main` command helps reduce conflicts by getting the latest remote changes first.

The `git add .` command stages all changed files.

The `git commit` command saves the changes locally.

The `git push origin main` command uploads the local commits to GitHub.

## Result

Your local changes are safely uploaded to GitHub, and your repository stays synchronized with the remote repository.

---

## 14. Common commands summary

| Command | Purpose |
|---|---|
| `git status` | Checks the current repository state. |
| `git branch` | Shows local branches and the active branch. |
| `git add file.txt` | Adds a file to the staging area. |
| `git add .` | Adds all changed files to the staging area. |
| `git commit -m "message"` | Saves staged changes as a local commit. |
| `git push origin main` | Uploads local commits to GitHub. |
| `git pull origin main` | Downloads and applies remote changes from GitHub. |
| `cat file.txt` | Displays the contents of a file. |

---

## 15. Important notes

### Commit does not mean upload

A commit only saves changes in your local repository.

To upload committed changes to GitHub, you need to use:

```bash
# Upload committed changes to the remote repository.
git push origin main
```

### GitHub changes do not automatically appear locally

If someone changes a file on GitHub, your local repository will not update automatically.

To download those changes, you need to use:

```bash
# Download remote changes to your local repository.
git pull origin main
```

### Push can fail if your local branch is outdated

If someone else pushed changes before you, your local branch may be behind the remote branch.

In that case, Git may reject your push.

You should pull first:

```bash
# Get the latest remote changes first.
git pull origin main

# Push again after your local branch is updated.
git push origin main
```

---

## 16. Simple comparison: push vs pull

| Command | Direction | Meaning |
|---|---|---|
| `git push` | Local -> Remote | Uploads your commits to GitHub. |
| `git pull` | Remote -> Local | Downloads GitHub changes to your computer. |

Simple memory trick:

```text
Push = send your work up to GitHub.
Pull = bring GitHub changes down to your computer.
```

---

## 17. Final summary

`git push` and `git pull` are used to synchronize your local repository with a remote repository like GitHub.

Use `git push` when you have local commits that you want to upload to GitHub.

Use `git pull` when GitHub has changes that you want to download to your local machine.

A good workflow is to check your status, pull the latest changes, make and commit your work, and then push your commits back to GitHub.

This workflow helps developers collaborate safely and keeps both local and remote repositories up to date.
