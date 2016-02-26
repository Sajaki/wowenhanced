Welcome to MangosWeb Enhanced v2. This is a Front end/CMS project for Mangos and Trinity. This project is a continuation of MangosWeb. 
Credits go to Shasha, Nafe, TGM, Peec and Jimmy06 as they are the Original creaters of mangosweb. 
This is just my version of MangosWeb which is more Uptodate, and has alot more features, and fixes then the old site.

# Warning

This version commit and modify your realmd database... I'll try to modify this in the future...

# 1.1 Full Install 

## 1.1a Requirements

* Apache with Mysql & PhP support
	* Apache v2.2/2.4
	* MySQL 5.0.x or higher
	* Php version 5.x
	* GD compiled into Php (In windows, enable GD exetension in php.ini file).

## 1.1b Installing The Site

1. **MAKE SURE** to backup your realmd database before updating or installing!
2. Make sure all files are in the same folder under you "htdocs" or "www" folder
3. Go -> "./config/" and remove the ".dist" at the end of all the config files. For ex. config.xml.dist, should look like this -> config.xml
4. If you want to use the online chat, Remove the ".dist" from the chat config file ("./components/chat/lib/config.php.dist").
5. Go -> "./install/" and rename the `DISABLE_INSTALLER.php`to anything you want.
6. Open your browser and imput your url to your MangosWeb installer (www.yoursite.com/(path_to_your_MangosWeb)/install/)
7. Imput all the requested information like your Emulator, Realm, Character, and World database.
8. Once at step 2, click on "full install sql injection".
9. Once you hit step 3, you need to make a super Admin account. Once completed, your mainsite is installed!
10. Now, go back and rename your old `DISABLE_INSTALLER.php` back to `DISABLE_INSTALLER.php`. This prevents people from hacking into your website.
11. Now its time to configure the Mainsite, open "config/config.xml" MAKE SURE you spend a good amount of time editing the site!
12. To configure the player map, open "config/playermap_config.php"

## 1.1c How To Update

1. **MAKE SURE** to backup your realmd database before updating!
2. Navigate to your MangoWeb Enhanced directory.
3. type `git pull`
4. Check the `/install/sql/updates/` for any new .sql files that need to be installed in your database.

## 1.2 Upgrading From v1

If you are upgrading from version 1 to version 2 of MangosWeb Enhanced, You need to open "/install/sql/updates/old_v1_updates/" and bring your MangosWeb database up to revision 56. Once that is done, run the "/install/sql/updates/upgrade_from_v1.sql" on your realmd database.

# 2. Configurations

## 2.1 Setting Up The News via News Module

The news forum IS SETUP ALREADY set up. To edit any anything, go: "admin panel -> add/edit news"

If you leave Default Component to frontpage, topics you post here will appear on the main page. Very Blizzlike.

## 2.2 Setting Up The Vote System 

* Your server remote access should be turned on (look in your server config file for Ra.Enable).

*If you prefer (most do), you can use SOAP as of patch 3.3.5a. Its setup just like Telnet. Make sure its turned on (look in your server config file for SOAP.Enable). If you choose to have SOAP enabled, you need RA.enabled as well.*

* Your telnet connection to the server remote must be working properly.

[Important] For the remote access user and pass you can use an existing Trinity/Mangos ACCOUNT or to CREATE a new one, BUT...

* Its best if you create an account via your server console. Out of experience, I've noticed that accounts created via the server console, have caused users the least amount of grief.

* For every realm, you must enter the RA/SOAP information to the database. 
	* You can either do this manually by going ->realmd-> realmlist->('ra_port', 'ra_user', and 'ra_pass'). 
	* Or you can do this the easy way by going ->yousite.com->admin panel->realms-> (click your realm name)-> enter your RA info in the fields -> click "update". 

MAKE SURE you copy the username just how it is in the database. It should be all CAPS. 
[NOTE] If using SOAP, make sure the port is the Soap port NOT the RA port.

[NOTE] know that its GM level (The ra account) must be set according to (not lower than) Ra.MinLevel in the server config file and this user must have "send money" and "send items" commands active. If you have any problems, check the ra.commands.log file that your sever creates "C:\YOUR SERVER ROOT\mangos\ra.commands.log"

* Ive also noticed through experiance that if you leave the RA.ip at 0.0.0.0, you will have less issues. (in your server config)

* If using trinity, open your "account_access" table in realmd database. Set realm ID for your telnet account to "-1"

* To adjust the rewards or site links etc. "go -> admin panel -> Vote system Admin"

### NOTE! 

The vote system is disabled through the config. look for `<vote><enable>1</enable></vote>`.
To remove the "click here to vote for us" logo on the frontpage, open "config/config.xml" Find <votebanner><enable>

