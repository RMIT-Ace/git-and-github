# XCode and git

Let's start with a project with this directory structure below.
The present of `.git` (hidden) folder implies that this directory and all its sub directories are under a git repository.

```
.
├── .git            <- This is a git repo.
├── docs
└── src
    ├── file0.txt
    ├── file1.txt
    ├── file2.txt
    └── file3.txt
```

Create new Xcode project.

![Xcode New Project](images/xcode-new-prj.jpg)


![Xcode Project Location](images/xcode-prj-location.jpg)

Checking directory structure.

```
└── src
    ├── file0.txt
    ├── file1.txt
    ├── file2.txt
    ├── file3.txt
    └── xcode-git-demo                \
        ├── xcode-git-demo            | Xcode's project folder
        └── xcode-git-demo.xcodeproj  /
```

Xcode allows a NEW git repository to be created upon creating a new project.
However, if this new Xcode project is to be a part of an existing git repository, this step should be skipped - it is not recommended nesting .git repository.

![Xcode Init Git](images/xcode-init-git.jpg)

```
└── src
    ├── file0.txt
    ├── file1.txt
    ├── file2.txt
    ├── file3.txt
    ├── xcode-git-demo
    │   ├── xcode-git-demo
    │   └── xcode-git-demo.xcodeproj
    └── xcode-git-demo2
        ├── .git                      <<- Nested .git - not recommended
        ├── xcode-git-demo2
        └── xcode-git-demo2.xcodeproj
```

To keep our tutorial tidy, we will remove this Xcode project `xode-git-demo2`.

Let checks Xcode's features that support git operations.

![Xcode Init Git](images/xcode-file-explorer.jpg)

![Xcode Source Navigator & Git](images/xcode-src-nav.jpg)

![Xcode Git Integration](images/xcode-git-integration.jpg)

![Xcode Stage Changes](images/xcode-stage-changes.jpg)

![Xcode Uncommitted Changes](images/xcode-uncommitted-changes.jpg)

Committing changes requires brief description.

![Xcode Commit Changes](images/xcode-git-commit.jpg)

![Xcode Git Branches Browser](images/xcode-git-branches.jpg)

See who made what changes and when, etc.

![Xcode Changes & Authors](images/xcode-git-authors.jpg)

![Xcode Stage Change](images/xcode-stage-single-change.jpg)

![Xcode Staged vs. Unstagged](images/xcode-stage-unstagged.jpg)

![Xcode Changes & Authors (2)](images/xcode-git-authors2.jpg)

# Git Ignore File (.gitignore)

Some files should not be included into git repository. For example:

- `.DS_Store`
- `*.xcuserstate`

![Xcode Git Ignore](images/xcode-git-ignore.jpg)

Solution: Add `.gitignore` file to project top-level directory.
This file contains 2 lines as shown below.

```
.DS_Store
*.xcuserstate
```

Optional - remove ignore files which have already been added to git.

```
$ git rm --cached path/to/.DS_Store
$ git rm --cached *.xcuserstate
```

Now add this new `.gitignore` file to your git repository.

```
$ git add .gitignore
$ git commit -m "Added git ignore file"
```

Now, notice when changing Xcode editor's configuration, Xcode stops reporting these changes as git changes.
