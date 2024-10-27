Which TCP port is hosting a database server?
``sudo nmap -sC -sV 10.129.120.0`` reveals 4 ports with port 1433 running a Microsoft SQL Server.
![[Pasted image 20241017154030.png]]

What is the name of the non-Administrative share available over SMB?
``smbclient -N -L \\\\10.129.120.0\\`` reveals the shares on the SMB server. The only non-admin share is ``backups``.
![[Pasted image 20241017154557.png]]
What is the password identified in the file on the SMB share?
``smb ls`` reveals there is a file called ``prod.dtsConfig`` . We can download this using ``smb get`` and read this using ``cat`` this reveals there is a password located in the file which is ``M3g4c0rp123``

What script from Impacket collection can be used in order to establish an authenticated connection to a Microsoft SQL Server?

Searching the web for ``Impacket mssql`` reveals a github repo at https://github.com/fortra/impacket/blob/master/examples/mssqlclient.py
This is also the collection which answers the question.

What extended stored procedure of Microsoft SQL Server can be used in order to spawn a Windows command shell?
``xp_cmdshell``

What script can be used in order to search possible paths to escalate privileges on Windows hosts?
``WinPeas``

What file contains the administrator's password?
``MEGACORP_4dm1n!!``

Submit user flag
``3e7b102e78218e935bf3f4951fec21a3``

Submit root flag
``b91ccec3305e98240082d4474b848528``