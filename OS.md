https://os.cybbh.io/public/os/latest/index.html
CTFd Activities
http://10.50.24.129:8000/
http://10.50.20.125:8000/challenges
15 is my stack number and 10.50.38.186
The XX on the stacks is your number so for me 10.15.0.4 for Workstation 2
Color coded for a reason, don't be stupid

Day 1 - Powershell
_______________________________________________________________________________________________________________________
Everything is an object
get-help and get-process
get-process | get-member | where-object {$_.membertype -match "method"}
(Get-Process | Select-Object name, id, path | Where-Object {$_.id -lt '1000'}).count 
Within the CIM, or Common Information Module
CIM is a database that messes with the hardware of the system. 
get-ciminstance -classname win32_logicaldisk -filter "drivetype=3" | get-member
get-wmiobject -class win32_bios 
get-cminstance -classname win32_bios
Get-ExecutionPolicy -list
Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser
$profile shows the profile of who you are signed into | PERSISTENCE
The Order precedence will always be ready with the All Users, All Hosts so on and so forth
PS C:\> test-path -path $profile.currentusercurrenthost
False
PS C:\> test-path -path $profile.currentuserallhosts
False
PS C:\> test-path -path $profile.allusersallhosts
False
PS C:\> test-path -path $profile.alluserscurrenthost
False
new-item -ItemType file -path $profile -force
set-alias -name ip -value get-nettcpconnection
good one for persistence and location 

Stuff for the activity stacks -----------------------------------------------------------------------------------------
get-item WSMan:\localhost\Client\TrustedHosts
Set-Item WSMan:\localhost\Client\TrustedHosts -value "file-server"
Set-Item WSMan:\localhost\Client\TrustedHosts -value "domain-control" -Concatenate
invoke-commamd -ComputerName file-server {get-service} -asjob
$sess=New-PSSession -ComputerName file-server -Credential andy.dwyer
enter-pssession $sess
get-service

$url = "http://downloads.volatilityfoundation.org/releases/2.6/volatility_2.6_win64_standalone.zip"
$output = "$PSScriptRoot\volatility_2.6_win64_standalone.zip"
$start_time = Get-Date

$wc = New-Object System.Net.WebClient 
$wc.DownloadFile($url, $output) 


(New-Object System.Net.WebClient).DownloadFile($url, $output)
Might have to use this


Day 2 - ADS and Registry
_______________________________________________________________________________________________________________________











Day 3 - Linux
_______________________________________________________________________________________________________________________








Day 4 - Windows Boot Process
_______________________________________________________________________________________________________________________
Turn on Computer
1. POST (Power On Self Test)
2. BIOS (Basic Input Output System)
3. UEFI *newer take on BIOS* (Unified Extensible Firmware Interface)
   Boots up faster than BIOS, allows to have 9Zetabytes which is 9 Billion Terrabytes
winload.exe is BIOS, winload.efi is UEFI
Anything non-essential is loaded in the Ntoskrnl.exe
smss.exe (Session Manager SubSystem) starts csrss.exe which starts each User Subsytem
Users cannot interact with kernel mode processes


In cmd prompt
bcdedit /export bcdbackup
bcdedit /set {current} description "Windows XP"
bcdedit /create {ntldr} 
bcdedit /delete {ntdlr} /f




Day 5 - Linux Boot Process
_______________________________________________________________________________________________________________________

Look in the book chucklenuts 





Day 6 - Windows Process Validity / User Account Control / SysInternals
_______________________________________________________________________________________________________________________
Process Validity
The importance of knowing when processes need to run, being able to tell if a process is a fake or not
Like how solar winds fucked everyone with a malware inside of the update
ALWAYS try to find persistence 
netstat -anob | more
never only trust one command, it will not show you everything
There's usually a GUI that will go along with whatever you're trying to see
Make sure processes are running from the right places
i.e. calc.exe running from Program Files instead of System32



UAC (User Account Control)
It is the "Do you want so and so to make changes to your computer?" Or run as admin
commands 
./sigcheck -m C:\Windows\System32\slui.exe
./sigcheck -m C:\windows\regedit.exe
./strings –s c:\windows\system32\*.exe | findstr /i autoelevate



