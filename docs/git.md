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
