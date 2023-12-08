





# SANS Holiday Hack Challenge 2023

---

Objective: Holiday Hack Orientation

To start you need to maneuver your boat and dock at Christmas Island: Oritentation

![Picture of boat at sea heading towards Orientation Island](/docs/assets/images/Dock.png)

Task 1: First Terminal Challenge

This is just to get your feet wet, simply enter *answer* to complete the challenge.

![](/docs/assets/images/Orientation.png)

---

Objective: Snowball Fight

You could play with another player to fight Santa and win, but that defeats the whole purpose of hacking...

If you look at the source code of the iframe, you will find a singlePlayer variable. You will see that if it is set to "true", a computer player is added to the game allowing you to play solo. 

![](/docs/assets/images/SinglePlayer.png)

Once you load into a private room, you can view the frame info to find the URL the frame is loading from. You will see the singleplayer variable set to false. If you copy the URL and update the <iframe> tag in Inspect with that URL and setting that variable to "true" it will load a single player game. 

Once you defeat Santa, you achieve GLORY!

![](/docs/assets/images/VICTORY.png)

However... why stop there?! You can also use the console once the game is started to alter other variables such as snowballDmg, playersVelocity, santaThrowDelay and more. There's many ways to make this challenge more fun. Pelting elves with no damage taken, who doesn't enjoy that?!

![](/docs/assets/images/Variables.png)

---

Objective: Linux 101

Task 1: Perform a directory listing of your home directory to find a troll and retrieve a present!

Answer: *ls*

Task 2: Now find the troll inside the troll.

Answer: *cat troll 19315479765589239*

Task 3: Great, now remove the troll in your home directory.

Answer: *rm troll 19315479765589239*

Task 4: Print the present working directory using a command.

Answer: *pwd*

Task 5: Good job but it looks like another troll hid itself in your home directory. Find the hidden troll!

Use ls -la to reveal hidden files

Answer: *cat .troll_5074624024543078*

Task 6: Excellent, now find the troll in your command history.

Answer: *history*

Task 7: Find the troll in your environment variables.

Answer: *env*

Task 8: Next, head into the workshop.

Answer: *cd workshop*

Task 9: A troll is hiding in one of the workshop toolboxes. Use "grep" while ignoring case to find which toolbox the troll is in.

Answer: *grep -ri "troll"*

Task 10: 

chmod +x present engine to make the file executable

Answer: *./present engine*

Task 11: Trolls have blown the fuses in /home/elf/workshop/electrical. cd into electrical and rename blown_fuse0 to fuse0.

Change to the proper directory using cd

Answer: *mv blown fuse0 fuse0*

Task 12:  Now, make a symbolic link (symlink) named fuse1 that points to fuse0

Answer: *ln -s fuse0 fuse1*

Task 13: Make a copy of fuse1 named fuse2.

Answer: *cp fuse1 fuse2*

Task 14: We need to make sure trolls don't come back. Add the characters "TROLL_REPELLENT" into the file fuse2

Answer: *echo "TROLL_REPELLENT" > fuse2*

Task 15: Find the troll somewhere in /opt/troll_den.

Answer: *find /opt/troll_den/ -iname "troll*"*

 Task 16: Find the file somewhere in /opt/troll_den that is owned by the user troll.

Answer: *find /opt/troll_den/ -user "troll"*

Task 17: Find the file created by trolls that is greater than 108 kilobytes and less than 110 kilobytes located somewhere in /opt/troll_den.

Answer: *find /opt/troll_den/ -size +108k -size -110k*

Task 18: List running processes to find another troll

Answer: *ps aux*

Task 19: The 14516_troll process is listening on a TCP port. Use a command to have the only listening port display to the screen.

Answer: *netstat -l*

Task 20: The service listening on port 54321 is an HTTP server. Interact with this server to retrieve the last troll.

Answer: *curl 0.0.0.0:54321*

Task 21: Your final task is to stop the 14516_troll process to collect the remaining presents.

Answer: *kill 12771*

---

Objective: Reportinator

---

Objective: Azure 101

Task 1: You may not know this but the Azure cli help messages are very easy to access. First, try typing:
$ az help | less

Answer: *az help | less*

Task 2: Next, you've already been configured with credentials. Use 'az' and your 'account' to 'show' your current details and make sure to pipe to less ( | less )

Answer: *az account show | less*

![]()

Task 3: Excellent! Now get a list of resource groups in Azure.
For more information:
https://learn.microsoft.com/en-us/cli/azure/group?view=azure-cli-latest

Answer: *az group list*

![](/docs/assets/images/azgroup.png)

Task 4: Ok, now use one of the resource groups to get a list of function apps. For more information:
https://learn.microsoft.com/en-us/cli/azure/functionapp?view=azure-cli-latest
Note: Some of the information returned from this command relates to other cloud assets used by Santa and his elves.

