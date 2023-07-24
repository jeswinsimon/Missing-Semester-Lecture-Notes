# Lecture 2 - Shell Tools and Scripting
[Lecture notes](https://missing.csail.mit.edu/2020/shell-tools/)

## Single quotes(') vs Double quotes(") in shell

Strings enclosed in single quotes are treated as literals, and the shell does not interpret any special characters within them. Everything inside the single quotes is preserved as-is, and variables or command substitutions are not expanded.
```
A='Hello'
echo '$A World
```
Running the above returns `$A World`. whereas double quotes allow for variable expansion and command substitution. The shell will interpret special characters within the double quotes and replace variables with their values. `echo "$A World` would return `Hello World`.

**`!!`** can be used to repeat the last command executed in the shell.

## `$`

**`$@`** returns all the variables passed as arguments. The arguments are returned as separate words in the same order as they are passed to the script. `$*` also returns the list of arguments but as a single string separated by spaces (The arguments are separated using the first letter of the Internal Field Separator(IFS) which is set to space by default).

**`$0`** returns the name of the command or the script which was executed.

**`$1..n`** returns the argument passed at the corresponding index.

**`$#`** returns the number of arguments passed to the script.

**`$$`** returns the Process ID(PID) of the current shell and `$!` returns the PID of the last background process that was executed.

**`$?`** returns the exit status of the last executed command. It is usually **0** for success and non-zero for failure.

**`$_`** returns the last argument of the previous command.

## Logical operators

Multiple commands passed in a single go by terminating each command with a `;`. In this case, the commands are sequentially executed one after the other.

Commands can also be chained using the Logical OR (`||`) or the Logical AND (`&&`) operators. When chained using `;` all commands are executed irrespective of the success or failure of the previous command whereas when chained using `&&` a command is executed only if the previous command succeeds and when chained using `||` a command is executed only if the previous command fails.

**`/dev/null`** is a special device file in Unix systems that acts as a null device. The primary purpose of `/dev/null`` is to discard unwanted output or to provide a convenient way to redirect data to nothingness. It is commonly used in shell scripts or command-line operations to suppress output or to discard data that is not needed.

## Wild cards

**`?`** is used for single character substitution

**`*`** is used for multi character substitution

**Brace expansion** s used to generate multiple strings based on the patterns enclosed within the braces. The result of brace expansion is a comma-separated list of strings, where each string is a combination of the patterns inside the braces.

```
echo project{1,2}
```
will echo `project1 project2`.

The values inside `{}` can be comma separated values or even a range like `{1..5}` or `{a..f}`.

**Process substitution** allows to use the output of a command as input or argument to another command, treating it as if it were a file. It provides a way to bridge the gap between commands that expect file inputs and commands that generate data dynamically. Process substitution is denoted by the `<(...)` syntax.

For example, `diff` command expects two files as input, we can compare the files in two directories by using process substitution on the `ls` command.

```
diff <(ls foo) <(ls bar)
```

Output substitution(`(...)>`) can also be used to capture the output of a command and use it as input to another command or program that expects input from a file.

## Other shells

The **shebang** or **hashbang** is the optional first line of a shell script that starts with `#!` and specifies which interpreter to be used for running the script. The `#!` is followed by the path of the interpreter. Use `/bin/sh` for using the default shell.
```
#!/bin/bash
```

`/usr/bin/env` will fetch the path of the shell from the available PATHs same as what happens when a command is executed directly in the shell. It can be used to make the path dynamic. `/usr/bin/env python` will execute the command using `python` found in `PATH`.

## Useful command line tools

**`shellcheck`** is a static analysis tool for checking the syntax of shell scripts.

**`rg`** or **ripgrep** a line-oriented search tool similar to grep but optimised for speed and ease of use. rg is designed to quickly search through large codebases and directories to find matching patterns in text files.

**`tldr`** provides simplified and concise versions of `man` pages.

**`find`** command allows to search for files and directories based on various criteria. It recursively traverses a directory tree starting from a specified location and searches for files and directories that match the specified criteria. There is an `-exec` option that allows you to run commands on searched files.

**`locate`** can also be used to quickly search for files and directories based on their filenames. `find` does a realtime search whereas `locate` uses a pre-built database, which is regularly updated, to find files quickly. 

**`ls -R`** can be used to recursively list all the contents of a directory and its sub directories.

**`broot`** is a file manager and directory management tool that can be used as an alternative to `ls`. `nnn` is another alternative. `fd` is an interactive alternate.

***`tree`*** command can be used to display the contents of a directory in a tree-like format. 