If you are still having issues with the vote system after reading this, please read "Remote Access" under support, on this page.

## 2.3 Setting Up The Donation System 

The donation system now uses Remote Access (New feature for MWE v2) to send items and Gold because of the changes to the mail and mail_items tables, as well as thhe removal of the characters data fields. To learn how to set up your remote access, read section 2.2 (Setting up the vote system), or Section 3.1 (Remote Access).

1. Create a premier paypal account. (It's free)
2. From the PayPal menu, go to Profile > Under selling Preferences > Instant Payment Notification Preferences.
3. Select Instant notification
4. Enter the full path including your domain name to donate.php in the root of your MaNGOS directory.
Example: http://you-domain-or-ip/subdirectoryifyouhaveone/donate.php

Everyone likes a little pat on the back for their donations, unless they're good samaritans like me...and just doing good deeds is satisfaction enough. If they're not like me :P, then you may want to reward them for their donations

To create, edit, or send donation packs and items, go to: Context menu: > Admin Panel> Donate Admin

TO TEST YOUR DONATION SYSTEM

1. open "donate.php" in your root directory
2. switch the comments out on these lines (24 - 27):
`// If testing on Sandbox use:
//$fp = fsockopen ('ssl://www.sandbox.paypal.com', 443, $errno, $errstr, 30);
$fp = fsockopen ('ssl://www.paypal.com', 443, $errno, $errstr, 30);`

3. go to `https://developer.paypal.com/us/cgi-bin/` and create a sandbox account.
4. go -> login -> click on link "Create a preconfigured buyer or seller account." -> Edit the details to your liking.
5. next go -> test tools -> Instant Payment Notification (IPN) Simulator. -> ... For the IPN handler url, enter the full url to your "donate.php". For payment type, select "eCheck complete" and "payment type "instant".

... Make sure under the "custom" field, you enter a characters guid number, that you can use to test and see if it fully works. Also, for testing purposes, under "item number", enter one on your donation packages, like "1" for example.

6. You should see the information posted in the database, and you should be able to log in with the account that owns the character ID you used, and click "send items to ingame mailbox" on the donate page. log in and check your mailbox :)

## 2.4 Character Copy System

The character copy system is a unique feature that allows admins to set up special accounts, and create max level characters, which users can copy as a reward (much like the "public test realm feature"). As of right now, the only way to charge users for this system is by spending vote points, but who says you cant charge money for that??

There are future plans to add a feature where users can spend real money for these "points", which allows them to use the character rename system, character re-customization, character copy system, and buy the vote rewards.

To set this feature up:
1. create 2 new accounts, 1 for alliance, and 1 for horde characters.
2. on these accounts, go ahead and create a level 80 character with full tier gear.
3. go in the config ->"mangosweb folder/config/config.xml" -> look for -> <character_copy_config> (around line 260).
4. It should already be enabled, all you have to do is edit how many points it costs users to copy a character, and the account numbers to the 2 accounts that you just made.
5. Now go to your site, login, and click "copy character" under account.
6. You should see the level 80 character you created, along with any other characters on that account, listed.

to copy a character to your personal account, click the "copy character" button. The character will be copied to your account, along with whats in his/her bags, and the armor that character is wearing. The realm is decided by which realm you currently have selected.

## 2.5 Advanced Template System

The advanced template system is one of the new features included in MangosWeb Enhanced v2. This new system allows you to make custom templates much easier then before. Please note that in order to attempt to make your own templates for this CMS, you need to know alittle php, mysql, html, and css.

1. First you need to enable the template system in the config: ->./config/config.xml -> <template_system> -> <enable> 1.

2. Next you need to copy all the files from "templates/offlike/", and paste them in a new template folder. For this tutorial, I will refer to this new template folder as "custom".

3. Now you need to start coming up with the design of your new template. create the images, css etc.O nce you have all that, you need to start writing the code to make your design come to life.

4. Open your custom folder -> body_functions.php. The code in here is completly optional. This files purpose is to contain the functions that put your design together.

5. Next open -> custom folder -> body_header.php. The code you place in here will create the top portions of your webpage. example code that should be placed in here is your left, and right backgrounds, your navigation panel, and your server banner or logo's.

6. Next open -> custom folder -> body_footer.php. The code you place in here will create the footer on all the pages. code placed in here should close all open tags (ex: </div></table>), as well as create the copyright info.

7. Next open -> custom folder -> frontpage -> frontpage.index.php. The code you place in here will be displayed on your main page ONLY. the code placed in here should contain mostly the same code as of for the news display, stuff like. but, its your template, do as you please.

