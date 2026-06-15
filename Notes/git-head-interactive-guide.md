# Understanding Git `HEAD` in a Simple, Detailed, Interactive Way 🚀

## 0. Tiny correction first

In the transcript, the word **"committee"** appears a few times. In Git, the correct word is **commit**.

A **commit** is a saved snapshot of your project at a specific point in time.

---

## 1. What you will learn

By the end of this guide, you will understand:

- What the hidden `.git` folder does
- What the `HEAD` file is
- How Git knows your current branch
- How branch files inside `.git/refs/heads/` work
- Why the commit hash changes only after a commit
- What happens when you switch branches

---

## 2. Big picture idea

Git keeps project history inside a hidden folder named:

```text
.git
```

This folder stores important information such as:

- Commits
- Branches
- Configuration
- Staging area information
- The current branch you are working on

The file that tells Git where you currently are is called:

```text
.git/HEAD
```

Think of `HEAD` as Git's **"you are here" pointer** 📍

---

## 3. Simple mental model

Imagine your project history like this:

```text
A --- B --- C  main
          \
           D --- E  testing
```

Here:

- `main` points to commit `C`
- `testing` points to commit `E`
- `HEAD` points to the branch you are currently using

If you are on `main`, Git sees this:

```text
HEAD -> main -> C
```

If you switch to `testing`, Git sees this:

```text
HEAD -> testing -> E
```

So, `HEAD` usually does **not directly point to a commit**. Usually, it points to a **branch**, and that branch points to the latest commit.

---

## 4. What is inside `.git/HEAD`?

When you are on the `main` branch, this command:

```bash
# Print the content of the HEAD file
cat .git/HEAD
```

May show something like this:

```text
ref: refs/heads/main
```

This means:

```text
HEAD -> refs/heads/main
```

In simple words:

> Git is saying: "The current branch is `main`."

---

## 5. What is inside `.git/refs/heads/main`?

The file `.git/refs/heads/main` stores the latest commit hash of the `main` branch.

Run this:

```bash
# Print the commit hash that the main branch currently points to
cat .git/refs/heads/main
```

You may see output like this:

```text
9c90a1e23f8b7d4a6c2e1f9b0a123456789abcd0
```

That long value is a **commit hash**.

A commit hash is like a unique ID for a commit.

So this relationship looks like:

```text
HEAD -> refs/heads/main -> 9c90a1e23f8b7d4a6c2e1f9b0a123456789abcd0
```

Meaning:

```text
HEAD -> main branch -> latest commit on main
```

---

## 6. Important command correction

The transcript says something like:

```text
cd.git
```

The correct command is:

```bash
# Move into the .git folder
cd .git
```

There must be a **space** between `cd` and `.git`.

Also, if you are already inside the `.git` folder, you can run:

```bash
# Print the current HEAD reference while inside the .git folder
cat HEAD
```

And:

```bash
# Print the commit hash for the main branch while inside the .git folder
cat refs/heads/main
```

But if you are in the project root, use:

```bash
# Print the current HEAD reference from the project root
cat .git/HEAD
```

```bash
# Print the commit hash for main from the project root
cat .git/refs/heads/main
```

---

## 7. Interactive Lab 1: Check your current branch

Run this from your project folder:

```bash
# Show all local branches and mark the current branch with an asterisk
git branch
```

Example output:

```text
* main
  testing
```

The `*` means you are currently on `main`.

Now check the `HEAD` file:

```bash
# Show what branch HEAD currently points to
cat .git/HEAD
```

Expected output:

```text
ref: refs/heads/main
```

This confirms:

```text
HEAD -> main
```

---

## 8. Interactive checkpoint 🧠

Answer this before continuing:

```text
If .git/HEAD contains ref: refs/heads/main, which branch are you on?
```

Answer:

```text
You are on the main branch.
```

---

## 9. Interactive Lab 2: Check the commit hash of your branch

Now check which commit `main` points to:

```bash
# Print the latest commit hash stored for the main branch
cat .git/refs/heads/main
```

Example output:

```text
8b55c2a9f43e2c91d4f7821a2b3c4d5e6f789abc
```

This means:

```text
main -> 8b55c2a9f43e2c91d4f7821a2b3c4d5e6f789abc
```

And because `HEAD` points to `main`:

```text
HEAD -> main -> 8b55c2a9f43e2c91d4f7821a2b3c4d5e6f789abc
```

---

## 10. What happens when you switch branches?

Suppose you have two branches:

```text
main
testing
```

Before switching:

```text
HEAD -> main
```

When you run:

```bash
# Switch from the current branch to the testing branch
git checkout testing
```

Or using the newer command:

