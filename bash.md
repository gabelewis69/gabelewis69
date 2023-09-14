Eepy so fuckin eepy just wanna eep
Student Guide 
https://cted.cybbh.io/tech-college/pns/public/pns/latest/guides/bash_sg.html
___________________________________________________________________________________________________
GALE-M-507


Bash Day 1

The Bourne Again Shell

Linux FileSystem 
 - Absolute/relative/home path
 - File Manipulation Commands (touch mkdir, rm, rmdir, ls, cd, pwd, cp, mv)
 - Link Files (Symbolic/soft an Hard Links)
Processes and Memory (ps, kill, killall, pkil, top)
Commands: Cat, More or Less
Finding Filesw and Directories (locate, whereis, which, find)
Commands: grep and cut
SHELL - A shell is a macro processor that executes commands
1. Command interpreter (interactive)
2. Programming language
ctrl+a brings cursor back to the beginnig
ctrl+e goes to the end of the line
ctrl+u erases the line
ctrl+c starts a new line
ctrl+r search bar
ctrl+l clear
Man
- shift+g will go to the bottom of the man pages
- g will go to the top
- / searches in the man page
- n goes to next existence of the search value
- shift+n will bring you to the previous one
- linux.die.net/man is a website that you can use
pwd prints working directory

Symbolic Link
touch file
ln -s file symfile and ln -s file symlink is a symbolic link between the two to file
if file is deleted the link stops working, but symbolic link works across multiple machines

Hard Link
touch file
ln file hardlinkfile
If file is deleted the hardlink file will not stop working, builds persistence

Find
Find is an extremely important portion of bash because we need it for everything
by default find will search starting with root
find is case sensitive 
find $home -name new.sh
./new.sh
touch NEW.sh
find $home -iname new.sh is the case insensitive version and should be used by default
find -size just finds the file based off of size, kinda useless
find / -group root is finding anything in the root directory with the permissions of root or in the root group
-maxdepth will find only what is the limited numbers of directories deep
-exec is finds way of a pipe 
find / -type <d f p l>
d for directory, f for file, p for pipe, l for symbolic links
find / -type d -iname log | ls -l {} \; 2>/dev/null
find / -atime 1 will find the last day accessed by a file with -ctime created -mtime modified
find / -mmin 30 is the same as time but with minutes
find / -executable ! -type d will find executable files
find /var/log -iname *.log 2>/dev/null -printf "%i %f\n" | more this finds all case insensitive .log files %i is inode number and %f is file name

grep
You can utilize grep to compare files
-C specifies how manyh lines you want to see
using grep -v inverts the result, so shows all the not matches
grep 'root' /etc/passwd
grep 'root' -A3 /etc/passwd which shows 3 lines after, B is before, and C is context
egrep allows us to input regex as a string
cat /etc/passwd | egrep -o "/home.*" without the "" and .* then it would only return /home/
egrep "student|root|ROOT: /etc/passwd

touch file{1..5} will create file1, file2, so on and so forth
this works with files, directories, pretty much anything

ps aux will show all processes on the system and who is running them

cut
relies on a character deliminator and cut itself will work on a tab, we can change the deliminator usually with the first option
tail /etc/passwd | cut -d: -f1
the -f stands for field, in this case showing the first field
the -s only shows the lines that match the delimiter

