This document contains short sections of the services found and how they were exploited. It contains tools used and the commands used to exploit these machines.
# Tools
## NMap
Nmap has been used for scanning the machines. This has been done consistently and consecutively in different ways. 
### Ways of usage
Usually `sudo nmap -sC -sV [10.10.10.1]` is sufficient. 
To target multiple targets, string them together, and divide by spaces: 
`sudo nmap 10.10.10.1 10.10.10.2 10.10.10.2`.
Scan an entire subnet: `sudo nmap 10.10.10.1/16`. 
Scan a file of ips: `sudo nmap -F -iL ipaddresses.txt`.
#### Choose interface
Usually, nmap chooses its interface automatically. Sometimes you might want to manually choose your interface. Therefore use `sudo nmap -e lo 192.168.1.1`.
#### ipv6
To scan ipv6 targets, use `sudo nmap -6 fe80:9d77:c9db:7a26:cb33`.
#### scan random targets
This is risky, never do this randomly. However it is possible to scan random targets using `sudo nmap -iR 5` to scan five random targets.
#### reason
This is a useful switch that will try to explain why a port would be in its current state, i.e open, closed, filtered, etc. Use it like so: `sudo nmap --reason 10.10.10.1`.
#### open
Using the `open` parameter, nmap will only reveal open ports, this could lead to less information, however the information you'll get is clear and concise. Use it like so: `sudo --open 10.10.10.1`.
#### Trace packets
Use `--packet-trace` to trace how to packets go. Use it like so: `sudo --packet-trace 10.10.10.1`. It provides detailed information about the packets nmap sends and the packets nmap receives.
### Portscanning
Usually, nmap scans only the top 1000 most used ports. However this might not be enough or could be too many depending on our situation. To cut that 1000 into 100 we can run `sudo nmap -F 10.10.10.1`. This will only check the top 100 ports.
To manually select ports, use: `sudo nmap -p 22 10.10.10.1`. Multiple is also possible, separate it with comma's: `sudo nmap -p 22,80,139,50-90 10.10.10.1`.
Scanning **all** target is possible using `sudo nmap -p "*" 10.10.10.1`. This will scan all `65535` ports.
#### Scan udp and tcp ports
If one needs to scan both udp and tcp ports. You can run `sudo nmap -sU -sT -p U:22,T:80 10.10.10.1`. This specifies which ports need to be scanned using tcp and udp.
#### Scan a range of top ports
Sometimes, we want to scan more than 1000 top ports. With nmap we can scan an x amount of ports with `--top-ports`. Use it like so: `sudo nmap --top-ports 10000 10.10.10.1`. This will scan the 10000 top ports.
#### Random port scanning
This will force nmap to scan ports in a random order, possibly evading detection systems. Use it like so: `sudo nmap -r 10.10.10.1`. To enhance your understanding. Use it with `-v`: `sudo nmap -v -r 10.10.10.1`.
### Advanced techniques
Now that the basic techniques have been discussed. Let's go over some advanced techniques.
#### Ping Requests
##### Don't ping
By default, nmap sends a `ping` request to see if the target to scan is alive. Sometimes this isn't helpful, especially if the target is behind a firewall that blocks `ping probes`. To evade the standard ping we can use the `-PN` switch. Use it like so: `sudo nmap -PN 10.10.10.1`.
##### ICMP ping
To see if the target(s) are up, we can also just ping the targets simply by using the `-sP` switch. This will only `ping` the target(s), use it like so: `sudo nmap -sP 10.10.10.0/16`.
##### TCP SYN ping
If `icmp` pings are blocked, we can try and send a TCP SYN ping. Do this by using the `-PS` switch. It will send a SYN packet to the target system, then it will listen to a response on the given port. If no port is provided, it will listen to port 80. Use it like so: `sudo nmap -PS 10.10.10.1`. If listening to another port use: `sudo nmap -PS 443 10.10.10.1`.
##### TCP ACK ping
To run a TCP ACK ping, use the `-PA` switch. It provides an alternative way of network exploration. Use it as follows: `sudo nmap -PA 10.10.10.1`.
##### UDP ping
Another way to ping is sending a UDP ping. Firewalls usually block this, however some poorly configured firewalls might allow it. Especially if it exclusively filters on `tcp` packets. Use the `-PU` switch for this. Use it as follows: `sudo nmap -PU 10.10.10.1`. A port can be specified. The default port is port `40125`.
##### SCTP INIT ping
The `-PY` switch allows to send a SCTP INIT ping to a specified target. Use it as follows: `sudo nmap -PY 10.10.10.1`. It can be used to discover hosts that use the Stream Control Transmission Protocol. SCTP is widely used in systems like VoIP. The default port it listens to is port 80.
##### ICMP echo ping
To classically send a ping to a target, we can use the `-PE` switch to send the ping. Use it as follows: `sudo nmap -PE 10.10.10.1`. It is commonly used in local networks where ICMP packets can be send with few restrictions. 
##### ICMP timestamp ping
Although a lot of firewalls might block `icmp echo pings`, some poorly configured firewalls might respond to `icmp timestamp pings`. Use it with the `-PP` switch. Use it as follows: `sudo nmap -PP 10.10.10.1`. 
##### ICMP address mask ping
Just like it's cousing, the `icmp timestamp ping`, this enables an `icmp` address mask ping on a specified target. Use it with the `-PN` switch. Use it as follows: `sudo nmap -PM 10.10.10.1`. It attempts to ping a target using alternative `icmp` registers. It can occasionally bypass firewalls configured to block standard `echo ping` requests.
##### IP protocol ping
Allows to ping a target with different IP protocols: icmp, igmp and ip-and-ip. Use it with the `-PO` switch, use it as follows: `sudo nmap -PO icmp 10.10.10.1`.
##### ARP ping
This allows to send an Address Resolution Protocol (ARP) Ping on a target. Use it with the `-PR` switch. Use it as follows: `sudo nmap -PR 10.10.10.1`. This offers increased accuracy over other ping requests because LAN hosts can't block ARP requests, even when situated behind a firewall. It is required to note that ARP is confined to your local subnet.
#### Miscellaneous
Except for different ping requests, there are also different switches one can use.
##### Traceroute
Performs a traceroute to each target after a scan is complete. Traceroute is a network diagnostic tool that determines the path packets take to reach a target host, showing the series of hops (routers) along the way. Use it with the `--traceroute` switch. Use it as follows: `sudo nmap --traceroute 10.10.10.1`. Nmaps traceroute proves superior to Linux's built-in traceroute functionality.
##### Reverse DNS resolution
The `-R` switch empowers you to enforce reverse DNS resolution on a target. Use it as follows: `nmap -R 10.10.10.1`. This can however, severely impact the performance of a scan.
##### Disable DNS lookup
The `-n` proves to improve performance by not looking for DNS resolutions. Use it as follows: `sudo nmap -n 10.10.10.1`.
#### Scans
##### TCP SYN scan (stealth)
A TCP SYN scan sends a SYN packet to the target and listens for a response. The stealth is in that it doesn't try to make a connection with the target. Thus a lot of firewalls won't log it. Yet modern firewalls most likely will. Use it with the `-sS` switch like so: `sudo nmap -sS 10.10.10.1`.
##### UDP scan
While nmap by default scans by TCP, a UDP scan might show more information by a poorly configured firewall. Use it with the `-sU` switch as follows: `sudo nmap -sU 10.10.10.1`.
##### TCP NULL scan
The `-sN` switch allows the user to send `null` packets to the target. While a target might usually be guarded, it might respond to a `null` packet. Use it as follows: `sudo nmap -sN 10.10.10.1`
##### TCP FIN scan
Just like the `null` scan, it is an unusual packet that might probe a response from the target. Use it with the `-sF` switch as follows: `sudo nmap -sF 10.10.10.1 `
##### XMAS scan
Another way to lure a response from a target, is by sending a lot of flags in one packet. This can be done using the `-sX` switch as follows: `sudo nmap -sX 10.10.10.1`. However not all firewalls might respond to such a packet.
##### TCP ACK scan
To determine whether the target is shielded by a firewall can be found out with the `-sA` switch. Use it as follows: `sudo nmap -sA 10.10.10.1`.  Nmap will be on the lookout for `rst` responses. If no response is received, signals the system is filtered. If the system is filtered it indicates the presence of a firewall.
### Useful switches
* `-sC`, **Default Script**: Runs a collection of Nmap Scripting Engine (NSE) scripts against the target IP address for common tasks such as service detection and vulnerability checking.
  * `-sV`, **Version Detection**: Detects the version of services running on the target by sending probes to open ports and analysing responses.
  * `-sS`, **TCP SYN Scan**: Performs a stealthy "half-open" scan to identify open ports by sending SYN packets and analysing responses without completing the TCP handshake. Commonly used for stealthy scans.
  * `-A`, **Aggressive Scan**: Enables OS detection, version detection, script scanning and traceroute.
  * `-O`, **OS Detection**: Uses various techniques to identify the targets operating system.
  * `-P`, **Port Range**: Specifies which ports should be scanned, i.e: `nmap -p 80,443 10.10.10.1` or `nmap -p- 10.10.10.1` to scan all 65535 TCP ports.
  * `-Pn`, **No Ping**: Disables host discovery and treats all hosts as online. Useful against targets that do not respond to ping requests but have open ports.
  * `-T`, **Timing Template**: Sets the timing template (from `T0` to `T5`) to control the speed of the scan.
  * `--min-rate`, **Minimum Number Of Packets**: Ensures that Nmap maintains a consistent rate of packet transmission.
  * `--exclude`, **Exclude target**: When scanning multiple hosts or a range of hosts, it might be important to leave some hosts out, this can be done with exclude.
  * `--excludefile`, **Exclude file**: Can exclude a list of ips listed in a file: `--excludefile ip.txt`.
