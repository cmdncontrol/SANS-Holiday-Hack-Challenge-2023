# SANS Holiday Hack Challenge 2023

---

Objective 1: Holiday Hack Orientation

To start you need to maneuver your boat and dock at Christmas Island: Oritentation

![Picture of boat at sea heading towards Orientation Island](/docs/assets/images/Dock.png)



Task 1: First Terminal Challenge

This is just to get your feet wet, simply enter *answer* to complete the challenge.

![](/docs/assets/images/Orientation.png)

---

Objective 2: Snowball Fight

You could play with another player to fight Santa and win, but that defeats the whole purpose of hacking...

If you look at the source code of the iframe, you will find a singlePlayer variable. You will see that if it is set to "true", a computer player is added to the game allowing you to play solo. 

![](/docs/assets/images/SinglePlayer.png)

Once you load into a private room, you can view the frame info to find the URL the frame is loading from. You will see the singleplayer variable set to false. If you copy the URL and update the <iframe> tag in Inspect with that URL and setting that variable to "true" it will load a single player game. 



Once you defeat Santa, you achieve GLORY!

![](/docs/assets/images/VICTORY.png)



However... why stop there?! You can also use the console once the game is started to alter other variables such as snowballDmg, playersVelocity, santaThrowDelay and more. There's many ways to make this challenge more fun. Pelting elves with no damage taken, who doesn't enjoy that?!

![](/docs/assets/images/Variables.png)

---

Objective 3: Linux 101

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

Objective 4: Reportinator



---

Objective 5: Azure 101

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