```bash
# Switch from the current branch to the testing branch
git switch testing
```

Git updates `.git/HEAD`.

Now:

```text
HEAD -> testing
```

You can confirm it:

```bash
# Show what branch HEAD points to after switching branches
cat .git/HEAD
```

Expected output:

```text
ref: refs/heads/testing
```

---

## 11. Interactive Lab 3: Switch branches and inspect `HEAD`

Run these commands:

```bash
# Show the branch you are currently on
git branch

# Switch to the testing branch
git checkout testing

# Show branches again to confirm the active branch changed
git branch

# Print the HEAD file to see where HEAD points now
cat .git/HEAD
```

Expected result:

```text
ref: refs/heads/testing
```

This means Git moved `HEAD` from `main` to `testing`.

Before:

```text
HEAD -> main
```

After:

```text
HEAD -> testing
```

---

## 12. Branch names with slashes

Sometimes branch names look like this:

```text
feature/testing-branches
```

When you switch to that branch:

```bash
# Switch to a feature branch that contains a slash in the branch name
git checkout feature/testing-branches
```

Then check `HEAD`:

```bash
# Print the HEAD file after switching to the feature branch
cat .git/HEAD
```

You may see:

```text
ref: refs/heads/feature/testing-branches
```

This means:

```text
HEAD -> feature/testing-branches
```

Inside `.git/refs/heads/`, Git may store it like a folder path:

```text
.git/refs/heads/feature/testing-branches
```

---

## 13. What happens when you edit a file?

Let us say you are on `main`.

First, check the current commit hash:

```bash
# Print the commit hash that main currently points to
cat .git/refs/heads/main
```

Example output:

```text
8b55c2a9f43e2c91d4f7821a2b3c4d5e6f789abc
```

Now edit `README.md`.

For example:

```bash
# Open README.md in Vim for editing
vim README.md
```

Add a small line like:

```text
Minor update to my first repo.
```

Save the file.

Now check the branch hash again:

```bash
# Print the commit hash for main again after editing the file
cat .git/refs/heads/main
```

You should see the **same hash as before**.

Why?

Because editing a file does **not** create a new commit.

At this point, Git knows the file changed, but the branch still points to the old latest commit.

---

## 14. Check file status

Run:

```bash
# Show changed files in the working directory
git status
```

You may see:

```text
modified: README.md
```

This means:

```text
The file changed, but the change is not committed yet.
```

Your branch hash still does not change.

---

## 15. Add and commit the change

Now stage the file:

```bash
# Add README.md to the staging area
git add README.md
```

Or stage all changed files:

```bash
# Add all changed files to the staging area
git add .
```

Now commit:

```bash
# Create a new commit with a message
git commit -m "Add minor update"
```

After committing, check the branch hash again:

```bash
# Print the new commit hash that main points to
cat .git/refs/heads/main
```

Now the hash should be different.

Before commit:

```text
main -> 8b55c2a9f43e2c91d4f7821a2b3c4d5e6f789abc
```

After commit:

```text
main -> 9c90a1e23f8b7d4a6c2e1f9b0a123456789abcd0
```

This happens because a new commit was created.

Now the `main` branch moves forward to the new latest commit.

---

## 16. Very important concept

When you make a commit, Git updates the current branch pointer.

If you are on `main`:

```text
HEAD -> main -> old commit
```

After a new commit:

```text
HEAD -> main -> new commit
```

Notice:

- `HEAD` still points to `main`
- `main` now points to the new commit
- The commit hash inside `.git/refs/heads/main` changes

---

## 17. Simple diagram of commit movement

Before editing:

```text
A --- B --- C  main
              ↑
             HEAD
```

After editing but before commit:

```text
A --- B --- C  main
              ↑
             HEAD

Working directory has changes, but no new commit exists yet.
```

After commit:

```text
A --- B --- C --- D  main
                    ↑
                   HEAD
```

The branch moved from `C` to `D`.

---

## 18. Interactive checkpoint 🧠

Question:

```text
If you edit README.md but do not commit, will .git/refs/heads/main change?
```

Answer:

```text
No. It changes only after a new commit is created.
```

---

## 19. What is the difference between `HEAD` and a branch pointer?

| Item | What it stores | Example |
|---|---|---|
| `.git/HEAD` | The current branch reference | `ref: refs/heads/main` |
| `.git/refs/heads/main` | The latest commit hash of `main` | `9c90a1e...` |
| `.git/refs/heads/testing` | The latest commit hash of `testing` | `3f71b2c...` |

Simple explanation:

```text
HEAD tells Git which branch you are on.
The branch file tells Git which commit that branch points to.
```

---

## 20. Quick command summary