## Burp and ZAP
Both applications are proxy tools. Where Burp is more userfriendly, ZAP is a completely free tool that out of the box has some very useful automated search tools. Because they are both proxy tools, they can be linked together in a proxy chain in order to have the best of both worlds! To do this, let's start with ZAP
### Installing ZAP
When Kali comes out of the box, ZAP is not installed. Download it on your machine from [this](https://www.zaproxy.org/download/) download link. Sometimes, problems can occur, in my case I've always got the problem that the `DISPLAY` variable had problems, just run `unset DISPLAY` and run the installer again. 
### Configuring ZAP
Upon running ZAP. Select the `gear box` or go to `tools > options...`. Then, navigate to `Network`.  Set your Local Proxy to `localhost` and port `8081`. Make sure your web browser has `FoxyProxy` or any other proxy extension and listens on `localhost` and port 8081 just like ZAP.
Now we should configure an upstream proxy (aka outgoing proxy). This can be done in the tab `Connection`. Here, navigate to `HTTP proxy` and set the `Host` to `localhost` and the port to 8080.
### Configuring Burpsuite
Now that ZAP is configured, run Burpsuite and make sure there is a proxy listening on localhost port 8080. This is all the configuration for Burpsuite. Now you can commence running the automated scan on ZAP and see the requests and responses come in in Burpsuite.
## SQLMap
sqlmap
## John the Ripper
The tool `john`, simply said, is used to crack passwords. This can be with hashes found in a database. For this we can run `john --format=raw-sha512 hash.txt` as is done in [[0020xGreenHorn]]. Another way it can be done is on zip files, therefore we can run `john -wordlist=/opt/SecLists/Passwords/Leaked-Databases/rockyou.txt hashes.txt` as is done in [[0014xVaccine]]. Other ways can be found [here](https://pentestmonkey.net/cheat-sheet/john-the-ripper-hash-formats).
## Hashcat
hashcat
## Python shell
To upgrade a reverse shell simply run: 
```python
python3 -c 'import pty;pty.spawn("/bin/bash")'
```
## NC64.exe
nc64
## winPEASx64.exe
winpeas
## Ffuf
Ffuf is a tool used for fuzzing webapplications. It is commonly used to fuzz for subdomains. It can be used like so:
```
ffuf -u http://example.abc -H "Host:FUZZ.example.abc" -w /opt/SecLists/Discovery/DNS/subdomains-top1million-5000.txt -fw 18
```
* **-u**: defines the URL to enumerate.
* **-H**: show where `ffuf` should enumerate the list.
* **-w**: The wordlist used for the enumeration. Every word in this list will be tried on the position where `FUZZ` is defined in the **-H** switch.
* **-fw**: defines the standard amount of words returned in the body. If it deviates from this amount, a subdomain is found.
Usage of these tools is done in [[002cxPermX]] and [[002dxEditorial]].
# Services
## Telnet
Telnet is a service that runs on port 23. Telnet is a network protocol used for remote terminal access, allowing users to connect to and interact with another computer or network device over a network connection. It is an old service. Connection requests are configured with username/password combinations for increased security.
However, in Telnet, due to configuration mistakes, important accounts can be left with blank passwords. To read more on this read [[0000xMeow]].
## FTP
FTP (File Transfer Protocol) is a service that runs on port 21. FTP is used to transfer files between a client and a server. It allows users to upload and download files among other things. Here as well, configuration mistakes can happen, to read more on that see [[0001xFawn]] or [[000AxCrocodile]]
## SMB
SMB (Server Message Block) is a network protocol that is standard enabled on ports 445 and 137-139. SMB is used primarily by Windows-based computers for sharing files, printers and other resources across a network. It enables networked devices to communicate and perform operations such as file and printer sharing, remote access to services and [inter-process communication](https://www.geeksforgeeks.org/inter-process-communication-ipc/) (IPC). In the first version, there was a critical vulnerability that was exploited by an exploit called **Eternal Blue** by the Shadow Brokers. To see how to use `smbclient` and own a badly configured server read [[0002xDancing]], [[000BxResponder]] or [[0011xTactics]].
## Redis
Redis is an in-memory data structure store known for its speed and versatility. It can serve as a database, cache and message-broker. Redis typically operates on port 6379. Due to Redis being practically an in-memory database, all memory is stored in RAM. It does however periodically save a snapshot of the dataset to the disk. To read about how to access a Redis database in Kali: [[0003xRedeemer]]
## RDP
RDP (remote Desktop) is a protocol developed by Microsoft that allows a user to remotely control a Windows-based computer over a network connection. RDP offers remote access to the graphical desktop as well as access to applications and files. RDP typically runs on port 3389. To access a service like RDP from Kali read [[0004xExplosion]].
## Nginx
Nginx is a webserver and reverse proxy. It barely uses any resources and is highly scalable. It can handle a large number of concurrent connections which comes in handy when running a website. Nginx operates on port 80. Which is the default port your web browser looks for upon visiting a web application. A webserver can have a lot of attack vectors. One of them is enumeration of directories. To read more about that: [[0005xIgnition]]
## Mongod
Mongod is the primary [daemon process](https://www.techtarget.com/whatis/definition/daemon) for MongoDB, it typically operates on port 27017. To interact with Mongod, read: [[0006xMongod]].
## Rsync
Rsync is a service that typically runs on port 873. It acts as a server that listens for incoming connections from rsync clients. The rsync daemon (rsyncd) is configured to run as a service on port 873/tcp, and clients can connect to it to synchronise files and directories over the network. To read how to interact with it: [[0007xSynced]].
## SQL
SQL (Structured Query Language) is a language used for SQL databases like MySQL. SQL databases typically operate on port 3306. SQL is popular in combination with webservers to persist user information like usernames and passwords. Herein lies the risk that if the web application is poorly coded or configured, the user input can be poorly handled enabling the risk of SQL injections. To read up on such a certain scenario [[0009xSequel]].
## Vhosts
vhosts
# Vulnerabilities
## Path traversal / Local File inclusion (LFI)
A path traversal is a security vulnerability typically found in web applications. It occurs when an attacker is able to manipulate input access to files and directories outside the intended path. This can expose sensitive information, allow unauthorized access, or enable the execution of malicious code. To defend against this, make sure all user inputs for accessing files is properly sanitised. To read more on this do check [[000BxResponder]].
### Examples
Possibility for a path traversal:
```http
http://example.com/index.php?language=french.html
```
Exploitation of the path traversal:
```http
http://example.com/index.php?language=../../../../../../../../etc/hosts
```
## IDOR
This is a vulnerability that allows users to bypass content meant for them, by changing a variable client-side to access content for others. A good example has been shown in [[0013xOopsie]] where the `guest` account everyone could access had the id of `2` when visiting the `account` page, upon changing this to `1` we could all of a sudden access the administrator account and had rights to a file upload which we could chain together to upload a `malicious php` script.
# Privilege escalations
Privilege escalations are the process of getting more permissions on a system. Here, we'll discuss the privilege escalations on two different type of devices; Windows and Linux.
## Windows
win
## Linux

