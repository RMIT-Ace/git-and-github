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