SysInternals
basically power user administrative tools 
net use comes in handy for a lot of things
commands to get the tools
net use * http://live.sysinternals.com
New-PSDrive -Name "SysInt" -PSProvider FileSystem -Root "\\live.sysinternals.com\Tools"
Alt.
$wc = new-object System.Net.WebClient 
$wc.DownloadFile("https://download.sysinternals.com/files/SysinternalsSuite.zip", "$pwd\SysinternalsSuite.zip")
Expand-Archive SysinternalsSuite.zip 

sc showsid
asInvoker
sigcheck



Day 7 Linux Process Validity
_______________________________________________________________________________________________________________________
ps -elf
ps --pid 1
top (real time process listing)
ps -elf --forest
Kernel space is separated from the user space to protect the system
EUID has rights, RUID is the owner
kill is a signal
SIGSTOP, SIGTERM, SIGCHILD, SIGPIPE, SIGIO, etc.
kill -l
a daemon is just a background process
disown -a && exit #Close a shell/terminal and force all children to be adopted
A zombie is dead but hasn't been fully reaped by the parent process
kill -18 *zombiePPID*
All daemons techincally are orphans, but all orphans are not daemons
Orphan processes can be persistent

On SysV
service <servicename> status/start/stop/restart

On SystemD
systemctl list-units --all
systemctl status <servicename.service>
systemctl status <PID of service>
systemctl start/stop/restart <servicename.service>

Job Control
jobs
kill -9 %1

Cron Jobs
The cron daemon checks /var/spool/cron, /etc/cron.d, and /etc/crontab STOMP STOMP STOMP
User and System
System is in /etc/crontab
Run backups, rotate logs
User cron jobs
User is in /var/spool/cron/crontabs/
whatever task the user wants to schedule
    crontab -u [user] file This command will load the crontab data from the specified file
    crontab -l -u [user] This command will display/list user’s crontab contents
    crontab -r -u [user] This Command will remove user’s crontab contents
    crontab -e -u [user] This command will edit user’s crontab contents
cat /etc/crontab
first numberblock is minute, hour, day of month, day of week
always try to cat, ls, or add a sudo to read these
CRON IS A PERSISTENCE MECHANISM
OR A LAUNCH MECHANISM

Processes and Proc Dir
Proc Dir is another place to enumerate processes
sudo lsof | tail -30
sudo lsof -c sshd
 sudo lsof -i udp:123

 FOR EVIL 
 cat /etc/cron.d/mdadm
 netstat -ano
 


Day 8 Windows Auditing & Logging
_______________________________________________________________________________________________________________________

Get-LocalUser | select name,sid
Will NOT show domain users

get-wmiobject win32_useraccount | select name,sid
Will show domain and local users
 
Get-ItemProperty "HKCU:\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}\Count\"
The encoding is in ROT13

Get-ItemProperty "Registry::hkey_users\*\software\microsoft\windows\currentversion\explorer\userassist\{CEBFF5CD-ACE2-4F4F-9178-9926F41749EA}\Count\"

LOOK AT 3.1 IN THE FG FOR INFO ON WHERE TO LOOK IN REGEDIT 
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\State\UserSettings #On 1809 and Newer

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\bam\UserSettings #On 1803 and below
get-item HKLM:\system\currentcontrolset\services\bam\UserSettings\*

Get-ComputerInfo | select osname,osversion

Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\bam\UserSettings\S-1-5-21-2881336348-3190591231-4063445930-1004

Get-Content 'C:\$RECYCLE.BIN\S-1-5-21-2881336348-3190591231-4063445930-1003\$RUZK3G5.txt'

Get-Childitem -path 'C:\Windows\Prefetch\' -erroraction 0 | select -first 10

Get-ChildItem -Recurse C:\Users\*\AppData\Roaming\Microsoft\Windows\Recent -ErrorAction Continue | select FullName, LastAccessTime

Get-Item 'Registry::\HKEY_USERS\*\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.*'

[System.Text.Encoding]::Unicode.GetString((gp "REGISTRY::HKEY_USERS\*\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt")."0")

Get-Item "REGISTRY::HKEY_USERS\*\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt" | select -Expand property | ForEach-Object {
[System.Text.Encoding]::Default.GetString((Get-ItemProperty -Path "REGISTRY::HKEY_USERS\*\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs\.txt" -Name $_).$_)
}

