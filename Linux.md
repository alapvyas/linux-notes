### Find vs Locate:
There are two main commands to locate files and directories in Linux. The `find` command in Linux is a versatile tool for searching files and directories based on various criteria, such as name, type, and size, with results generated in real-time. The `locate` command, on the other hand, is a faster option that relies on a pre-built database for quick file searches but may not provide real-time updates.

**Find**: To find a file name "Translators" for instance within one of the directories from the current working directory, you'd use the following command.

```bash
  find . -name "Translators"

```
Here, . refers to the current working directory.

**Locate**: You can use the following command to find the same file.

```bash
  locate Translators

```
If this command doesn't work, make sure you have the mlocate package installed. If it is already installed, use `updatedb` and then try again.

### Wildcards: 
Wildcards are useful in many ways for a GNU/Linux system and for various other uses. Commands can use wildcards to perform actions on more than one file at a time, or to find part of a phrase in a text file. There are many uses for wildcards, there are two different major ways that wildcards are used, they are globbing patterns/standard wildcards that are often used by the shell. The alternative is regular expressions, popular with many other commands and popular for use with text searching and manipulation.

[Standard Wildcards and Regular expressions](https://tldp.org/LDP/GNU-Linux-Tools-Summary/html/x11655.htm)
