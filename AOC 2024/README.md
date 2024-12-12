INCOMPLETE MESSY WRITEUP

## Day 1: Maybe SOC-mas music, he thought, doesn't come from a store?

**Looks like the song.mp3 file is not what we expected! Run "exiftool song.mp3" in your terminal to find out the author of the song. Who is the author?** 

As specified in the title, running exiftool against song.mp3 gives the answer

![image](https://github.com/user-attachments/assets/88062853-40bd-4f34-871b-d8a5cc555e8d)

Answer = Tyler Ramsbey

**The malicious PowerShell script sends stolen info to a C2 server. What is the URL of this C2 server?**

Following the activity along leads you to a github address which is hosting the script:
https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1

Within the script is the function "Send-InfoToC2Server". In PowerShell, variables are represented by text strings that begin with a dollar sign ($). You will find the answer. under the variable _$c2Url_.

![image](https://github.com/user-attachments/assets/e062b283-c5f4-42da-8e2e-cbca832b5b8a)

Answer = http://papash3ll.thm/data

**Who is M.M? Maybe his Github profile page would provide clues?**

By doing a basic Github Search for the very identifiable string found within the code of the previous question (Created by the one and only M.M.), this leads us to a profile claiming to be owned by M.M

![image](https://github.com/user-attachments/assets/27a98888-3dfb-42a0-a213-87de874adde8)

![image](https://github.com/user-attachments/assets/dc0e85cd-4603-4180-b19c-f5a45d34279e)

Answer = Mayor Malware

**What is the number of commits on the GitHub repo where the issue was raised?**

Instead of searching for repositories, if we instead search for "Issues", there is an issue titled "python version of this" for a tool called "CryptoWallet-Search" by "Bloatware-WarevilleTHM".

![image](https://github.com/user-attachments/assets/5393c8aa-07cb-4f6f-8af4-b4ccf3059fe4)

By traversing to Bloatware-WarevilleTHM/CryptoWallet-Search (click on the name above the issue) you can see there is 1 commit that has been made.

![image](https://github.com/user-attachments/assets/f6543ff7-5833-438d-a1d8-65f14305d407)

Answer = 1

##  Day 2: One man's false positive is another man's potpourri.

**What is the name of the account causing all the failed login attempts?**

Filter the results event.outcome to "failure" and event.category to "authentication" to see the answer

![image](https://github.com/user-attachments/assets/9bc875f6-ca04-490b-b83b-c5094118307c)

Answer = service_admin

**How many failed logon attempts were observed?**

With the same results filtered as the previous question, look at the number of "hits"

![image](https://github.com/user-attachments/assets/195212e2-ec9e-4a4a-a84f-b0f58b313567)

Answer = 6791

**What is the IP address of Glitch?**

By following the tutorial for this day it will lead you to 6802 events. filtering out the most common source IP will provide the answer.

![image](https://github.com/user-attachments/assets/2caf0312-fb53-43a4-949b-1c0b25fa3946)

![image](https://github.com/user-attachments/assets/dbc0919e-8a1f-4933-97b4-f85696cd92e0)

![image](https://github.com/user-attachments/assets/ac30cf16-4c96-4f07-b896-ce69c869bb06)


Answer = 10.0.255.1

**When did Glitch successfully logon to ADM-01? Format: MMM D, YYYY HH:MM:SS.SSS**

Filtering event.outcome to "success" and adding a filter to the Glitch's IP (10.0.255.1) found in the previous question gives you the answer

![image](https://github.com/user-attachments/assets/5fceaec5-dfa1-4670-bbcf-afeee2420f6a)

Answer = Dec 1, 2024 @ 08:54:39.000

**What is the decoded command executed by Glitch to fix the systems of Wareville?**

The command can be found by resetting the time zone back to 29th Nov - Dec 3rd and removing all filters. This, with the collums applied in the screenshot below will show the encoded string that Glitch supposedly used.

![image](https://github.com/user-attachments/assets/53fdd7a1-2a0d-43fc-a1ce-275f0118af0f)

Chucking the string in cyberchef with the recipe of from base64 coupled with "Remove Null Bytes" will give the answer.

Answer = Install-WindowsUpdate -AcceptAll -AutoReboot









Answer = 

