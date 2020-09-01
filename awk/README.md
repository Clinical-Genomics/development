# AWK - A basic tool to find and attack
Maybe you already know what awk is, and what it is capable of doing, but IF you don't then here is a short introduction to this tool convenient tool. 

AWK (a.k.a. gawk) is a very basic tool able to search through lines of text, identifying user defined patterns. Upon finding the user defined pattern, awk allows for easy reformatting of found texts into a stdout. As awk is a scripting language included in POSIX and Single Unix, one can always count on that the language is usable on every modern distro of Unix.

## How does one talk the awk?
Awk was released in the 1980's and has been widely used since then. Hence, there are many good guides to learning awk. This guide will only briefly touch this tool but here is a more comprehensive guide [here][awk_manual] for those who want to delve even further into awk.

As awk is implemented in Unix it can be directly used on the CLI, but wether you would like to make a script.awk or use awk as oneliner CLI, is up to your own choosing.

The very basis of awk is that you give the tool a pattern, and on that pattern you perform a action.


```shell
$ cat intro.awk
##!/bin/bash

pattern_1 { action }
pattern_2 { action }
```

The execution of intro.awk on a text file will thus first look in line one for pattern\_1, and then if found perform 'action'. Sequently, awk will look for pattern\_2 and if found perform 'action'.

The action performed can either be additions of sorts, but very often awk is used to reformat the output of text files. For instance, in 'random\_data.csv' below we have one line of nonsense in the data. This is where awk shines, with its relatively simple syntax: 

```shell
foobar$ cat random_data.csv
nonsense	1	3
good_data	4	5
good_data	6	7
foobar$ awk -F '\t' '$0 !~ /nonsense/ { print $0 }' random_data.csv

good_data	4	5
good_data	6	7
```

Woah?! What happened there? ... No, awk is not a very flashy tool, but the work it does is done very quick and with arguably little effort into the scripting.

By default, awk uses blankspaces as the field separator. Above the `-F` flag was used, specifying that `random\_data.csv` is tab-separated. 

`$0` is a pointer to the current line that awk is reading. Thus, the 'action' print is carried out IF the line fulfills the logical expression or 'pattern'. The logical expressions used in awk are: 'AND', 'OR', 'EQUAL TO', 'CONTAINS', and 'NOT', written as '&&', '||', '==', '~', and '!' in awk. Using these expressions in combinations enables the user to filter their text properly.

In this case, the line is skipped if it contains the word nonsense, due to negating using `!~`. Awk is also able to check if the entry is equal to something by specifying '==' instead of '~'. 

However, if you know that nonsense is only in the first column, awk allows you to check that in a 1-based indexing system (created from the specified field-separator).

```shell
foobar$ awk -F '\t' '$1 !~ /nonsense/ { print $0 }' random_data.csv

good_data	4	5
good_data	6	7
```

This also means that by using the fields we can extract specific data, in this case below we want that 'good\_data'

```shell
foobar$ awk -F '\t' '$1 == /good_data/ { print $1 }' random_data.csv

good_data
good_data
```

or changing the order of field 2 and 3:

```

foobar$ awk -F '\t' '$1 == /good_data/ { print $1, $3, $2 }' random_data.csv

good_data	5	4
good_data	7	6
```

In some cases you might want to perform an action at the beginning or at the end of an awk script. For instance, maybe you want to get a number for the number of rows where there is good data. This action is then performed by the BEGIN and END sections of the awk script. They are in turn only executed once, so for instance you can declare a variable to increment in the BEGIN section, and print it in the END section:

```shell
$ foobar$ awk -F '\t' awk 'BEGIN { c = 0 }; $1 ~ /good_data/ { c++ }; END { print 'The number of rows with good data is: 'c }' random_data.csv

The number of rows with good data is: 2
```

This is just a taste of the possibilities of using awk, and I strongly recommend people to try it out for themselves!

[awk_manual]: https://www.gnu.org/software/gawk/manual/gawk.html
