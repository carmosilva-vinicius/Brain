Here are the minimal required to command line interface in a [[Linux]] operational system.
# File content view
### cat, more and less

`cat`, `more`, and `less` are commands used for viewing the contents of a file. Each has unique features that make them more suitable for certain tasks.
- `cat` It is commonly used to have a quick view of small files. It outputs the full content of the file to the terminal without any way to scroll up or down, so for large files, it is not that convenient. You can also use for file creation, concatenation, appending, displaying line numbers, squeezing blank lines, and showing non-printing characters..
- `more` is a medium navigator. It is better than `cat` for viewing large files as it supports **forward navigation**. It displays the file contents one screenfull at a time, and you can scroll through the contents of the file using the Enter key, one line at a time, or the Space bar, page by page.
- `less` is a full-featured experience and has more features compared to `more`. It supports both forward and backward navigation, which makes it best for viewing large files. It also supports line numbers, searching strings, marking positions, and viewing multiple files. It starts up faster compared to text editors, especially when viewing large files.

```zsh
cat /etc/ssh/ssh_config
less /etc/ssh/ssh_config
more /etc/ssh/ssh_config
```

In conclusion, `cat` is a good tool for having a quick overview of short files, `more` is better for viewing large files and supporting forward navigation, and `less` is a feature-rich and advanced version of `more` command. Less has better performance, once that it use **streams** to read the content, while the other two load all the content in memory.

### tail
Print  the  last  10  lines of each FILE to standard output. It is commonly used to view the end of a log. 
Options:
- -f, --follow[={name|descriptor}]
	This allows you to be appended in file and output the data while the files is growing;
- -n, --lines=[+]NUM
    output a specific number of end lines from the file

# Pipe
Pipes are used to create interactions between two ore more commands. It works connecting the standard output of a command in a standard input the follow one.
```zsh
command_1 | command_2 | command_3 | .... | command_N
```

###### Example:
Use the `ls` command to list all files in the current directory and pipe its output to the `grep` command to search for a specific filename and then pipe the output to the `sort` command to sort the output:
```zsh
ls | grep "filename.txt" | sort
```
