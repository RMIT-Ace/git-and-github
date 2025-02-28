# Working with Git Branches

- By default, git starts with one main repository - a main branch
- A branch is a duplicate repository of another branch/repository
- There is no limit number of branches
- Use branches for different purposes or usages, i.e.
    - Several branches for different experiments that can be discarded
    - Branches for releases
    - etc
- Contents of a branch can be merged with contents/changes from one or more branches

```
.
├── .git                     <<- Hidden folder
                                                
    +-----------------+
    |                 |
    | Git's Repository|
    |     (main)      |
    +-----------------+
             ^
             |
    +- - - - - - - - -+
    |                 |
    | Git's Staging   |
    | (imaginary)     |
    +- - - - - - - - -+

├── docs                      \
├── src                       |                  
├── any future direcotory     |- Your work area
├── any future direcotory     |
└── ...                       /

```

First check or list all branches within your project's repository.

```bash
$ git branch --all
```

Output

```
* main
```

# Creating a branch

Creating a new branch (i.e. from main branch)

```bash
$ git branch branch-1
```
Check/list all branches.

```
$ git branch --all
   branch-1
 * main
```

'*' denotes your current branch.

Switching branches, i.e. switching to `branch-1`

```
$ get checkout branch-1
Switched to branch 'branch-1'
```

List branches.

```
$ git branch --all
* branch-1
  main
```

'*' indicates `branch-1` is the current branch.


```
.
├── .git                     <<- Hidden folder
                                                
    +-----------------+     +------------+
    |                 |     |            |
    | Git's Repository| ->  |  branch-1  |
    |     (main)      |     |            |
    +-----------------+     +------------+
                                  ^
                                  |
                         +- - - - - - - - -+
                         |                 |
                         | Git's Staging   |
                         | (imaginary)     |
                         +- - - - - - - - -+

├── docs                      \
├── src                       |                  
├── any future direcotory     |- Your work area
├── any future direcotory     |
└── ...                       /
```

You work on a branch similarly to when working on the main branch. Your changes
are batch-updated from staging area into a current branch.

Let's check changes from working area (against the current branch).

```bash
$ git status
On branch branch-1
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	src/file3.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Let's add `file3.txt` into branch-1 repository.

```bash
$ git add src/file3.txt
```

Now current repository (branch-1) status shows:

```
$ git status
On branch branch-1
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   src/file3.txt
```

Commit this change.

```bash
$ git commit -m "Added file3"
```

Now, `file3.txt` is added to `branch-1` (note that `file3.txt` is NOT (yet) part of `main` branch).

Checking the contents of your project directory:

```bash
$ tree -L 2
.
├── docs
├── file2.txt
└── src
    ├── file0.txt
    ├── file1.txt
    └── file3.txt
```

Let's move `file2.txt` under `src` directory.

```bash
$ mv file2.txt src
$ tree -L 2
.
├── docs
└── src
    ├── file0.txt
    ├── file1.txt
    ├── file2.txt
    └── file3.txt
```

Check what does git sees:

```bash
$ git status
On branch branch-1
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	deleted:    file2.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	src/file2.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Git sees that `file2.txt` has been deleted from the staging area. It also sees `file2.txt` has been added to `src` (which is not within staging area).

Let's add these changes to staging area.

```bash
$ git add .
```

Note '.' denotes `everything` under the current directory and all sub directories.

Checking git's status.

```
$ git status
On branch branch-1
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    file2.txt -> src/file2.txt
```

Note that git is smart enough to correlate the 2 changes on `file2.txt` and determine as that the file has been renamed (or moved).

We are now happy with on the changes and now telling git to update this batch to the current branch (branch-1).

```
$ git commit -m "Added and relocate files"
[branch-1 3545a9d] Added and relocated files
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename file2.txt => src/file2.txt (100%)
```

Let's check git's log.

```
$ glol
* 3545a9d - (HEAD -> branch-1) Added and relocated files (69 seconds ago) <Ace>
* 3710bfc - Added file3 (12 minutes ago) <Ace>
* 3da5786 - (main) Update 3 files. file3.txt is omitted (4 hours ago) <ace>
* 4176516 - Added file0 (4 hours ago) <ace>
* 8e31a92 - Added file1 (4 hours ago) <ace>
```

Note: `glol` is an alias of `git log --graph --pretty="%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset"`

Now let switch back to `main` branch.

```
$ git checkout main
Switched to branch 'main'
```

We are now on `main`, let's see the log entries from main branch.

```
$ glol
* 3da5786 - (HEAD -> main) Update 3 files. file3.txt is omitted (4 hours ago) <ace>
* 4176516 - Added file0 (4 hours ago) <ace>
* 8e31a92 - Added file1 (4 hours ago) <ace>
```

