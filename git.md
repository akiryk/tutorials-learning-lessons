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

Directory structure of your two repos
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

1. Clone repo-a and repo-b, then create a new branch in repo-a and filter out all content but the directory we want to copy over, in this case, `components`. 
```sh
git clone https://github.path.to/repo-a tmp-repo
git clone https://github.path.to/repo-b
cd tmp-repo
git checkout -b filtered-branch 

# Remove everything but the components directory
git filter-branch --subdirectory-filter resources/components -- --all

# The above will show a warning which you can ignore since you aren't concerned with preserving tmp-repo.
# (to be extra careful, you could run git remote rm origin before filtering)

```

You will now how a new directory structure for repo-a:
```sh
```sh
# repo-a
repo-a
  file-a.js
  file-b.js 
  file-c.js
```

2. Create a new directory in repo-a that maps to the directory in repo-b.
```sh
# create app/src in repo-a
cd repo-a
mkdir -p app/src

# copy the filtered files into app/src 
git mv -k * app/src`
```

3. Move to repo b, create a new branch, and link it to the local tmp-repo
```sh
cd ../repo-b
git checkout -b new-branch
git remote add origin-tmp-repo ../tmp-repo
```

4. Fetch the tmp-repo's branch and then merge with the all-unrelated-histories flag
```sh
git fetch origin-tmp-repo filtered-branch
git merge origin-tmp-repo/filtered-branch --allow-unrelated-histories
``