8. Now you need to create a new file called "include.php" in your custom root folder (templates/custom/include.php). In this file, put: <?php $pagefiles = "custom"; ?>. Replace custom with your template name.

9. Open your config.xml, and add your template. (config.xml -> templates -> template -> custom). Replace custom with your template name. This will be located towards the bottom. Now you should be able to see your frontpage via your browser

10. Finally, you need to edit each template file from (./templates/ your template name/("account", "admin", "community", "forum", "media", and "server")). You should only need to do slight revising to each template because most of the page's design comes from the body_header.php, and body_footer.php. Make sure you are creating your .css files as well.

Things to keep in mind when writing your code.

1. Most of the script code is written in (./components/$extension/$extension.$subext.php) $extension being "server" or "admin".
2. when writing your code, make sure you also have the script file open so you know how to display the query's and such that are already open. You should just be "revising" the code in each template file.
3. to call your current template: <?php echo $currtmp; ?>
4. to call your template file's template <?php echo $offtmp; ?>

## 2.6 Using PBWoW Forum (extra) 

In this release of MangosWeb, I have included a pre-installed/setup PBWoW Forum, using PBWoW RC4, and phpbb v3.0.7pl1. What is PBWoW you ask? PBWoW is a phpbb mod, that makes your forum look like a blizzlike forums. In order to use these forums, theres only 3 steps.

1. Enable it in your config. look for this:

`<!-- If you want to use external forums ( example Phpbb , you must configure these values) -->
<externalforum>0</externalforum>
<frame_forum>0</frame_forum>
<forum_external_link>LINK HERE</forum_external_link>`

And set it like this:

`<!-- If you want to use external forums ( example Phpbb , you must configure these values) -->
<externalforum>1</externalforum>
<frame_forum>0</frame_forum>
<forum_external_link>forum/</forum_external_link>`

2. Next you need to either create a new database, or just run it on your realmd, its up to you. Run the `./install/sql/extra_install/pbwow_forums.sql` on a database. There is another sql called. `pbwow_forums_blizzlike_setup.sql`. If you run that, all the forum catagories and sub catagories are setup very blizzlike.

3. The final step is editing the config file. go `./forum/config.php` and edit the db username, db password, and db name.

* The admin info to the forums is Username: admin Password: admin1. you should change the password ASAP.
* I have also included the PBWoW readme. its located at `./install/pbwow/PBWoW RC4 readme.pdf`. Make sure to read that before asking for help.

[NOTE] The login info for pbwow is not integrated into MWEv2, so your users will need to create another account via the forums to use the forums.

# 3. Support

## 3.1 Remote Access

The new donation system as well as the vote system use whats called "remote access" to send items and mail to characters in game. Basically the website script tells your server console what to do, using server commands.

If you are having troubles with the vote system, or the donation system, trust me, you arent/werent the only one ever. Here are some cause/effect/fixes for a few things ive learned while helping you guys all out.

1. Errors
A. Telnet connection problem: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed because connected host has failed to respond.

Solution: Make sure your realm is online. Also make sure your server is accepting Remote Access requests. This is checked by opening your server config, and finding ("RA.enable" and "RA.IP" and "RA.port"). Also, make sure your ports forwarded!

B. Telnet connection problem: -Not enough privileges.

Solution: This states that your current account doesnt have a high enough GM level to make the requested command happen. Make sure the account GM level is higher then the RA.minLevel. If using Trinity, make sure that the account has admin access on all realms... go ->realmd->account_access. make sure under realmId, it says "-1"

C. Telnet connection problem: -No such user.

solution: If using mangos, make sure the username is in ALL CAPS, in the config, aswell as the database.

D. Telnet connection problem: (no error)

Open your config.xml and go -> vote_system -> sleep_timer -> and change the 1 to a 2 or 3. The sleep timer is the amount of seconds the script will sleep (halt the script) after ever command sent to the RA. there are 3 commands, 1 -> time to wait after sending username 2 -> time to wait sending the command after loggin in and 3 -> Checking to see if the command was executed properly. So for ever interval you increase the sleep timer, it will slow the RA down by 3 seconds.

2. When all else fails, check you ra_commands.log from your server directory. It will always say what the error was. If you are still having issues, then post them here: https://github.com/saintfrater/wowenhanced/issues

## 3.2 Login Problems

'''Solution 1: regenerate your dynamic site configuration''' Blank out the following in config/config.xml:

`<!-- Dynamic done by site. Dont touch this. -->
<temp>
<site_href>/</site_href>
<site_domain>www.mydomain.com</site_domain>
<email_href>www.mydomain.com</email_href>
<base_href>http://www.mydomain.com/</base_href>
<template_href>/templates/offlike/</template_href>
</temp>`