| Purpose | Command |
|---|---|
| Show current branch | `git branch` |
| Show HEAD content | `cat .git/HEAD` |
| Show main branch commit hash | `cat .git/refs/heads/main` |
| Switch branch | `git checkout branch-name` |
| Switch branch using newer command | `git switch branch-name` |
| Check changed files | `git status` |
| Stage changes | `git add .` |
| Commit changes | `git commit -m "message"` |

---

## 21. Safe practice exercise

Use this exercise in a test folder, not an important project.

```bash
# Create a new folder for practice
mkdir git-head-practice

# Move into the new practice folder
cd git-head-practice

# Initialize a new Git repository
git init

# Create a README file with initial text
echo "My first repo" > README.md

# Add the README file to the staging area
git add README.md

# Create the first commit
git commit -m "Initial commit"

# Show the current branch
git branch

# Show what HEAD points to
cat .git/HEAD

# Show the commit hash for the current branch, usually main or master
cat .git/refs/heads/main
```

> Note: Some Git installations create the first branch as `master` instead of `main`.
>
> If your branch is `master`, use:
>
> ```bash
> # Show the commit hash for the master branch
> cat .git/refs/heads/master
> ```

---

## 22. Practice branch switching

```bash
# Create and switch to a new branch named testing
git checkout -b testing

# Show the active branch
git branch

# Show that HEAD now points to testing
cat .git/HEAD

# Move back to main
git checkout main

# Show that HEAD now points back to main
cat .git/HEAD
```

If your default branch is `master`, use this instead:

```bash
# Move back to master if your default branch is master
git checkout master

# Show that HEAD now points back to master
cat .git/HEAD
```

---

## 23. Practice commit hash changes

```bash
# Show the current commit hash for main before editing
cat .git/refs/heads/main

# Add a new line to README.md
echo "Minor update" >> README.md

# Show Git status after editing the file
git status

# Show the commit hash again before committing
cat .git/refs/heads/main

# Stage the changed README.md file
git add README.md

# Commit the staged change
git commit -m "Add minor update"

# Show the commit hash again after committing
cat .git/refs/heads/main
```

Expected result:

```text
The hash before editing and before committing is the same.
The hash after committing is different.
```

---

## 24. Extra useful idea: Detached HEAD

Most of the time, `HEAD` points to a branch:

```text
HEAD -> main
```

But sometimes, `HEAD` can point directly to a commit:

```text
HEAD -> 9c90a1e23f8b7d4a6c2e1f9b0a123456789abcd0
```

This is called a **detached HEAD** state.

You may see it if you checkout a specific commit:

```bash
# Checkout a specific commit directly by its hash
git checkout 9c90a1e23f8b7d4a6c2e1f9b0a123456789abcd0
```

In that situation, `.git/HEAD` may contain a commit hash directly instead of:

```text
ref: refs/heads/main
```

For beginners, try to work on branches instead of working in detached HEAD mode.

---

## 25. Do not manually edit `.git` files

You can inspect files inside `.git`, but be careful.

Recommended:

```text
Reading .git files is okay for learning.
```

Not recommended:

```text
Manually editing .git files can damage your repository.
```

Use Git commands such as:

```bash
# Switch branches safely using Git
git checkout branch-name
```

```bash
# Create commits safely using Git
git commit -m "message"
```

Git commands update `.git` correctly for you.

---

## 26. Final summary

`HEAD` is Git's current position pointer.

Usually:

```text
HEAD -> current branch -> latest commit
```

Example:

```text
HEAD -> main -> 9c90a1e23f8b7d4a6c2e1f9b0a123456789abcd0
```

When you switch branches:

```text
HEAD moves to another branch.
```

When you commit:

```text
The current branch moves to the new commit.
```

When you only edit a file:

```text
The branch commit hash does not change yet.
```

The branch hash changes only after:

```text
git commit
```

---

## 27. Mini quiz

### Question 1

What file tells Git which branch you are currently on?

<details>
<summary>Show answer</summary>

```text
.git/HEAD
```

</details>

### Question 2

If `.git/HEAD` contains this:

```text
ref: refs/heads/testing
```

Which branch are you on?

<details>
<summary>Show answer</summary>

```text
testing
```

</details>

### Question 3

If you edit a file but do not commit, does the branch hash change?

<details>
<summary>Show answer</summary>

```text
No. The branch hash changes only after a commit.
```

</details>

### Question 4

What does `.git/refs/heads/main` store?

<details>
<summary>Show answer</summary>

```text
The latest commit hash of the main branch.
```

</details>

---

## 28. One-line memory trick

```text
HEAD tells Git where you are; the branch tells Git which commit is latest.
```

