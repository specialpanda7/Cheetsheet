# Cheetsheet

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








































