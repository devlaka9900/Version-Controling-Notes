# Git Conflict Handling Documentation

## Purpose

This document explains how to handle Git conflicts in a simple but detailed way. It is written for beginners who already know the basic Git workflow:

```bash
# Add file changes to the staging area
git add .

# Save staged changes into the local Git history
git commit -m "Write a clear commit message"

# Upload local commits to the remote repository
git push origin main

# Download and merge the latest changes from the remote repository
git pull origin main
```

A Git conflict usually happens when Git cannot automatically combine two different changes. Git pauses the operation and asks you to decide what the final version should look like.

---

## Table of Contents

1. [What Is a Git Conflict?](#what-is-a-git-conflict)
2. [Why Conflicts Happen](#why-conflicts-happen)
3. [Common Conflict Situations](#common-conflict-situations)
4. [Important Conflict Terms](#important-conflict-terms)
5. [Conflict Markers Explained](#conflict-markers-explained)
6. [Main Conflict Resolution Workflow](#main-conflict-resolution-workflow)
7. [Handling a Conflict During Merge](#handling-a-conflict-during-merge)
8. [Handling a Conflict During Pull](#handling-a-conflict-during-pull)
9. [Handling a Conflict During Rebase](#handling-a-conflict-during-rebase)
10. [Handling Deleted File Conflicts](#handling-deleted-file-conflicts)
11. [Using Ours and Theirs](#using-ours-and-theirs)
12. [Using a Merge Tool](#using-a-merge-tool)
13. [Handling Conflicts in a GitHub Pull Request](#handling-conflicts-in-a-github-pull-request)
14. [Complete Example 1: Same Line Conflict](#complete-example-1-same-line-conflict)
15. [Complete Example 2: Conflict During Git Pull](#complete-example-2-conflict-during-git-pull)
16. [Complete Example 3: Rebase Conflict](#complete-example-3-rebase-conflict)
17. [Complete Example 4: Deleted File Conflict](#complete-example-4-deleted-file-conflict)
18. [How to Cancel a Conflict Resolution](#how-to-cancel-a-conflict-resolution)
19. [Best Practices to Avoid Conflicts](#best-practices-to-avoid-conflicts)
20. [Quick Cheat Sheet](#quick-cheat-sheet)
21. [Summary](#summary)
22. [References](#references)

---

## What Is a Git Conflict?

A Git conflict happens when Git tries to combine changes from two different sources but cannot safely decide which change should be kept.

For example, imagine two developers edit the same line in the same file:

- Developer A changes line 10 to say `Welcome to the homepage`.
- Developer B changes the same line to say `Welcome to our website`.

When Git tries to merge these changes, it does not know which sentence is correct. So Git stops and shows a conflict.

A conflict is not a disaster. It simply means a human needs to review the file and choose the correct final content.

---

## Why Conflicts Happen

Conflicts usually happen because two branches contain changes that overlap.

Common reasons include:

| Reason | Explanation |
|---|---|
| Same line changed | Two people changed the same line in the same file. |
| File edited and deleted | One person edited a file while another person deleted it. |
| Large branches | A branch was not updated for a long time, so many changes built up. |
| Generated files committed | Files created by tools or builds were committed and changed often. |
| Poor communication | Multiple developers worked on the same area without coordination. |

Git can automatically merge many changes. It only asks for help when the changes are too similar or conflicting.

---

## Common Conflict Situations

### 1. Merge conflict

This happens when you merge one branch into another branch.

```bash
# Switch to the branch that should receive changes
git checkout main

# Merge the feature branch into the current branch
git merge feature/login-page
```

If Git cannot automatically combine the changes, it will show a conflict.

---

### 2. Pull conflict

`git pull` downloads changes from a remote repository and combines them with your local branch.

```bash
# Pull latest changes from the remote main branch
git pull origin main
```

A conflict can happen if your local work and the remote work changed the same part of a file.

---

### 3. Rebase conflict

`git rebase` moves your commits on top of another branch. This can create a conflict if your commits overlap with commits from the target branch.

```bash
# Rebase the current branch on top of the latest main branch
git rebase main
```

If a conflict happens during rebase, you resolve the conflict, stage the file, and continue the rebase.

---

### 4. Pull request conflict

A GitHub pull request can show a conflict when the feature branch cannot be automatically merged into the base branch.

For example:

- Base branch: `main`
- Feature branch: `feature/navbar`
- Conflict: both branches changed the same line in `index.html`

You must resolve the conflict before the pull request can be merged.

---

## Important Conflict Terms

| Term | Meaning |
|---|---|
| Current branch | The branch you are currently working on. |
| Incoming branch | The branch being merged into your current branch. |
| `HEAD` | A pointer to your current branch or current commit. |
| `origin` | The usual name for the remote repository. |
| `main` | The main/default branch in many repositories. |
| Conflict markers | Special symbols that Git adds to show conflicting sections. |
| Staging | Marking the resolved file with `git add`. |
| Merge commit | A commit that records a completed merge. |

---

## Conflict Markers Explained

When Git finds a conflict, it edits the conflicted file and adds conflict markers.

Example:

```text
<<<<<<< HEAD
Welcome to the homepage
=======
Welcome to our website
>>>>>>> feature/homepage-title
```

This means:

| Marker | Meaning |
|---|---|
| `<<<<<<< HEAD` | Start of the current branch version. |
| Text under `HEAD` | The version from your current branch. |
| `=======` | Separator between the two versions. |
| Text under separator | The version from the branch being merged in. |
| `>>>>>>> feature/homepage-title` | End of the incoming branch version. |

Your job is to edit the file and remove the conflict markers.

Final resolved example:

```text
Welcome to our homepage
```

After resolving, the file should not contain:

```text
<<<<<<<
=======
>>>>>>>
```

If these markers remain in the file, the conflict is not fully resolved.

---

## Main Conflict Resolution Workflow

This is the main workflow you should follow for most Git conflicts.

### Step 1: Check the repository status

```bash
# Show current branch and conflicted files
git status
```

Git will show files that need conflict resolution. They may appear under `unmerged paths`.

---

### Step 2: Open the conflicted file

Open the file in your code editor.

Example:

```bash
# Open the conflicted file in Visual Studio Code
code index.html
```

You can also use any editor you prefer.

---

### Step 3: Find the conflict markers

Search inside the file for:

```text
<<<<<<<
```

This helps you quickly find the conflict.

---

### Step 4: Decide what the final file should contain

You have three main choices:

1. Keep your current branch change.
2. Keep the incoming branch change.
3. Combine both changes into a new correct version.

Do not choose blindly. Read the code and understand the expected final result.

---

### Step 5: Remove the conflict markers

Delete these marker lines from the file:

```text
<<<<<<< HEAD
=======
>>>>>>> branch-name
```

Keep only the final correct content.

---

### Step 6: Test the project

If the project has tests, run them.

```bash
# Run project tests if the project uses npm
npm test
```

Or run the relevant command for your project.

---

### Step 7: Stage the resolved file

```bash
# Mark the conflicted file as resolved
git add index.html
```

This tells Git that you fixed the conflict in that file.

---

### Step 8: Finish the merge, pull, or rebase

For a merge conflict:

```bash
# Complete the merge by creating a merge commit
git commit
```

For a rebase conflict:

```bash
# Continue the rebase after resolving the conflict
git rebase --continue
```

For a pull conflict, the final command depends on how the pull was done:

```bash
# Complete a normal pull conflict that used merge
git commit
```

```bash
# Complete a pull conflict that used rebase
git rebase --continue
```

---

## Handling a Conflict During Merge

A merge conflict happens when you run `git merge` and Git cannot automatically combine changes.

### Example workflow

```bash
# Switch to the branch that should receive the changes
git checkout main

# Make sure main is updated with the latest remote changes
git pull origin main

# Merge the feature branch into main
git merge feature/header-update
```

If Git shows a conflict, run:

```bash
# Check which files are conflicted
git status
```

Open each conflicted file and resolve the markers.

Then run:

```bash
# Stage the resolved file
git add index.html

# Complete the merge commit
git commit
```

Git usually opens an editor with a default merge commit message. You can keep the default message unless your team wants a different format.

---

## Handling a Conflict During Pull

A `git pull` normally means:

1. Download changes from the remote repository.
2. Merge those changes into your current local branch.

So this command:

```bash
# Pull changes from the remote main branch
git pull origin main
```

Is similar to:

```bash
# Download remote changes without merging yet
git fetch origin

# Merge the downloaded origin/main into the current branch
git merge origin/main
```

A conflict can happen if your local branch and the remote branch changed the same lines.

### Pull conflict workflow

```bash
# Check the current branch and conflict state
git status

# Open the conflicted file in your editor
code test.txt

# Stage the file after resolving the conflict
git add test.txt

# Complete the merge created by git pull
git commit
```

After the conflict is resolved, you can push if needed.

```bash
# Push the resolved changes to the remote main branch
git push origin main
```

---

## Handling a Conflict During Rebase

A rebase conflict is handled slightly differently from a merge conflict.

During a rebase, Git pauses at the commit that caused the conflict.

Example:

```bash
# Switch to your feature branch
git checkout feature/profile-page

# Rebase the feature branch on top of main
git rebase main
```

If Git shows a conflict:

```bash
# Check which file has conflicts
git status

# Open the conflicted file in your editor
code profile.html

# Stage the file after resolving the conflict
git add profile.html

# Continue the rebase process
git rebase --continue
```

If there are more conflicts, Git may stop again. Repeat the same process:

1. Resolve the file.
2. Stage it with `git add`.
3. Continue with `git rebase --continue`.

When the rebase is finished, your branch history will be placed on top of the target branch.

---

## Handling Deleted File Conflicts

A deleted file conflict happens when one branch deletes a file while another branch edits the same file.

Git may show messages like:

```text
deleted by us:   notes.txt
```

or:

```text
deleted by them: notes.txt
```

You need to decide whether the final result should keep or delete the file.

### Option 1: Keep the file

```bash
# Check which file has the delete/edit conflict
git status

# Open the file and review the content if it still exists
code notes.txt

# Stage the file to keep it in the final result
git add notes.txt

# Complete the merge after choosing to keep the file
git commit
```

### Option 2: Delete the file

```bash
# Remove the file from the final result
git rm notes.txt

# Complete the merge after choosing to delete the file
git commit
```

The correct option depends on the project requirement.

---

## Using Ours and Theirs

Sometimes you may want to choose one complete side of a conflict.

### Keep the current branch version

```bash
# Keep the version from the current branch
git checkout --ours index.html

# Stage the resolved file
git add index.html
```

### Keep the incoming branch version

```bash
# Keep the version from the branch being merged in
git checkout --theirs index.html

# Stage the resolved file
git add index.html
```

Important note:

- In a normal merge, `ours` usually means the current branch.
- In a normal merge, `theirs` usually means the branch being merged in.
- During a rebase, these names can feel confusing because Git is replaying commits on top of another branch.

Use these commands carefully. They are useful, but they can remove important work if used without checking.

---

## Using a Merge Tool

A merge tool gives you a visual interface to resolve conflicts.

Common merge tools include:

- VS Code
- Meld
- KDiff3
- Beyond Compare
- Vimdiff

To use Git's configured merge tool:

```bash
# Start the configured merge tool for conflicted files
git mergetool
```

After resolving the conflict in the tool:

```bash
# Check the status after using the merge tool
git status

# Stage the resolved file if it is not already staged
git add index.html

# Complete the merge commit
git commit
```

Merge tools are helpful because they show the conflicting versions side by side.

---

## Handling Conflicts in a GitHub Pull Request

When you create a pull request on GitHub, GitHub checks whether the feature branch can be merged into the base branch.

If GitHub says the branch has conflicts, you have two main options.

### Option 1: Resolve simple conflicts on GitHub

GitHub may allow you to resolve simple line conflicts directly in the browser.

Basic process:

1. Open the pull request.
2. Click the conflict resolution option if available.
3. Edit the conflicted file.
4. Remove conflict markers.
5. Mark as resolved.
6. Commit the resolution.

This is useful for small text conflicts.

---

### Option 2: Resolve conflicts locally

For larger or more complex conflicts, resolve them on your local machine.

```bash
# Switch to the main branch
git checkout main

# Pull the latest main branch from GitHub
git pull origin main

# Switch back to your feature branch
git checkout feature/navbar

# Merge main into your feature branch
git merge main
```

If a conflict happens:

```bash
# Check which files are conflicted
git status

# Open the conflicted file in your editor
code index.html

# Stage the file after resolving the conflict
git add index.html

# Commit the conflict resolution
git commit -m "Resolve merge conflict with main"

# Push the updated feature branch to GitHub
git push origin feature/navbar
```

After pushing, the pull request should update automatically.

---

## Complete Example 1: Same Line Conflict

### Scenario

You have a file called `message.txt`.

On the `main` branch, the file says:

```text
Hello from main branch
```

On the `feature/message-update` branch, the same line says:

```text
Hello from feature branch
```

When you merge the feature branch into main, Git cannot decide which line to keep.

### Commands

```bash
# Switch to the main branch
git checkout main

# Merge the feature branch into main
git merge feature/message-update
```

Git may show output similar to:

```text
Auto-merging message.txt
CONFLICT (content): Merge conflict in message.txt
Automatic merge failed; fix conflicts and then commit the result.
```

### Conflicted file

`message.txt` may now look like this:

```text
<<<<<<< HEAD
Hello from main branch
=======
Hello from feature branch
>>>>>>> feature/message-update
```

### Resolve the conflict

You decide the final sentence should be:

```text
Hello from both main and feature branches
```

So you edit `message.txt` to contain only:

```text
Hello from both main and feature branches
```

### Finish the merge

```bash
# Stage the resolved file
git add message.txt

# Commit the resolved merge
git commit -m "Resolve message conflict"
```

### Final result

The conflict is resolved, and the `main` branch now contains the final corrected line.

---

## Complete Example 2: Conflict During Git Pull

### Scenario

You and another developer both edit `test.txt`.

Your local file says:

```text
This is my local change
```

The remote GitHub version says:

```text
This is the remote change
```

You run:

```bash
# Pull latest changes from the remote main branch
git pull origin main
```

Git cannot automatically combine the two changes.

### Check the conflict

```bash
# Show the files that need conflict resolution
git status
```

### Conflicted file

`test.txt` may look like this:

```text
<<<<<<< HEAD
This is my local change
=======
This is the remote change
>>>>>>> origin/main
```

### Resolve the conflict

You decide to keep both ideas:

```text
This is my local change
This is the remote change
```

### Finish the pull merge

```bash
# Stage the resolved file
git add test.txt

# Complete the merge created by git pull
git commit -m "Resolve pull conflict in test.txt"

# Push the completed resolution to the remote repository
git push origin main
```

### Final result

Your local branch and the remote branch are now synchronized with the resolved file content.

---

## Complete Example 3: Rebase Conflict

### Scenario

You are working on a branch called `feature/about-page`.

The `main` branch has new commits, so you want to replay your feature branch commits on top of the latest `main` branch.

### Start the rebase

```bash
# Switch to your feature branch
git checkout feature/about-page

# Download latest remote data
git fetch origin

# Rebase your branch on top of origin/main
git rebase origin/main
```

Git may stop with a conflict.

### Check the conflict

```bash
# Show conflicted files during the rebase
git status
```

### Resolve the file

Open the conflicted file, remove conflict markers, and keep the final correct version.

```bash
# Open the conflicted file in your editor
code about.html
```

### Continue the rebase

```bash
# Stage the resolved file
git add about.html

# Continue replaying commits after the conflict is fixed
git rebase --continue
```

If another conflict appears, repeat the same steps.

### Push after rebase

If the feature branch was already pushed before the rebase, you may need to force push safely.

```bash
# Push rewritten branch history safely after rebase
git push --force-with-lease origin feature/about-page
```

`--force-with-lease` is safer than `--force` because it checks whether the remote branch changed unexpectedly before replacing it.

---

## Complete Example 4: Deleted File Conflict

### Scenario

You are merging `feature/remove-old-docs` into `main`.

- In `main`, someone edited `old-guide.md`.
- In the feature branch, someone deleted `old-guide.md`.

Git does not know whether to keep the edited file or delete it.

### Start the merge

```bash
# Switch to the main branch
git checkout main

# Merge the branch that deleted the file
git merge feature/remove-old-docs
```

### Check the conflict

```bash
# Show delete/edit conflict details
git status
```

You may see something like:

```text
CONFLICT (modify/delete): old-guide.md deleted in feature/remove-old-docs and modified in HEAD.
```

### Option A: Keep the file

```bash
# Keep the edited file in the final merge result
git add old-guide.md

# Complete the merge commit
git commit -m "Keep old guide after conflict review"
```

### Option B: Delete the file

```bash
# Remove the file from the final merge result
git rm old-guide.md

# Complete the merge commit
git commit -m "Remove old guide after conflict review"
```

### Final result

Choose the option that matches the project requirement.

---

## How to Cancel a Conflict Resolution

Sometimes you may start a merge or rebase and realize you want to stop.

### Cancel a merge conflict

```bash
# Abort the current merge and return to the previous state
git merge --abort
```

This tries to restore your branch to the state it was in before the merge started.

### Cancel a rebase conflict

```bash
# Abort the current rebase and return to the original branch state
git rebase --abort
```

Use abort when you are unsure, need to restart, or want to ask a teammate before continuing.

---

## Best Practices to Avoid Conflicts

You cannot avoid all conflicts, but you can reduce them.

### 1. Pull latest changes often

```bash
# Switch to your working branch
git checkout feature/my-task

# Pull latest changes from the remote branch if tracking is set
git pull
```

This keeps your local branch closer to the remote branch.

---

### 2. Keep feature branches small

Small branches are easier to review, merge, and fix.

Instead of one huge branch:

```text
feature/build-entire-application
```

Prefer smaller branches:

```text
feature/add-login-form
feature/add-navbar
feature/add-user-profile
```

---

### 3. Commit logical changes

A commit should represent one clear change.

Good commit message:

```text
Add validation to login form
```

Less useful commit message:

```text
Update stuff
```

---

### 4. Communicate with teammates

If two developers need to edit the same file, talk first.

This is especially important for:

- Shared configuration files
- Large components
- Database migration files
- Package lock files
- Generated files

---

### 5. Do not commit unnecessary generated files

Generated files often change automatically and can create conflicts.

Use `.gitignore` where appropriate.

```bash
# Open the .gitignore file in your editor
code .gitignore
```

Example `.gitignore` entries:

```gitignore
node_modules/
dist/
build/
.env
```

---

### 6. Run tests after resolving conflicts

A conflict can be textually resolved but logically wrong.

```bash
# Run automated tests after resolving conflicts
npm test
```

Also run the application manually if needed.

---

### 7. Do not leave conflict markers in files

Before committing, search for conflict markers.

```bash
# Search for unresolved conflict markers in the project
grep -R "<<<<<<<" .
```

If this command returns results, inspect them before committing.

---

## Quick Cheat Sheet

### Check conflict status

```bash
# Show current branch and conflicted files
git status
```

### View conflict differences

```bash
# Show unstaged changes and conflict sections
git diff
```

### Stage a resolved file

```bash
# Mark one resolved file as fixed
git add filename.txt
```

### Complete a merge conflict

```bash
# Finish a merge after all conflicts are staged
git commit
```

### Continue a rebase conflict

```bash
# Continue a rebase after all conflicts for the current commit are staged
git rebase --continue
```

### Abort a merge

```bash
# Cancel the current merge
git merge --abort
```

### Abort a rebase

```bash
# Cancel the current rebase
git rebase --abort
```

### Use a merge tool

```bash
# Open the configured merge tool
git mergetool
```

### Keep current branch version

```bash
# Keep the current branch version of the file
git checkout --ours filename.txt

# Stage the chosen version
git add filename.txt
```

### Keep incoming branch version

```bash
# Keep the incoming branch version of the file
git checkout --theirs filename.txt

# Stage the chosen version
git add filename.txt
```

---

## Summary

Git conflicts happen when Git cannot automatically combine changes from different branches or repositories. The most common conflict is when two branches edit the same line in the same file.

The basic conflict resolution process is:

1. Run `git status`.
2. Open the conflicted file.
3. Find the conflict markers.
4. Choose or combine the correct changes.
5. Remove the conflict markers.
6. Test the project.
7. Stage the resolved file with `git add`.
8. Finish with `git commit` for merge conflicts or `git rebase --continue` for rebase conflicts.

The most important rule is simple: do not panic. A conflict is just Git asking you to decide what the final version should be.

---

## References

- Coursera course supplement link provided by the user: https://www.coursera.org/learn/introduction-to-version-control/supplement/R2ZBG/resolving-conflicts
- Git documentation: `git merge` - https://git-scm.com/docs/git-merge
- Git documentation: `git status` - https://git-scm.com/docs/git-status
- Git documentation: `git rebase` - https://git-scm.com/docs/git-rebase
- Git documentation: `git mergetool` - https://git-scm.com/docs/git-mergetool
- GitHub Docs: Resolving a merge conflict using the command line - https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line
