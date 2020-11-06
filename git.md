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
