# Essential Git Commands Every Developer Should Know

As a developer, mastering Git is crucial for effective version control and collaboration. In this comprehensive guide, I'll walk you through the most essential Git commands that I use daily, complete with practical examples and best practices.


## Table of Contents
- [Git Status](#git-status)
- [Git Add](#git-add)
- [Git Commit](#git-commit)
- [Git Push](#git-push)
- [Git Pull](#git-pull)
- [Git Fetch](#git-fetch)
- [Git Rebase](#git-rebase)
- [Git Reflog](#git-reflog)
- [Git Log](#git-log)
- [Git Reset](#git-reset)

## Git Status
Shows the status of files in your working directory and staging area.

```bash
# Check the status of your repository
git status

# Get a simplified status output
git status -s
```

**Example:**
```bash
$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   src/app.js

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        docs/
```

## Git Add
Adds files to the staging area for commit.

```bash
# Add a specific file
git add filename.txt

# Add all files
git add .

# Add all files with a specific extension
git add *.js

# Add files interactively
git add -p
```

**Example:**
```bash
$ git add src/app.js
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   src/app.js
```

## Git Commit
Records changes to the repository.

```bash
# Commit with a message
git commit -m "Your commit message"

# Add and commit in one command
git commit -am "Add and commit message"

# Amend the last commit
git commit --amend

# Commit with a detailed description
git commit -m "Add user authentication feature" -m "- Implement login/logout functionality
- Add password hashing
- Create user session management
- Add remember me option
- Update tests for new features"
```

**Example:**
```bash
$ git add src/app.js
$ git commit -m "feat: add user authentication"
[main 5d6e8f9] feat: add user authentication
 1 file changed, 25 insertions(+), 2 deletions(-)
```

## Git Push
Uploads local repository content to a remote repository.

```bash
# Push to default remote (origin) and branch
git push

# Push to specific remote and branch
git push origin main

# Force push (use with caution!)
git push -f origin main

# Push all branches
git push --all
```

**Example:**
```bash
$ git push origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 2.95 KiB | 2.95 MiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
To github.com:username/repo.git
   8d5e7f9..5d6e8f9  main -> main
```

## Git Pull
Fetches and integrates changes from a remote repository.

```bash
# Pull from default remote
git pull

# Pull from specific remote and branch
git pull origin main

# Pull with rebase instead of merge
git pull --rebase
```

**Example:**
```bash
$ git pull origin main
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 3 (delta 1)
Unpacking objects: 100% (3/3), done.
From github.com:username/repo
 * branch            main       -> FETCH_HEAD
   8d5e7f9..5d6e8f9  main       -> origin/main
Updating 8d5e7f9..5
```

## Git Fetch
Downloads objects and refs from a remote repository without integrating changes.

```bash
# Fetch from all remotes
git fetch --all

# Fetch from specific remote
git fetch origin

# Fetch a specific branch
git fetch origin feature-branch

# Fetch and prune deleted remote branches
git fetch -p
```

**Example:**
```bash
$ git fetch --all
Fetching origin
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From github.com:username/repo
   5d6e8f9..7a9b2c3  feature-branch -> origin/feature-branch
```

## Git Rebase
Reapplies commits on top of another base.

```bash
# Start an interactive rebase
git rebase -i HEAD~3

# Continue the rebase
git rebase --continue

# Abort the rebase
git rebase --abort

# Skip the current commit and continue
git rebase --skip
```
**Example:**
```bash
$ git reflog
7a9b2c3 HEAD@{0}: commit: Add payment integration
5d6e8f9 HEAD@{1}: commit: Add user authentication
8d5e7f9 HEAD@{2}: commit: Add user session management
7a9b2c3 HEAD@{3}: commit: Initial commit


$ git rebase -i HEAD~3
# In editor, change:
pick 8d5e7f9 Add user session management
edit 5d6e8f9 Add user authentication #changed
pick 7a9b2c3 Add payment integration


# After making changes:
$ git add src/auth.js
$ git commit --amend
$ git rebase --continue
Successfully rebased and updated refs/heads/main.
```

## Git Reflog
Shows a log of changes to the local repository's HEAD.

```bash
# Show reflog
git reflog
```
**Example:**
```bash
$ git reflog
7a9b2c3 HEAD@{0}: rebase finished: returning to refs/heads/main
7a9b2c3 HEAD@{1}: rebase: Add payment integration
5d6e8f9 HEAD@{2}: rebase: Add user authentication
8d5e7f9 HEAD@{3}: checkout: moving from main to 5d6e8f9
```


## Git Log
Shows commit logs.

```bash
# Show commit history
git log

# Show compact log
git log --oneline

# Show graph of commits
git log --graph --oneline --decorate

# Show commits by author
git log --author="username"

# Show commits in date range
git log --since="2 weeks ago"
```
**Example:**
```bash
$ git log --oneline --graph --decorate
* 7a9b2c3 (HEAD -> main, origin/main) Add payment integration
* 5d6e8f9 Add user authentication
* 8d5e7f9 Initial commit
```

## Git Reset
Resets the current HEAD to a specified state.

```bash
# Soft reset - keeps changes staged
git reset --soft HEAD~1

# Mixed reset (default) - unstages changes but keeps them in working directory
git reset HEAD~1
git reset --mixed HEAD~1

# Hard reset - discards all changes
git reset --hard HEAD~1

# Reset to specific commit
git reset --hard commit_hash

# Reset a specific file to last commit
git reset HEAD filename.txt

# Reset to remote branch state
git reset --hard origin/main

# Undo a reset using reflog
git reset --hard HEAD@{1}
```
**Example:**
```bash
$ git reset --hard HEAD~1
HEAD is now at 5d6e8f9 Add user authentication

$ git reflog
5d6e8f9 HEAD@{0}: reset: moving to HEAD~1
7a9b2c3 HEAD@{1}: commit: Add payment integration

# Undo the reset
$ git reset --hard HEAD@{1}
HEAD is now at 7a9b2c3 Add payment integration
```