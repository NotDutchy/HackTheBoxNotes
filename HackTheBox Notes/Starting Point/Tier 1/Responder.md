When visiting the web service using the IP address, what is the domain that we are being redirected to?
-> unika.htb

Which scripting language is being used on the server to generate webpages?
-> php

What is the name of the URL parameter which is used to load different language versions of the webpage?
-> page

Which of the following values for the `page` parameter would be an example of exploiting a Local File Include (LFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"
-> ../../../../../../../../windows/system32/drivers/etc/hosts

Which of the following values for the `page` parameter would be an example of exploiting a Remote File Include (RFI) vulnerability: "french.html", "//10.10.14.6/somefile", "../../../../../../../../windows/system32/drivers/etc/hosts", "minikatz.exe"
-> //10.10.14.6/somefile

What does NTLM stand for?
-> New Technology Lan Manager

Which flag do we use in the Responder utility to specify the network interface?
-> -I

There are several tools that take a NetNTLMv2 challenge/response and try millions of passwords to see if any of them generate the same response. One such tool is often referred to as `john`, but the full name is what?.
-> John the Ripper

What is the password for the administrator user?
-> badminton
![[Pasted image 20240905151746.png]]

We'll use a Windows service (i.e. running on the box) to remotely access the Responder machine using the password we recovered. What port TCP does it listen on?
-> 5985

Submit root flag
->
ea81b7afddd03efaa0945333ed147fac