to look like this:

`<!-- Dynamic done by site. Dont touch this. -->
<temp>
<site_href></site_href>
<site_domain></site_domain>
<email_href></email_href>
<base_href></base_href>
<template_href></template_href>
</temp>`

Then browse to the site, so MangosWeb automatically fills these settings in config.xml. After doing this, your login problems may be solved. If not, proceed to the next solution:

'''Solution 2: Delete Your Cookies'''
This mostly happens when you change this site cookie, but not always. If this doesn't help or you're not able to identify the product possibly responsible for turning the referer header off, please continue to the next solution:

'''Solution 3: Delete account keys'''
Sometimes the website (according to reports on the mangosproject.org forum) doesn't alwasy delete the account key issued at login which is contained in the account_keys table in realmd database. The website basically thinks you are logged in already and will not let you login again. To solve this problem, you can try deleting the keys for people that are having trouble logging in
Note: this seems to be a bigger issue with Firefox than with Internet Explorer.

## 3.3 FAQ 

### 1. Question: How do i add Menu links?

Answer:

'''Step 1'''

You need to decide on a link name and the location that link will point to

i.e. Link name = Myspace
Location = www.myspace.com/yourmyspacepage

'''Step 2'''

Open /lang/en.English.lang with your favorite editor
(this step needs to be repeated for each language you are supporting)

Type this line into the file |=|MS :=: Myspace
(you will see how the others are formatted, also try to put it at the top or bottom so its easy to find later if necessary)

The MS is the pointer you will need to match up later and the Myspace is what will actually show in the menu

'''Step 3'''

Open /core/default_components.php with your favorite editor

On this page you will see all the menus and how they are formatted

Decide which menu you want your link to fall under and goto that section

For our purposes we will use the account menu

Under 2-menuAccount you will see 5 arrays, we are adding the sixth here

at the bottom of the fifth array you will see:
),
),
'3-menuGameGuide' =>
We are adding our link between the first and second ),

It will now look like this
),
6 =>
array (
0 => 'MS',
1 => 'www.myspace.com/yourmyspacepage',
2 => '',
),
),
'3-menuGameGuide' =>

The 0 index in the array is the pointer from the language page you added earlier. It will goto the MS pointer and retrieve Myspace
The 1 index in the array is the destination you want the link to take you to

'''Step 4'''

Close and save all of your changes and you are ready to go! Congratulations!


### 2. Question: How do edit/add quicklinks on the main page?

Answer:

'''Step 1'''

You need to decide on a link name and the location that link will point to

i.e. Link name = Myspace
Location = www.myspace.com/yourmyspacepage

'''Step 2'''

Open /lang/en.English.lang with your favorite editor
(this step needs to be repeated for each language you are supporting)

Type this line into the file |=|MS :=: Myspace
(you will see how the others are formatted, also try to put it at the top or bottom so its easy to find later if necessary)

The MS is the pointer you will need to match up later and the Myspace is what will actually show in the menu

'''Step 3'''

open /templates/offlike/body_right.php with your favorite editor

Add links following this example:

<li class="e">
<a href="<?php echo mw_url('account', 'register'); ?>"><?php echo $lang['quicklink1']; ?></a>
</li>
<li>
<a href="<?php echo mw_url('server', 'realmstatus'); ?>"><?php echo $lang['quicklink3']; ?></a>
</li>

So your would look like this:

li class="e">
<a href="www.myspace.come/yourmyspacepage" /> <?php echo $lang['myspace']; ?></a>
</li>
<li>
<a href="" /></a>
</li>

### 3. Question: How do i use the site with multiple realms?

Answer:
For those of you running multiple realms, it may get alittle confusing to configure the website to feature all realms. So i decided to write a tutorial on how to do it:

1.Open your config.xml, and scroll down to <multirealm>...Change the 0 to a 1.
2.Next, go to the website. Go into the admin panel, and select "Realms" under Site Managment.
3.In the empty fields below, enter you realm information. When you get to the Dbinfo column, enter in this format: "mysql username;mysql password;mysql port;mysql IP address;world database name;character database name". DONT FORGET the semi colon between each field.
4.Click create new realm... A window will pop up asking if your sure, click yes.
5.And boom, you should have it. Please note that all your realms must use the same "realmd" database in order for it to work!


### 4. Question: How do i add my own page into the site?

Answer:
Check out the MangosWeb Enhanced Wiki pages, there is a bunch of tutorials and resources fo you to use there.


## 3.4 Resources

MangosWeb Enhanced Developer Site
MangosWeb Enhanced Forums
MangosWeb Enhanced Google Page
MangosWeb Enhanced Wiki Pages
Issue Tracker / Submit An Issues 
