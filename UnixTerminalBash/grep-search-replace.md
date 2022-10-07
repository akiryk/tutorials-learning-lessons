```sh
# search for a word in a file
grep "something" ./some-file.txt

# case insensitive
grep "thing" -i ./some-file.txt

# grep from curl
curl -v --stderr - https://www.gutenberg.org/cache/epub/69102/pg69102.txt | grep "website" -i
```

Search for all files in a directory that include a word
and output name of the files into a txt file

* `grep -r -c 'Lnrs key=' * > ~/Desktop/temp.txt`

In VS Code, replace all empty lines
* use  edit > replcae
* select the regular expression search
* in find: `^(\s)*$\n` 
* in replace: nothing

