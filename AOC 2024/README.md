INCOMPLETE MESSY WRITEUP

Day 1: Maybe SOC-mas music, he thought, doesn't come from a store?

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




