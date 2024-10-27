What does the 3-letter acronym SMB stand for?
-> Server message block

What port does SMB use to operate at?
-> 445

What is the service name for port 445 that came up in our Nmap scan?
-> microsoft-ds
![[Pasted image 20240904191340.png]]
What is the 'flag' or 'switch' that we can use with the smbclient utility to 'list' the available shares on Dancing?
-> -L
![[Pasted image 20240904191556.png]]

How many shares are there on Dancing?
-> 4
![[Pasted image 20240904191723.png]]

What is the name of the share we are able to access in the end with a blank password?
-> Workshares

What is the command we can use within the SMB shell to download the files we find?
-> smb get

Submit root flag
-> Get into the SMB server using ***smbclient \\\\\\\\10.129.136.203\\\\\WorkShares**

Used ls to list all directories in the share. Opened the shares using cd {Sharename}. 
Found flag.txt file in James.P directory.
Downloaded flag.txt using ***smb get flag.txt***
Exited smbclient and used cat flag.txt to read out the flag

5f61c10dffbc77a704d76016a22f1664
