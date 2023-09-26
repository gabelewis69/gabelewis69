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