Answer: *az functionapp list -g "northpole-rg1"*

You could've also used northpole-rg2 here. This also revealed an interesting URL: https://northpole-ssh-certs-fa.azurewebsites.net/api/create-cert?code=candy-cane-twirl

![](/docs/assets/images/azfunctionapp.png)

Task 5: Find a way to list the only VM in one of the resource groups you have access to.
For more information:
https://learn.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest

Answer: *az vm list -g "northpole-rg2"*

![](/docs/assets/images/azvms.png)

Task 6: Find a way to invoke a run-command against the only Virtual Machine (VM) so you can RunShellScript and get a directory listing to reveal a file on the Azure VM.
For more information:
https://learn.microsoft.com/en-us/cli/azure/vm/run-command?view=azure-cli-latest#az-vm-run-command-invoke

Answer: az vm run-command invoke -g northpole-rg2 -n NP-VM1 --command-id RunShellScript --scripts "ls"

![](/docs/assets/images/azls.png)

---

Objective: Elf Hunt

After reading about JSON Web Tokens (JWTs), I learned about a flaw to force the server to accept a token with no signature present. I found a cookie that appeared to be the JWT for Elf Hunt called "ElfHunt_JWT". The JWT was already flawed since the "alg" parameter was set to none, which made my job easier. I simply had to decode the cookie using CyberChef. It took a few tries messing around with the speed until the elves were just fast enough...

Original Cookie: eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJzcGVlZCI6LTUwMH0. 

Decoded Original: {"alg":"none","typ":"JWT"}>{"speed":-500}>

Answer: I ended up finding that -50 was a good speed. I replaced the cookie in my session with my new base64 encoded speed variable. The full cookie value became *eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJzcGVlZCI6LTUwfT4.*

GLORY:

![](/docs/assets/images/elfhunt.png)

---

Objective: Certificate SSHenanigans

Domain: **ssh-server-vm.santaworkshopgeeseislands.org** 

Account: **monitor**

Goal: **access TODO list**

---

Objective: Faster Lock Combination

When applying tension to the shackle and turning the dial clockwise, the number that the lock repeatedly hangs on is the sticky number. 

Sticky Number: 20

When applying heavy tension to the shackle and turning the lock counter clockwise, the numbers we are looking for will sit between two half numbers and will be between 0-11

Guess Number 1: 0

Guess Number 2: 3

First Digit: Sticky Number + 5 = ***25***

Third Digit: 13  OR 33, 13 feels more loose when applying tension to the shackle so we can eliminate 33 as an option

Third Digit Process: 

First Digit/4 = 6 with remainder of 1

Guess Numbers: 0 & 3

0    10    20   30

3    13    23    33

13/4 = 4 with remainder of 1 & 33/4 = 8 with remainder of 1

Second Digit Process:

First Row Below: Remainder + 2  = 3

Add 8 to it 4 times, exceeding 39 resets to 0

Second Row Below: remainder + 2 + 4 = 7

Add 8 to it 4 times, exceeding 39 resets to 0

3    ~~11~~    19    27    35

7    ~~15~~     23    31    39

The second and third digit on the lock cannot be within 2 digits of eachother, we can eliminate 15 & 17 from our second digit guesses. 

After trying the 8 options, our true combination is: 25, 39, 13!

If you want to "hack" the challenge instead, you can look at the javascript variables in the iframe to reveal the combination for your session. The variable that holds the combination is: lock_numbers

![]()

You can also edit the lock combination that the game is looking for if you'd like. This just makes it faster to solve the combo :D 

![]()

---

Objective: Phish Detection Agency

Valid SPF: 

| Domain           | Type | Value                               |
| ---------------- | ---- | ----------------------------------- |
| geeseislands.com | TXT  | v=spf1 a:mail.geeseislands.com -all |

Valid DKIM:

| Domain           | Type | Value                                                                                                                                                                                                                                  |
| ---------------- | ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| geeseislands.com | TXT  | v=DKIM1;t=s;p=MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDjtqsLqwecFGF7AmP+Siln86O1v9NOKJw4ZsEHDV5fo0Vjj0qNPyyARKSkDmnIKjnzLGUUQO31Fr+vdZU61IaI9/ZD39WJKaAeX96uQ65mRQqqPVYxPLN5OvuFRmIHJ/TgOkD6z5/7VM7Zs1kw5Qnl04FmOLwWd00D+uNZnj8TCwIDAQAB |

Valid DMARC:

| Domain           | Type | Value                                                                  |
| ---------------- | ---- | ---------------------------------------------------------------------- |
| geeseislands.com | TXT  | v=DMARC1; p=reject; pct=100; rua=mailto:dmarc-reports@geeseislands.com |

In this challenge we had to weed through all the emails in the Inbox along with those that were already in the Phishing folder to determine if ChatNPT properly assessed the emails. The key piecees to look at in the email headers displayed was:

