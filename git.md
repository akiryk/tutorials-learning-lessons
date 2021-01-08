# Git

### Tips 'n tricks
```sh
# Show only the names of files that have been deleted
git diff master --diff-filter=D --summary

# have been modified
git diff master --diff-filter=M --name-only

# have been re-named
git diff master --diff-filter=R 

# Show only commits authored by an author
git log --author akiryk
```

### Copy directory from one repo to another
This will enable copying a directory from one repo to another so that you maintain git history.
Assume you want to move a directory called `src` from repo-a to repo-b and you want to leave in place all the other content in both repos.

Example directory structure of your two repos. **Goal:** move the files in `repo-a/resources/components` to `repo-b/app/src` and keep thei git history.
```sh
# repo-a
repo-a
  resources
    components
      file-a.js
      file-b.js
      file-c.js
  otherstuff
  ...
  
# repo-b
repo-b
  app
    src
  data
  important-stuff
  ...
```

**Alert** There's an older way of doing this that uses `git filter-branch --subdirectory-filter`. This works fine with small, simple repos, but is unusably slow with large, complex repos. 

Prerequisite. Install [git-filter-repo](https://github.com/newren/git-filter-repo). There are various ways to do this, but an easy way is with homebrew:
```sh
brew install git-filter-repo
```

#### tldr;
```sh
# repo-a
git checkout -b filtered-branch
# filter out everything but what is in components directory
git filter-repo --subdirectory-filter resources/components --force
# move components files to new directory
mkdir -p app/src
git mv -k * app/src
# in repo-b
git checkout -b new-branch
git remote add origin-repo-a ../repo-a
# link to local repo-a's filtered branch and pull
git fetch origin-repo-a filtered-branch
git merge origin-repo-a/filtered-branch --allow-unrelated-histories
git commit
```

1. In repo-a, checkout a new branch and filter out all but the content we want to keep.
```sh
cd repo-a
git checkout -b filtered-branch

# optionally remove git link for security
git remote rm origin

# Remove everything but the components directory
# The old way: git filter-branch --subdirectory-filter resources/components -- --all
# Use the git-filter-repo way:
# --force may not be necessary, but you may need it. git-filter-repo uses various tactics 
# to make clear its actions are destructive.
# This will move all files in components to a new directory called 'src' and will 
# replace all tags with the 'new-module' tag.
git filter-repo --subdirectory-filter resources/components --force

# You will now how a new directory structure for repo-a:
# repo-a
#   file-a.js
#   file-b.js 
#   file-c.js

# Create a new directory in repo-a that maps to the directory in repo-b.
mkdir -p app/src

# copy the filtered files into app/src 
git mv -k * app/src
```

2. In repo-b, create a new branch, link it to the local repo-a 
```sh
cd ../repo-b
git checkout -b new-branch
git remote add origin-repo-a ../repo-a

# Fetch repo-a filtered-branc and merge
git fetch origin-repo-a filtered-branch
git merge origin-repo-a/filtered-branch --allow-unrelated-histories
git add .
git commit -m 'add directory-a'
```
