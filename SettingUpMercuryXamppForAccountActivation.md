# Setting Up Mercury Mail In Xampp #

As im sure, many of you guys probably use xampp to host your websites. Whether locally or on the web, Im sure there are a few of you out there who would like to use the "account activation" feature, but dont know how to set up mercury mail in xampp.

For this tutorial, I will be using xampp 1.7.3.

1. Open your php.ini file located at "xampp\php\php.ini". If using older versions of xampp, try "xampp\apache\bin\php.ini.

find this:
```
[mail function]
; For Win32 only.
; http://php.net/smtp
SMTP = localhost
; http://php.net/smtp-port
smtp_port = 25
```

Insert a ";" in front of "SMTP = localhost", and "smtp\_port = 25"

2. Next open ->"xampp\sendmail\sendmail.ini"

Look for this:
```
# A freemail service example
account Hotmail
tls on
tls_certcheck off
host smtp.live.com
from [exampleuser]@hotmail.com
auth on
user [exampleuser]@hotmail.com
password [examplepassword]
```
Enter your info there. Here is an example of what mine looks like:
```
# A freemail service example
account google
tls on
tls_certcheck off
host smtp.gmail.com
from wilson.steven10@gmail.com
auth on
user wilson.steven10@gmail.com
password mygmailpassword
```

3. Next, we will need to configure Mercury Mail.

Lets begin:
Open up MercuryMail and click on configuration and then go to Protocal Modules here we will only check the protocals that we need. The following should only be check:<br />
-MercuryS SMTP Server <br />
-MercuryP POP3 Server <br />
-MercuryC SMTP relaying client <br />
-MercuryD distributing POP3 client <br />
-MecuryI IMAP4rev1 Server <br />
Restart MercuryMail <br />
Once back in mercurymail click on configuration and then go to MercuryC SMTP client and fill in the following information. <br />
Smart host name: smtp.somedomain.com <-your isp smtp server should go here, if you do not know it you can use the services from bluebottle.com <br />
Username: isp username or other mail service username <br />
Password: isp password or other mail service password <br />
then click on save once you have those fields conpleted. <br />
Click on configuration and go to Mercury core module and click on the Local domains tab, then click on add new domain, then add your domain to both the boxes and click on. Next we will add which users will have an email account on your server and to do this click on configuration then go to Manage local users here you can edit, delete, or add users. <br /><br />

4. Now that we have Mercury Mail setup, we need to edit the website "config/config.xml".
Scroll down till you see 

<smtp\_adress>

. Now, enter "localhost" for the username. For the password, enter your password of an account, that you have created under Mercury Mail. The username will obviously be the username that goes with the password.


## Thats it. Now you are all set and should have a working SMTP server on your computer. ##