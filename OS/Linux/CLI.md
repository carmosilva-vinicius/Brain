Here are the minimal required to command line interface in a [[Linux]] operational system.
#### [Top 50 Linux Commands You Must Know as a Regular User](https://www.digitalocean.com/community/tutorials/linux-commands#top-50-linux-commands-you-must-know-as-a-regular-user)
1. **ls** - The most frequently used command in Linux to list directories
2. **pwd** - Print working directory command in Linux
3. **cd** - Linux command to navigate through directories
4. **mkdir** - Command used to create directories in Linux
5. **mv** - Move or rename files in Linux
6. **cp** - Similar usage as mv but for copying files in Linux
7. **rm** - Delete files or directories
8. **touch** - Create blank/empty files
9. **ln** - Create symbolic links (shortcuts) to other files
10. **cat** - Display file contents on the terminal
11. **clear** - Clear the terminal display
12. **echo** - Print any text that follows the command
13. **less** - Linux command to display paged outputs in the terminal
14. **man** - Access manual pages for all Linux commands
15. **uname** - Linux command to get basic information about the OS
16. **whoami** - Get the active username
17. **tar** - Command to extract and compress files in Linux
18. **grep** - Search for a string within an output
19. **head** - Return the specified number of lines from the top
20. **tail** - Return the specified number of lines from the bottom
21. **diff** - Find the difference between two files
22. **cmp** - Allows you to check if two files are identical
23. **comm** - Combines the functionality of diff and cmp
24. **sort** - Linux command to sort the content of a file while outputting
25. **export** - Export environment variables in Linux
26. **zip** - Zip files in Linux
27. **unzip** - Unzip files in Linux
28. **ssh** - Secure Shell command in Linux
29. **service** - Linux command to start and stop services
30. **ps** - Display active processes
31. **kill and killall** - Kill active processes by process ID or name
32. **df** - Display disk filesystem information
33. **mount** - Mount file systems in Linux
34. **chmod** - Command to change file [[Permissions]]
35. **chown** - Command for granting ownership of files or folders
36. **ifconfig** - Display network interfaces and IP addresses
37. **traceroute** - Trace all the network hops to reach the destination
38. **wget** - Direct download files from the internet
39. **ufw** - Firewall command
40. **iptables** - Base firewall for all other firewall utilities to interface with
41. **apt, pacman, yum, rpm** - Package managers depending on the distro
42. **sudo** - Command to escalate privileges in Linux
43. **cal** - View a command-line calendar
44. **alias -** Create custom shortcuts for your regularly used commands
45. **dd** - Majorly used for creating bootable USB sticks
46. **whereis** - Locate the binary, source, and manual pages for a command
47. **whatis** - Find what a command is used for
48. **top** - View active processes live with their system usage
49. **useradd and usermod** - Add new user or change existing users data
50. **passwd** - Create or update passwords for existing users
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
