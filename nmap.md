# Nmap

![alt text](image.png)

![alt text](image.png)

You can also provide a file as input for your list of targets, nmap -iL list_of_hosts.txt.

If you want to check the list of hosts that Nmap will scan, you can use nmap -sL TARGETS. This option will give you a detailed list of the hosts that Nmap will scan without scanning them; however, Nmap will attempt a reverse-DNS resolution on all the targets to obtain their names. Names might reveal various information to the pentester. (If you don’t want Nmap to the DNS server, you can add -n.)


