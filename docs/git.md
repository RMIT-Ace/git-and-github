# Introduction to `git`

- Created by Linus Torvalds in 2005
- Tracking changes to source files
- Tracking who made changes
- The most widely used Source Code Management (SCM)
- Mature and actively maintained
- De Facto standard
- Distributed Version Control System (DVCS)
    - Flexible - support _any_ workflow
- Small and fast 
- Support LARGE repositories
- Data Assurance
- Staging area
- Free and open (source)


# Creating a git project

```bash
$ cd SOME_DIR
$ mkdir my-project
$ cd my-project
$ mkdir -p src docs 
```

Checking directory structure

```bash
$ tree -a -L 1
```

Output

```
.
├── docs
└── src
```

Turn a directory into a git repository.

```bash
$ git init
```

Output

```bash
Initialized empty Git repository in /Users/ace/temp/git-tutorials/my-project/.git/
```

Checking directory structure.

```bash
.
├── .git        <<- Hidden folder for git to use
├── docs
└── src
```

Now `git` can track changes to source files within this folder (a git repository).

# Git's Staging Area


```bash
.
├── .git                     <<- Hidden folder
                                                
    +-----------------+                         
    |                 |                         
    | Git's Repository|                         (3)
    |                 |                          ^
    +-----------------+                          |
                                                 |
    +- - - - - - - - -+                          |
    |                 |                          |
    | Git's Staging   |                         (2)
    | (imaginary)     |                          ^
    +- - - - - - - - -+                          |
                                                 |
├── docs                      \                  |
├── src                       |                  
├── any future direcotory     |- Your work area (1)
├── any future direcotory     |
└── ...                       /

```

1. You make changes to your project
2. You add changes to staging area
3. You update chagnes from staging area to Git's repository

# Note on `.git` Hidden Folder

- Git manages the contents within this folder
- There should be only one and no nested or duplicate `.git` within this project directory
- Directly changing the contents of this folder may permanently damage git repository
- Removing this folder will permanently remove git repository

# Working with your (local) repository

- Rule #1 - do not directly modify `.git` (hidden) folder
- You make changes to files and folders in the work area (any files or folder outside `.git` folder). These changes includes:
    - add, update, or delete files and folders
    - move files and/or folders

Checking for changes.

```bash
$ git status
```

Sample output.

```bash
On branch main
Changes not staged for commit:                                          \
  (use "git add/rm <file>..." to update what will be committed)         | Git's 
  (use "git restore <file>..." to discard changes in working directory) | staging
	deleted:    file0.txt                                               | area
	modified:   src/file1.txt                                           /

Untracked files:                                                        \
  (use "git add <file>..." to include in what will be committed)        | Your working
	file2.txt                                                           | area outside
	src/file0.txt                                                       | the staging
	src/file3.txt                                                       / area

no changes added to commit (use "git add" and/or "git commit -a")
```


- You selectively add (or remove) each change (above) into the staging area.
    - if you change your mind on certain change or changes, they can be removed from the staging area
    - you can even removes all changes from staging area and start a new one from the previous `commit` (see definition of `commit` below)

Add a single change, change to `file0.txt`. In this case, `file0.txt` has been moved from current directory to a directory `src`.

```bash
$ git add file0.txt
```

Sample output:

```bash
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	deleted:    file0.txt                                             ----+
                                                                          |
Changes not staged for commit:                                            |
  (use "git add <file>..." to update what will be committed)              |
  (use "git restore <file>..." to discard changes in working directory)   |
	modified:   src/file1.txt                                             |
                                                                          |
Untracked files:                                                          |
  (use "git add <file>..." to include in what will be committed)          |
	file2.txt                                                             |
	src/file0.txt                                                    <----+
	src/file3.txt
```

Notice, git reports `file0.txt' as being deleted from the current directory and added as a new file under 'src' directory (also note that `src` is currently outside git's staging area).

Add another change to git's staging area. In this case, `file1.txt` has been modified.

```bash
$ git add src/file1.txt
```

Checking git's changes and status.

```
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	deleted:    file0.txt
	modified:   src/file1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	file2.txt
	src/file0.txt
	src/file3.txt
```

To add all changes at once, do:

```bash
$ git add .
```

Checking git's status.

```bash
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   file2.txt
	renamed:    file0.txt -> src/file0.txt
	modified:   src/file1.txt
	new file:   src/file3.txt
```

Let pretend that `file3.txt` is not ready to be committed. We can remove this file from the current git's staging by:

```bash
$ git restore --staged src/file3.txt
```

Checing status again.

```bash
$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   file2.txt
	renamed:    file0.txt -> src/file0.txt
	modified:   src/file1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	src/file3.txt
```

- You tell Git to update it's repository with the contents in the staging area
    - This is a batch update - also called a `commit`
    - Upon successful update, git will give you a unique ID for this commit - this is called `a commit hash`

So, now, we are ready to commit this batch of changes which consists of chabnges to the 3 files (file0.text, file1.txt, and file2.txt). We can tell git to commit this batch as follow:

```bash
$ git commit -m "Updated 3 files. Omitted file3.txt for now"
```

Checking git status

```bash
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	src/file3.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Checking git's log.

```bash
$ git log
```

Git's output:

```bash
commit 3da5786f7250f780a2432cc2f14b73ce356f105f (HEAD -> main)
Author: ace <ace@ADA-1.local>
Date:   Fri Jan 3 10:10:51 2025 +1100

    Update 3 files. file3.txt is omitted

commit 41765161f00e6fd64a2ab9346008540eff4463f3
Author: ace <ace@ADA-1.local>
Date:   Fri Jan 3 09:55:02 2025 +1100

    Added file0

commit 8e31a92144552abe8a89dec4537ae8af8ec5e0a1
Author: ace <ace@ADA-1.local>
Date:   Fri Jan 3 09:46:07 2025 +1100

    Added file1
```

You can reformat git's log for pretty outputs, i.e:

```bash
git log --graph --pretty="%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset"
```

A prettier output:

```bash
* 3da5786 - (HEAD -> main) Update 3 files. file3.txt is omitted (4 minutes ago) <ace>
* 4176516 - Added file0 (20 minutes ago) <ace>
* 8e31a92 - Added file1 (29 minutes ago) <ace>
```

