# Lecture 1 - Course overview + the shell
[Lecture notes](https://missing.csail.mit.edu/2020/course-shell/)

All available shells are listed in the `/etc/shells`, they can be listed by running

```
cat /etc/shells
```

Names can either be included in quotes or `\` can be used to escape space in names.

```
cat "hello world.txt"
cat hello\ world.txt
```

The `/etc` directory in Unix-like operating systems serve as a central location for configuration and system-related administrative files. 

## Shell vs Terminal

A **shell** is a command-line interface (CLI) program that interprets user commands and executes them on the operating system. It acts as an intermediary between the user and the operating system, providing a way to interact with the system through text-based commands. The shell takes input from the user, interprets and executes the commands, and displays the output. Examples of Unix shells include Bash, Zsh, and Fish.

A **terminal**, also known as a terminal emulator, is a software application that provides a graphical interface for interacting with a shell. It emulates the behaviour of a physical computer terminal and allows you to enter commands and see their output. The terminal provides an environment for running the shell and displaying the command-line interface. It includes features like text display, keyboard input, and support for multiple shell sessions or tabs. In modern systems, the terminal is typically a window or a tab within a graphical user interface (GUI) application. Examples includes Terminal on Mac OS, and Windows Terminal on Windows.

A **shell prompt**, also known as a command prompt or command line prompt, is a specific text string displayed in a shell or terminal to indicate that the shell is ready to receive user commands. It typically appears as a fixed cursor or marker at the beginning of the input line, waiting for the user to enter a command.

The shell prompt usually includes information such as the current working directory, the user's username, the hostname of the machine, and sometimes additional contextual information. The format and appearance of the prompt can vary depending on the shell and its configuration.

**Environment variables** in a shell are named values that can affect the behaviour and configuration of the shell and its associated programs. They are part of the shell's environment and provide information or settings that can be referenced or modified by shell scripts and commands.

## Global Variables

Environment variables can be listed using the `env` command.

**`$PATH`** variable stores a list of directories where the shell searches for executable programs. **`$SHELL`** indicates the current shell. **`$USER`** stores the current user's name and **`$HOME`** stores the current user's home directory.

`which` command returns the path where the program resides.

`cd -` changes the active directory to the previous directory. The current and previous directories are stored in environment variables as `$PWD` and `$OLDPWD`. PWD Stands for **P**rint **W**orking **D**irectory.

Environment variables can be set for the current session by using `export`. If the variable is required only for a single command, it can be set by prepending the command with the variable.

```
export NODE_OPTIONS=--max_old_space_size=4096
```
```
NODE_OPTIONS=--max_old_space_size=4096 npm run dev
```

Environment variables can be permanently set by adding them to the corresponding shell configuration file (`.zshrc` in case of zsh and `.bashrc` in case of bash). Launch a new shell or reload the configuration file using `source` command for the changes to take effect.

## `source` and `export`

Whenever a program is normally executed in a shell, the shell creates a child process and executes the program in that context. But when a program is executed using `source`, the program is executed in the same process. One of the differences here is that any variable created in the program is available in the shell even after execution when using `source` whereas it isn't otherwise. 

#### `var.sh`
```
A="This is a var"
```
Running `source var.sh` will have the same effect as directly setting the variable A on the shell using `A="This is a var"` whereas executing `var.sh` directly using `./var.sh` will not make A available to the parent process. 

Setting a variable to a shell does not make it available to the child processes. The variable `A` set above will only be available in the current shell and not within the child processes. 

#### `print-var.sh`
```
echo $A
```

In this case, running `./print-var.sh` will return empty since `A` is not available to the child process. 

`export` command can be used to set variables that are accessible by the child processes. Running `export A="This is a var"` sets the variable as an environment variable and will be copied on to the child process created during a program execution. 

#### `env-var.sh`
```
export A="This is a var"
```
Environment variables will only be copied from parent to child and not vice versa. So running the above normally will only set the environment variable to the child process and will be lost after the execution. Running `source env-var.sh` will set this variable `A` as an environment variable in the shell instance.

```
echo export NODE_OPTIONS=--max_old_space_size=4096 >> .zshrc
source .zshrc
```

The `.(zsh|bash)rc` configuration file contains all the environment variables to be set when a shell instance is loaded. In the above snippet `echo export NODE_OPTIONS=--max_old_space_size=4096 >> .zshrc` appends the `NODE_OPTIONS` environment variable to the `.zshrc` file. This new environment variable will be available in a new shell instance. And if you want the updated environment variable in the current shell instance, running `source .zshrc` causes all the environment variables from `.zshrc` to be reloaded in the current instance. 


## Input and output

**Input Stream**, also known as standard input (stdin), is a source of data that is fed into a command-line program. It provides a way for the program to receive input from the user or from other sources.

**Output Steam**, also known as standard output (stdout), is the default destination for a program's normal output. It is where the program sends its regular output or information.

**Error Stream**, or the standard error stream (stderr), is used by programs to output error messages and diagnostic information. It is where the program sends error output or any messages that indicate issues or exceptions.

A program usually takes input through arguments, input stream or both. The output is usually through output stream or error stream. By default the input stream is connected to the keyboard and both output and error streams are connected to the console. They can be redirected using `<`or `>` operator.

Input to a program can be redirected using the `<` operator.
```
cat < hello.txt
```

Output can be redirected using the `>` operator.
```
cat > hello.txt
```
`>` Overwrites the file if it already exists whereas using `>>` instead will append to the end of the file. `>` only redirects stdout, use either `&>` to redirect both stdout and stderr to the same destination or `2>` to redirect only stderr to a different destination.

Output from one command can be used as input to another command by using the `|` (pipe) operator.

`tee` command can be used to read from standard input and write to both standard output and files simultaneously. 

```
drwxr-xr-x   5 jeswinsimon  staff   160 Jul 19 19:58 missing-semester-notes
```
In the above sample output of `ls -l`, the first character is used to indicate whether it is a file, directory or a stream, the rest of the characters indicate permissions for owner, group and others respectively. 

The `du` or disk usage command can be used to find the size of a file. `-s` flag can be used to get the size of the entire directory and `-k/m/g` can be used to display the size in KB, MB or GB respectively.
