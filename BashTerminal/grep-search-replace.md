
## Resources
https://www.youtube.com/watch?v=VGgTmxXp7xQ decent intro to the basics

## Basics
```sh
# search for a word in a file
grep "something" file.txt

# case insensitive
grep "thing" -i file.txt

# -w
# search only for the word (find "Eve" not "Evening")
grep "eve" -i -w names.txt

# -n 
# show me where by line number 
grep "eve" -n names.txt

# Combine arguments
grep "eve" -win names.txt

# pass arguments to arguments
# show 2 lines before and 2 lines after each result
grep "ede" -iwn -B 2 -A 2 names.txt

# Better yet, use -C
grep "ede" -iwn -C 2 names.txt

# Search everying in current directory, use wildcard
grep "what" -in ./*

# search in current directory AND subdirectories with -r 
# no need for the slash
grep "what" -winr .
```

## Piping with Curl
```sh 
# grep from curl
curl -v --stderr - https://www.gutenberg.org/cache/epub/69102/pg69102.txt | grep "website" -i

# pipe json to nice format
curl -v --stderr - https://www.gutenberg.org/cache/epub/69102/pg69102.txt | python3 -m json.tool
```

Search for all files in a directory that include a word
and output name of the files into a txt file

* `grep -r -c 'Lnrs key=' * > ~/Desktop/temp.txt`

In VS Code, replace all empty lines
* use  edit > replcae
* select the regular expression search
* in find: `^(\s)*$\n` 
* in replace: nothing

