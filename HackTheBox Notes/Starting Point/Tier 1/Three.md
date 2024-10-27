How many TCP ports are open?
-> `nmap -sC -sV 10.129.207.135` 
![[Pasted image 20240907164935.png]]
What is the domain of the email address provided in the "Contact" section of the website?
-> Navigate to the `10.129.207.135` in the browser and go to the contact section.
![[Pasted image 20240907165311.png]]
This reveals the domain of the mail address is `thetoppers.htb`

In the absence of a DNS server, which Linux file can we use to resolve hostnames to IP addresses in order to be able to access the websites that point to those hostnames?
-> Googled `Linux Hostname Resolution` , this revealed we can resolve hostnames through a local `/etc/hosts` file.

Which sub-domain is discovered during further enumeration?
-> s3.thetoppers.htb

Which service is running on the discovered sub-domain?
-> Amazon S3

Which command line utility can be used to interact with the service running on the discovered sub-domain?
-> awscli

Which command is used to set up the AWS CLI installation?
-> aws configure

What is the command used by the above utility to list all of the S3 buckets?
-> 

This server is configured to run files written in what web scripting language?
->

Submit root flag
->