# Lecture 4 Data Wrangling
[Lecture notes](https://missing.csail.mit.edu/2020/data-wrangling/)

**`wc`** returns the word count of the input. It returns the line, word and character count by default. `l`, `w` or `c` can be used for returning lines, word or character count respectively. `m` returns the number of characters by taking multiline characters into account. 

**`sort`** can be used to return sorted line from the input. `r` can be used for reverse, `n` for sorting numbers, `f` for case insensitive search, `u` only returns unique entries and `k` can used to specify a field or range of fields for sorting. `t` can also be used to specify a custom delimiter for the fields.

**`uniq`** can be used to return the unique entries in an input. It provides the unique entries in a file and also the number of occurrences.

**`paste`** command can be used to merge multiple lines with or without a delimiter. It can be used to merge multiple files horizontally to create a tabular data structure or append horizontally

**`bc`** or Basic Calculator can be used to perform quick arithmetic in the shell.

**`-`** can be used to convert STDIN and STDOUT to arguments. 