What Nmap scanning switch employs the use of default scripts during a scan?
-> -sC

What service version is found to be running on port 21?
-> vsftpd 3.0.3
![[Pasted image 20240905140944.png]]

What FTP code is returned to us for the "Anonymous FTP login allowed" message?
-> 230

After connecting to the FTP server using the ftp client, what username do we provide when prompted to log in anonymously?
-> anonymous

After connecting to the FTP server anonymously, what command can we use to download the files we find on the FTP server?
-> get

What is one of the higher-privilege sounding usernames in 'allowed.userlist' that we download from the FTP server?
-> First list directories using _ls_ ![[Pasted image 20240905141521.png]]
Use _get_ to download the allowed.userlist file.
![[Pasted image 20240905141600.png]]
Now we can read the file on our main kali system
![[Pasted image 20240905141633.png]]
The highest privlege sounding username in this file is "admin"

What version of Apache HTTP Server is running on the target host?
-> Apache httpd 2.4.41

What switch can we use with Gobuster to specify we are looking for specific filetypes?
-> -x

Which PHP file can we identify with directory brute force that will provide the opportunity to authenticate to the web service?
-> login.php
![[Pasted image 20240905142923.png]]
Submit root flag
->
Navigate to http://10.129.181.124/login.php in the browser.

This opens up a login page ![[Pasted image 20240905143235.png]]

Now we can try and enter a combination of username and password we previously found using the FTP client files
![[Pasted image 20240905143305.png]]![[Pasted image 20240905141633.png]]

After a successful combination :
![[Pasted image 20240905143411.png]]

The root flag for this machine is c7110277ac44d78b6a9fff2232434d16