# PickleRick
A small walk through from try hack me pickle rick challenge, This Rick and Morty themed challenge requires you to exploit a webserver to find 3 ingredients that will help Rick make his potion to transform himself back into a human from a pickle.


#I like to add a brief disclaimer before a writeup to encourage people to attempt the room before reading this article. There will obviously be spoilers in this writeup and I believe you will get more satisfaction from completing the CTF yourself! If you get stuck or you are not sure how to proceed, then I would advise the following:

    Use multiple tools when enumerating the target machine.
    Consider common methods used to escalate privileges.
    Be patient and take regular breaks. You may notice something you didn’t see before with a fresh pair of eyes!
    
    
![1*NyFGzFrfb1kigLJ3QcIABQ](https://user-images.githubusercontent.com/79510640/119017388-f4384d80-b968-11eb-8b6a-5819e9335f1e.png)

#my notes : 
QMARK CTF

Task 1 :
#For all three flags

#Do a nmap scan against the machine IP using the command  "sudo nmap -sV -A 10.10.99.86 | tee nmapout.txt "

#Two ports Open "22, 80"

#Port 80 has a website hosted, use burp suit open the IP inside the burp

#On checking the source code  "Username: R1ckRul3s" was found

#Lets do a gobuster scan against the IP using the command   " sudo gobuster -u http://10.10.99.86/ dir -w gobusterwordlist.txt -x .txt,php | tee gobusterout.txt"

#Found interesting location that has to checked 

#Found some string character in /robots.txt

#use the username and password found to bypass the login on /login.php

#Command panel page allows us to enter command lets try some command 

#"pwd" to print the current working directory, "ls" to list the files

#use the command less and the filename to show the first ingridiant



-----------------------------------------------------------------------------
First ingrediant is solved

#on looking burp suit the backend of /portal.php few strings are there looks like base64 lets use the base64 decode feature inbuilt in burp suit

#after few filteration "rabbit hole" is the string what we got from it

#Since we know we can execute the commands lets try pentest money cheat sheet http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet or i have  filtered version of cheatcode.txt do have a look at it, lets try onebyone PERL reverse shell works just replace with the local ip and port 

#Use NetCat "nc -lvnp 4444" lets start to listen the connection on port 4444 

#cd /home/rick gives the secong ingridiant 

#cat "second ingredients" 1 jerry tear is the out string


-----------------------------------------------------------------------------
Second ingrediant is solved

#lets try sudo -l to cheat weather we can login without any password

#yeah we can so use the command "sudo su"  now  "id" shows we are root now /root

#"ls" gives the 3rd.txt cat 3rd.txt reveals the 3rd ingredients: fleeb juice

-----------------------------------------------------------------------------
Third ingrediant is solved
