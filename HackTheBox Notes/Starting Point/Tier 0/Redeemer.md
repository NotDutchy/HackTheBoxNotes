Which TCP port is open on the machine?
-> Port 6379 is open
![[Pasted image 20240904194324.png]]

Used ***nmap -p- -sV 10.129.247.253** to scan for open ports.

Which service is running on the port that is open on the machine?
-> Redis 

What type of database is Redis? Choose from the following options: (i) In-memory Database, (ii) Traditional Database
-> In-memory Database
![[Pasted image 20240904194525.png]]

Which command-line utility is used to interact with the Redis server? Enter the program name you would enter into the terminal without any arguments.
-> redis-cli

Which flag is used with the Redis command-line utility to specify the hostname?
-> -h is used to specify the hostname

Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server?
->  Info

What is the version of the Redis server being used on the target machine?
->5.0.7
![[Pasted image 20240904195220.png]]

Which command is used to select the desired database in Redis?
-> Select

How many keys are present inside the database with index 0?
-> Use Select 0 to go to database with index 0. Used info command to list info on the database which returns Keys=4

There are 4 keys in this database
![[Pasted image 20240904195418.png]]

Which command is used to obtain all the keys in a database?
-> KEYS *

Submit root flag
-> 03e1d2b376c37ab3f5319922053953eb