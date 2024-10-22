# Cheetsheet
## Websites
- Shodan.io: Gives info on websites
- https://www.ssllabs.com/ssltest/ = ssl vul teste and info on sites

  
# nmap  


```

reddit

```























# Nmap 

### Starting scan 
```
nmap -sCV -T4 -O --osscan-guess -v -p- <target_ip>

```

### Script for checking for base cves

```
sudo nmap -p<port> --script "vuln" 192.168.50.114
```


### try this

```
sudo nmap -Pn -n $IP -sC -sV -p- --open
```


### run udp after tcp nmap to see if its open because its important if it is
```
sudo nmap -Pn -n $IP -sU --top-ports=100 --reason
```
### SMD enumeration typically for port 139 and 445 if they open
```
nmap -p 139,445 --script=smb-enum-shares,smb-enum-users,smb-os-discovery,smb-vuln* <target_ip>
```
# WEBsite scanning

### Gobuster
```
gobuster dir -u <target> -w /usr/share/wordlists/dirb/common.txt
```


### Net cat
It is used to send and recive data over an open port, -lvnp is to setup a listener
```
nc <target_ip> <port>
```


### SNMP
```
-Nmap UDP scan-
sudo nmap <IP> -A -T4 -p- -sU -v -oN nmap-udpscan.txt

snmp walk is important to see what software and user accounts are on the machine

snmpcheck -t <IP> -c public #Better version than snmpwalk as it displays more user friendly

snmpwalk -c public -v1 -t 10 <IP>     #Displays entire MIB tree, MIB Means Management Information Base
snmpwalk -c public -v1 <IP> 1.3.6.1.4.1.77.1.2.25    #Windows User enumeration
snmpwalk -c public -v1 <IP> 1.3.6.1.2.1.25.4.2.1.2     #Windows Processes enumeration
snmpwalk -c public -v1 <IP> 1.3.6.1.2.1.25.6.3.1.2       #Installed software enumeraion
snmpwalk -c public -v1 <IP> 1.3.6.1.2.1.6.13.1.3           #Opened TCP Ports

-Windows MIB values-
1.3.6.1.2.1.25.1.6.0 - System Processes
1.3.6.1.2.1.25.4.2.1.2 - Running Programs
1.3.6.1.2.1.25.4.2.1.4 - Processes Path
1.3.6.1.2.1.25.2.3.1.4 - Storage Units
1.3.6.1.2.1.25.6.3.1.2 - Software Name
1.3.6.1.4.1.77.1.2.25 - User Accounts
1.3.6.1.2.1.6.13.1.3 - TCP Local Ports



```
































