What does the 3-letter acronym FTP stand for?
->File transfer protocol

Which port does the FTP service listen on usually?
->21

FTP sends data in the clear, without any encryption. What acronym is used for a later protocol designed to provide similar functionality to FTP but securely, as an extension of the SSH protocol?
->Sftp

[What is the command we can use to send an ICMP echo request to test our connection to the target?](Meow#What is the name of the most common tool for finding open ports on a target?)
->Ping

From your scans, what version is FTP running on the target?
-> Used **nmap -Sv 10.129.239.254** to scan with version detection. 
FTP version that is running on target is: vsftpd 3.0.3

From your scans, what OS type is running on the target?
-> Unix, This was also returned with the above used nmap scan.

What is the command we need to run in order to display the 'ftp' client help menu?
-> ftp -h

What is username that is used over FTP when you want to log in without having an account?
->anonymous

What is the response code we get for the FTP message 'Login successful'?
-> Used ***ftp 10.129.239.254*** to connect to host machine. Logged in with "anonymous" followed with any random password that gets disregarded.
Responded 230 Login successful

Response code is 230.

There are a couple of commands we can use to list the files and directories available on the FTP server. One is dir. What is the other that is a common way to list files on a Linux system.
->ls

What is the command used to download the file we found on the FTP server?
-> Used ftp help to see all commands. Used ftp get to download flag.txt

Submit root flag
->Exited the ftp server using ftp bye. Used cat flag.txt to read the txt file and obtain the root

035db21c881520061c53e0536e44f815