Return-Path - if the return path was not for emailaddress@geeseislands.com the email should be marked as malicious, as all mail is expected to be from that domain in this challenge

DMARC - if this value is set to "Fail", you can assume phishing in this challenge

DKIM-Signature - if the domain value (d=) in the signature is not geeseislands.com, you can assume it is a phishing email OR if this is just showing "Invalid"

Recieved - If the received field is from a different domain than the expected sender of geeseislands.com, you can assume it is a phishing email

Phish email example 1:

![](/docs/assets/images/phish1.png)

Phish email example 2:

![](/docs/assets/images/phish2.png)

Valid email example 1:

![](/docs/assets/images/valid1.png)

GLORY:

![](/docs/assets/images/acedetect.png)

---

Objective: Na'an

If you cover both the numerical low (0) and high (9) and use NaN as one of the options, the other numbers you place do not matter. The evaluation will fail in your favor. As long as you cover the extremes, NaN will be seen as winner for both min and max due to the python evaluation error. 

GLORY:

![](/docs/assets/images/nan.png)

---

Operation: Kusto Detective

Onboarding: How many craftperson elves are using laptops?

![](/docs/assets/images/kd1.png)

Answer: *25*

Case 1: Welcome to Operation Giftwrap: Defending the Geese Island network

Question 1: What is the email address of the employee who received this phishing email?

![](/docs/assets/images/kd2.png)

Answer: *alabaster_snowball@santaworkshopgeeseislands.org*

Question 2: What is the email address that was used to send this spear phishing email?

![](/docs/assets/images/kd3.png)

Answer: *cwombley@gmail.com*

Question 3: What was the subject line used in the spear phishing email?

![](/docs/assets/images/kd4.png)

Answer: *[EXTERNAL] Invoice foir reindeer food past due*

Case 2: Someone got phished! Let's dig deeper on the victim...

Question 1: What is the role of our victim in the organization?

![](/docs/assets/images/kd5.png)

Answer: *Head Elf*

Question 2: What is the hostname of the victim's machine?

![](/docs/assets/images/kd6.png)

Answer: *Y1US-DESKTOP*

Question 3: What is the source IP linked to the victim?

![](/docs/assets/images/kd7.png)

Answer: *10.10.0.4*

Case 3: That's not good. What happened next?

Question 1: What time did Alabaster click on the malicious link? Make sure to copy the exact timestamp from the logs!

![](/docs/assets/images/kd8.png)

Answer: *2023-12-02T10:12:42Z*

Question 2: What file is dropped to Alabaster's machine shortly after he downloads the malicious file?

![](/docs/assets/images/kd9.png)

Answer: *giftwrap.exe*

Case 4: A compromised host! Time for a deep dive.

Question 1: The attacker created an reverse tunnel connection with the compromised machine. What IP was the connection forwarded to?

![](/docs/assets/images/kd10.png)

Answer: *113.37.9.17*

Question 2: What is the timestamp when the attackers enumerated network shares on the machine?

![](/docs/assets/images/kd11.png)

Answer: *2023-12-02 16:51:44.0000000*

Question 3: What was the hostname of the system the attacker moved laterally to?

![](/docs/assets/images/kd12.png)

Answer: *NorthPolefileshare*

Case 5: A hidden message

Question 1: When was the attacker's first base64 encoded PowerShell command executed on Alabaster's machine?

![](/docs/assets/images/kd13.png)

Answer: *2023-12-24 16:07:47.0000000*

Question 2: What was the name of the file the attacker copied from the fileshare? (This might require some additional decoding)

We can check out the first encoded powershell command after the attacker accessed the fileshare.

![](/docs/assets/images/kd14.png)

After base64 decoding, we can see that this is also reversed. We can use the reverse() command to assist here and reveal the answer.

![]()

Answer: *NaughtyNiceList.txt*

Question 3: The attacker has likely exfiltrated data from the file share. What domain name was the data exfiltrated to?

We can review the next powershell command after the file was copied. 

![](/docs/assets/images/kd16.png)

After base64 decoding, we can see that this command is also encoded in decimal. We need to convert this to ASCII for it to be easily legible.

![](/docs/assets/images/kd17.png)

I used: [charcode encoder-decoder](https://codepen.io/HerbertAnchovy/pen/XLzdYr) to decode the char decimal into ASCII, which revealed our answer.

![](/docs/assets/images/kd18.png)

Answer: *giftbox.com*

Case 6: The final step!

Question 1: What is the name of the executable the attackers used in the final malicious command?

To start we need to find the last encoded powershell command ran by the attacker![](/docs/assets/images/kd19.png)We can base64 decode it to reveal our answer.

![]()

Answer: *downwithsanta.exe*

Question 2: What was the command line flag used alongside this executable?

We can use the same decoded powershell to find the answer for this question.

![](/docs/assets/images/kd20.png)

Answer: *--wipeall*