Notice that currently `main` has no knowledge of changes from branch-1.
Checking the contents of project's directory (and all sub directories), you will see that git has restored the contents back.

```
$ tree -L 2
.
├── docs
├── file2.txt
└── src
    ├── file0.txt
    └── file1.txt

3 directories, 3 files
```

You can switch back/forth between branches and see that the contents are indepedant of each others.

# Merging changes from branches

- You merge changes from other branches into your current branch
- So if your current branch is `branch-1`, then you can merge changes from `main` into `branch-1`
- This also works in reverse, say if you want to merge changes from `branch-1` into `main`, simply switch to `main` then do the merge.
- You can merge changes from multiple (other branches) into the current branch all at once.

In this scenario, let's say we are happy with the experiment we did on `branch-1` and want to integrate these changes into `main`. So we switch our current branch to `main` and do the merge.

```
$ git checkout main
Switched to branch 'main'
```

Now do the merge.

```
$ git merge branch-1
```

Git shows result as:

```
Updating 3da5786..3545a9d
Fast-forward
 file2.txt => src/file2.txt | 0
 src/file3.txt              | 1 +
 2 files changed, 1 insertion(+)
 rename file2.txt => src/file2.txt (100%)
 create mode 100644 src/file3.txt
```

Checking directory's contents.

```
$ tree -L 2
.
├── docs
└── src
    ├── file0.txt
    ├── file1.txt
    ├── file2.txt
    └── file3.txt

3 directories, 4 files
```

This process can be repeated, i.e. more changes made to both `main` and `branch-1` and merge changes between the 2 branches.

# Conflicts!

Normally, git is quite good and handling merging changes automatically. However, conflicts occur when changes occur on the same file from different branches.

Let assume that `file0.txt` was updated on both `main` and `branch-1`. In this case, auto-merge will fail. Git will display this error, for example:

```
$ git checkout main
...
$ git merge branch-1
Auto-merging src/file0.txt
CONFLICT (content): Merge conflict in src/file0.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Checking git status, it is complaining with this message:

```
$ git status
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   file0.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

In this scenario, git cannot determine how to merge changes. It will add `conflict` markers into files with conflicts. For example:

```
$ cat file0.txt
<<<<<<< HEAD                               <<- Conflict marker
file0 - main also updated this line!
=======                                    <<- Conflict marker
file0(zero) - modified from branch-1
branch-1 add extra line - this line
>>>>>>> branch-1                           <<- Conflict marker
```

## Conflict Resolution

Files marked with conflict markers must be manually resolved (edited) first. You resolve conflicts by:

1. Manually edit changes (selectively exclude unwanted chages)
2. Remove conflict markers
3. Add this change to staging area
4. Commit changes from staging area (into current branch)

For example, let's keep everything done on `branch-1` and remove all changes done on `main` for file `file0.txt`. So now, `file0.txt` looks like this after the resolution.

```
file0(zero) - modified from branch-1
branch-1 add extra line - this line
```

Now add this change into staging.

```
$ git add file0.txt
```

Add commit this change from staging to the current branch.

```
$ git commit -m "Resolve conflicts"
```

Let's look at our current log.

```
$ glol
*   d255ebd - (HEAD -> main) Resoved conflict (5 seconds ago) <Ace>
|\
| * 147d00d - (branch-1) Update file0.txt (14 minutes ago) <Ace>
* | b970ecf - Updated file0 (13 minutes ago) <Ace>
|/
* 3545a9d - Added and relocated files (46 minutes ago) <Ace>
* 3710bfc - Added file3 (57 minutes ago) <Ace>
* 3da5786 - Update 3 files. file3.txt is omitted (4 hours ago) <ace>
* 4176516 - Added file0 (5 hours ago) <ace>
* 8e31a92 - Added file1 (5 hours ago) <ace>
```

# Removing branch

When a branch is no longer needed, we can delete it.

```
$ git branch -d branch-1
Deleted branch branch-1 (was 147d00d)
```

Listing all branches. Take note that 'branch-1' is now gone.

```
$ git branch --all
* main
```

Also note the different now when displaying git log.

```
$ glol
*   d255ebd - (HEAD -> main) Resoved conflict (6 minutes ago) <Ace>
|\
| * 147d00d - Update file0.txt (20 minutes ago) <Ace>
* | b970ecf - Updated file0 (19 minutes ago) <Ace>
|/
* 3545a9d - Added and relocated files (52 minutes ago) <Ace>
* 3710bfc - Added file3 (63 minutes ago) <Ace>
* 3da5786 - Update 3 files. file3.txt is omitted (5 hours ago) <ace>
* 4176516 - Added file0 (5 hours ago) <ace>
* 8e31a92 - Added file1 (5 hours ago) <ace>
```

