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

Step 1. Install [git-filter-repo](https://github.com/newren/git-filter-repo). There are various ways to do this, but an easy way is with homebrew:
```sh
brew install git-filter-repo
```

1. Clone repo-a and repo-b, then create a new branch in repo-a
```sh
git clone https://github.path.to/repo-a tmp-repo
git clone https://github.path.to/repo-b
cd tmp-repo
git checkout -b filtered-branch 
```

2. Filter out all content but the directory we want to copy over, in this case, `components`. 
```sh
# in repo-a
# Remove everything but the components directory
# The old way: git filter-branch --subdirectory-filter resources/components -- --all
# Use the git-filter-repo way:
# --force may not be necessary, but you may need it. git-filter-repo uses various tactics to make clear its actions are destructive.
# This will move all files in components to a new directory called 'src' and will replace all tags with the 'new-module' tag.
git filter-repo --subdirectory-filter resources/components --force
```

You will now how a new directory structure for tmp-repo (repo-a):
```sh
tmp-repo
  file-a.js
  file-b.js 
  file-c.js
```

3. Create a new directory in tmp-repo that maps to the directory in repo-b.
```sh
# create app/src in tmp-repo (repo-a)
cd tmp-repo
mkdir -p app/src

# copy the filtered files into app/src 
git mv -k * app/src`
```

4. Move to repo b, create a new branch, and link it to the local tmp-repo
```sh
cd ../repo-b
git checkout -b new-branch
git remote add origin-tmp-repo ../tmp-repo
```

5. Fetch the tmp-repo's branch and then merge with the `--allow-unrelated-histories` flag
```sh
git fetch origin-tmp-repo filtered-branch
git merge origin-tmp-repo/filtered-branch --allow-unrelated-histories
git add .
git commit -m 'add directory-a'
```