Frequency
.\strings.exe 'C:\users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\History' -accepteula 

Most Visited
strings.exe 'C:\users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\Top Sites'

User Names
strings.exe  'C:\users\andy.dwyer\AppData\Local\Google\Chrome\User Data\Default\Login Data'


$History = (Get-Content 'C:\users\student\AppData\Local\Google\Chrome\User Data\Default\History') -replace "[^a-zA-Z0-9\.\:\/]",""
$History| Select-String -Pattern "(https|http):\/\/[a-zA-Z_0-9]+\.\w+[\.]?\w+" -AllMatches|foreach {$_.Matches.Groups[0].Value}| ft


ls

Answer Key Bullshit
C:\TempContents> cat .\17249efc-482e-4ab4-ba5d-bda14bbafb81.ps1
PS C:\TempContents> cat \windows\system32\artifacts.ps1



Day 9 Linux Auditing & Logging
_______________________________________________________________________________________________________________________
All logging is saved on a physical hardrive space, biggest issue with logging is finding a good balance between information and efficiency. 

human-readable text documents within /var/log
configured using files in /etc/rsyslog/

cat /etc/rsyslog.d/50-default.conf
-/var/log/syslog is a catch all
/var/log/mail.err is logging that severity code and anything more critical
IF THERE IS A ! IN FRONT OF THE ERR THEN IT IS THE OPPOSITE AND ANYTHING LESS CRITICAL

grep timesyncd /var/log/syslog 
log rotations are backups in linux machines
cat /etc/logrotate.conf
ls -l /var/log
when backed up the files are zipped to save space

Any logs having to do with logins and authentication attempts. . /var/log/auth.log - Authentication related events . /var/run/utmp - Users currently logged in .. Not in human readable format. Must use last command . /var/log/wtmp - History file for utmp .. Not in human readable format. Must use last command . */var/log/btmp - Failed login attempts
only root level permission users can look at /var/log/btmp, there is also /var/run/utmp and a /var/run/wtmp.
dmesg is a kernel message



Location: All logs are in /var, most are in /var/log
Config File: /etc/rsyslog.conf
Service: /usr/sbin/rsyslogd

journalct --list-boots
all logs between boot and run
journalctl -b 321 
journalctl -u ssh.service
might have to use systemctl to find the units for journalctl -u




Day 10 Windows Memory Analysis & Active Directory
_______________________________________________________________________________________________________________________
Volatility
Most Volatile - Cache maybe RAM
Least Volatile - Backups or other HDD type devices

Volatility is a tool, with the Python being the largest, and the standalone just being a binary
Volatility uses profiles to parse through data, because no machine is the same

Memory dumps are not human readable, use strings

 
 PERSISTENCE
 Registries
 Malicious Processes 
 Scheduled Processes
 Services
 


Day 11 Review
_______________________________________________________________________________________________________________________

Windows  

Ports: get-nettcpconnection, netstat -ano -anob, tcpview.exe
   sus ports: patterns, 4444, 6667, etc OR CHECK IANA.ORG
   
Processes: get-process, procmon.exe, tasklist, task manager
   sus processes: system windows processes running out of wrong directory, misspelling in standard processes

Persistence: get-scheduledtask, reg query, regedit, ps-provider, schedtask, $psprofile (understand the precedence, and why), use get-content on the profile
   Powershell profiles, registry run keys (run/runonce), scheduled tasks, autorun 

Artifacts: logs that applications create that are left behind, like browser history, bam, and prefetch
   bam, user assist, jump list, etc (windows auditing logging) 
Powershell commands:
   get-childitem, get-item, get-itemproperty, get-property


Linux

Ports: netstat -ano -anop -ltup
   sus ports: patterns, 4444, 6667, etc

Processes: ps -elf, top, htop
   sus processes, running in wrong directory, misspelled

Persistence: cat /etc/crontab
   /etc/profile, .bash_profile, system profile, user profile, cron jobs



cat /etc/shadow
sudo !!   #this is a shortcut to run the previous command with sudo
sudo cat /var/spool/cron/crontabs/root
ls -l to view permissions

10.50.44.63 for linux with ssh
10.50.25.2 for windows with xfreerdp
http://10.50.20.125:8000/challenges
