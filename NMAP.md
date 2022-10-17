# NMAP notes

Nmap
-sL list can (text tile import)
-sn ping Scan

## Scans

Nmap can perform multiple scan types by default a syn scan is performed. Their are two main types of scan TCP and UDP scans.

TCP Scans
-sS TCP Syn
-sT Connect
-sA Ack
-sW Window
-sM Maimon
UDP Scans
-sU UDP
-sN TCP Null
-sF FIN
-sX Xmas scan

## Port scans

-p Port
-p- default all port scan
-p22 Single port
-p1-65535 port range
-p U:53,111,137 T:21-25,80,139,8080,S:9

In the below example the nmap will scan the target ip ports 1 to 65535 using a syn scan (-sS)
Example: nmap -p- <Target_IP>



### Examples

Basic Scan (Full port syn scan TCP)
nmap -p- `<Target_IP>`


### Links

NMAP examples
https://phoenixnap.com/kb/nmap-scan-open-ports#:~:text=How%20to%20Scan%20Nmap%20Ports,-To%20scan%20Nmap&text=Replace%20the%20IP%20address%20with,the%20ports%20on%20that%20system.&text=Note%3A%20The%20developers%20at%20nmap,at%20scanme.nmap.org.

NMAP switches
https://www.ciscopress.com/articles/article.asp?p=469623&seqNum=4
