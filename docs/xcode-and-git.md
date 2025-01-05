# XCode and git

```
.
├── .git
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
    └── xcode-git-demo
        ├── xcode-git-demo
        └── xcode-git-demo.xcodeproj
```

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

![Xcode Init Git](images/xcode-file-explorer.jpg)

![Xcode Source Navigator & Git](images/xcode-src-nav.jpg)

![Xcode Git Integration](images/xcode-git-integration.jpg)

![Xcode Stage Changes](images/xcode-stage-changes.jpg)

![Xcode Uncommitted Changes](images/xcode-uncommitted-changes.jpg)

![Xcode Commit Changes](images/xcode-git-commit.jpg)