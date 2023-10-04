https://os.cybbh.io/public/os/latest/index.html
CTFd Activities
http://10.50.24.129:8000/
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


