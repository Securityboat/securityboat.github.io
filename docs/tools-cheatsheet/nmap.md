# **NMAP**

## **Basic Commands**

```
#quickly check live hosts on a network using ARP ping scan
nmap -sP 192.168.1.1/24

#Aggressive scan. (Enable OS detection, version detection, script scanning, and traceroute)
nmap -A 192.168.1.1

#Scan Multiple Hosts from a file
nmap -iL hosts.txt

#Scan all ports and save data in XML format
nmap -p 1–65535 host -oX results.xml

#scan host with high speed and server version detection and save data in all formats.
nmap -T3 -sV -p 1–65535 host -oA outputfile

#Scan all vulnerabilities of smb using NSE scripts
nmap --script=smb-vuln-* host

#Scan top "N" ports
nmap --top-ports 10 192.168.1.1

#Scan with custom ports
nmap -p 22,443,25,139,120–500,U:663,2000–3000 host
```

## **Firewall Evasion**

```
#Scan host by spoofing your mac address
nmap --spoof-mac 01:02:03:04:05:06 host

#randomize hosts to evade network monitoring systems
nmap --randomize-hosts -iL hosts.txt

#Using packets with invalid TCP/UDP checksums
nmap --badsum host

#Append custome binary data to packets
nmap --data 0xdeadbeef host
```

