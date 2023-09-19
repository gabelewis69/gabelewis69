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
find / -atime 1 will find the last day accessed by a file with -ctime created -mtime modified Goes by day, ie the 1 means 1 day
find / -mmin 30 is the same as time but with minutes
find / -executable ! -type d will find executable files
find /var/log -iname *.log 2>/dev/null -printf "%i %f\n" | more this finds all case insensitive .log files %i is inode number and %f is file name
MAC - Modified Accessed Changed
-exec COMMAND -OPTIONS {} /; #execute COMMAND against every object (think foreach)
-exec COMMAND -OPTIONS {} + #execute COMMAND against everything all at one

tar -c create
    -v verbost
    -f file
    -z gzip

wc -l

delete
     rm - delete files
     rmdir - delete directories

touch
      -d "2020-09-19 09:00:00" File 💯
      -t [[CC]YY]MMDDhhmm[.ss]

kill
pkill
kill -9
killall

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
cat /etc/passwd | cut -d: -f1
cut -d: -f1 /etc/passwd


alias
an alias is a different name that can be assigned to command
copy for cp, move for mv, or cls for clear
if a=$(cat /etc/passwd)
$a will not return anything
echo $a will give you the intended results

conditionals
if [[ condition ]]; then 
        commands
elife [[ condition ]]; then
        commands
else
        commands
fi
-e          file exists ?
-f          file exists, and is regular file ?
-d          file exists, and is a directory ?
-s          file exists, and is NOT empty ?
-x          file exists, and IS executable ?
-w          file exists, and is writable by me ?
-gt >       is greater than
-lt <       is less than
-ge         is greater than or equal to
-le         is less than or equal to
-eq ==      is equal to
-ne !=      is NOT equal to
w and above is all for files, the greater than less than double equals and not equals are very specific for strings themselves. Misusing these conditionals can provide you with false positives or false negatives
When comparing strings and integers you need to know which comparision you need to use. With strings use ==, with integers use -eq

sed
it is similar to cut because it lets you change things in the output, main difference is sed allows you to make the changes permanent -i. 
cat passworde | sed 's/telnetd/TELNETD/' passworde
passworde is just a copy of /etc/passwd 
cat password | sed -e '/xrdp/d' -e '/telnetd/d'

awk
cat hosts | awk -F: '{print $1}'
cat hosts | awk -F: 'BEGIN {OFS="&"}{print $1,$3}'
tail password | awk =F: '{print $NF}'
$NF is printing the last field of this string no matter how many fields there are
tail password  | awk -F: 'BEGIN {OFS="$"}{print $1,$3,$4,$NF}'
cat passworde | awk -F: '($3 >= 100)&&($4 <= 1000){print $0}'
SSgt made this fat one-liner for the hosts on the watch floor
cat hosts | awk -F: -v "awkuser=$user" -v "awkoffice=$office" 'BEGIN {OFS=":"} {$2=awkuser}{$4=awkoffice}{print $0}'
cat hosts | awk -F. -v "awkip = $ip" 'BEGIN {OFS"."} {$2=awkip}{print $0}'
"


sort
tail password | awk -F: '{print $3}' | sort -n
sort                sorts content according to position on the ASCII table
sort -n             sorts content numerically
sort -u             sorts content uniqely
sort -nr            sorts content numerically reversed
sort -t +
sort -k 2,4         sorts 1st by content in the 2nd column, then by content in the 4th column
cat password | awk -F: '{print $1}' | sort
sort -u will uniquely sort them but cannot show a count like uniq
cat passworde | awk -F: '{print $3,$4}' | sort -n -k 2


uniq
uniq                sorts content uniqely
uniq -c             sorts content uniqely with a count reading
MUST USE SORT BEFORE USING UNIQ
is going to cut out any duplicates and with -c will say how many repeats there are of things

Parameter is the same thing as variable
variable_name = value
$varable_name -- calls a variable
expr == does math
c = $(expr $a - $b)
echo $c

special variable 
$* -- The positional parameters, starting from one
$@ -- Position parameters, starting from one
$# -- Number of positional parameters
$? -- The exit status of previous command
$- -- The current option flags of the shell
$$ -- The process ID of the shell
$! -- The process ID of the most recent background job
$0 -- $0 is set to the name of the script
$_ -- First command in a script, is the path/name of the script as invoked.
Otherwise, it is the last parameter passed to the most recent command.

functions
myfunc() {
   commands
   more commands
}
#call the function
myfunc

demo 1
car1 = 'A'
var2 = 'B'
myfunc() {
   local vari='c'
   var2 = 'D'
   echo "Inside function car1: $var1 $var2: $var2"
}
echo "Before execution function var1;$var1 var2:$var2"
myfunc
echo "after executing function var1:$vsar1 var2:$var2"

variable substitution
a='5'
b='10'
c='0'
eho 'Bash is only $1 days long'
echo "BASH should be $2 days long"
echo "I wish I spent $3 days in bash"
./bash.sh 5 10 0 --outputs
Bash is only 5 days long
Bash should be 10 days long
I wish I spent 0 days in bash
a=$(b + c)

md5sum exists

Alternate answer for question 15
find /bin /etc /var -maxdepth 3 ! -type p -exec md5sum {} > $HOME/demo/demo2/success 2>$HOME/demo/demo2/fails \;
a=$(wc -l $HOME/demo/demo2/success | awk '{print $1}' )
b=$(grep -c "Is a directory" $HOME/demo/demo2/fails )
if [[ "$a" ]];
       then
               echo "Successfully hashed files: $a";
               echo "Unsuccessfully Hashed Directories:" $b;
       else
               echo "oops";-maxdepth 3
fi

The other end thing like \; is +

LOOPS
x=0
while [[ $x -le 10 ]] ; do
    echo $x
    x=$(($x+1))
done
for x in {0..10}; do
>echo $x
>done
for x in {cosc,jcac,mct,'parris island'}; do
>echo $x
>done
for x in $(cat /etc/passwd | awk -F: '{print $1}')
         do echo $x is a user on this compooter
done
x=0
while [[ $x -le 10 ]] ; do
>echo $x
>x=$(($x+1))
>done

for a in 1 2 3 4 5 6 7 8 9 10
do
    if [ $a == 5 ]
    then
      break
    fi
    echo Iteration is $a
done
which, route or ip route, tar, zip

if [[ <CONDITION> ]]; then
        commands
elif [[ <CONDITION> ]]; then
        commands
fi


Alternate Solution to 20
find /etc -type f -exec stat -c '%a' {} /; > ./perms 2>/dev/null

for x in $(cat ./perms); do
        if [[ $x -le 640 ]]; then
                echo "$x" >> ./low
        elif [[ $X -ge 642 ]]; then
                echo "$x" >> ./high
        fi
done

echo "Files w/ Octal Perm Values 642+:"
cat ./high | sort | uniq -c | sort -nr
echo
echo "File w/ Octal Perm Values 0-640:"
cat ./low | sort | uniq -c | sort -nr
