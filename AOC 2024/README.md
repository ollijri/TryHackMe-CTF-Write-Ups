INCOMPLETE MESSY WRITEUP

## Day 1: Maybe SOC-mas music, he thought, doesn't come from a store?

<details>
<summary> Looks like the song.mp3 file is not what we expected! Run "exiftool song.mp3" in your terminal to find out the author of the song. Who is the author? </summary>
  <p></p>

____________________________________________________________________________________________________________________

As specified in the title, running exiftool against song.mp3 gives the answer

![image](https://github.com/user-attachments/assets/88062853-40bd-4f34-871b-d8a5cc555e8d)

```Answer = Tyler Ramsbey```
____________________________________________________________________________________________________________________

</details>

<details>
<summary> The malicious PowerShell script sends stolen info to a C2 server. What is the URL of this C2 server? </summary>
  <p></p>

____________________________________________________________________________________________________________________
Following the activity along leads you to a github address which is hosting the script:
https://raw.githubusercontent.com/MM-WarevilleTHM/IS/refs/heads/main/IS.ps1

Within the script is the function "Send-InfoToC2Server". In PowerShell, variables are represented by text strings that begin with a dollar sign ($). You will find the answer. under the variable _$c2Url_.

![image](https://github.com/user-attachments/assets/e062b283-c5f4-42da-8e2e-cbca832b5b8a)

```Answer = http://papash3ll.thm/data```
____________________________________________________________________________________________________________________

</details>

<details>
<summary> Who is M.M? Maybe his Github profile page would provide clues? </summary>
  <p></p>

____________________________________________________________________________________________________________________
By doing a basic Github Search for the very identifiable string found within the code of the previous question (Created by the one and only M.M.), this leads us to a profile claiming to be owned by M.M

![image](https://github.com/user-attachments/assets/27a98888-3dfb-42a0-a213-87de874adde8)

![image](https://github.com/user-attachments/assets/dc0e85cd-4603-4180-b19c-f5a45d34279e)

```Answer = Mayor Malware```

____________________________________________________________________________________________________________________

</details>

<details>
<summary> What is the number of commits on the GitHub repo where the issue was raised? </summary>
  <p></p>

____________________________________________________________________________________________________________________

Instead of searching for repositories, if we instead search for "Issues", there is an issue titled "python version of this" for a tool called "CryptoWallet-Search" by "Bloatware-WarevilleTHM".

![image](https://github.com/user-attachments/assets/5393c8aa-07cb-4f6f-8af4-b4ccf3059fe4)

By traversing to Bloatware-WarevilleTHM/CryptoWallet-Search (click on the name above the issue) you can see there is 1 commit that has been made.

![image](https://github.com/user-attachments/assets/f6543ff7-5833-438d-a1d8-65f14305d407)

```Answer = 1```

____________________________________________________________________________________________________________________

</details>

##  Day 2: One man's false positive is another man's potpourri.

</details>

<details>
<summary> What is the name of the account causing all the failed login attempts? </summary>
  <p></p>

____________________________________________________________________________________________________________________
Filter the results event.outcome to "failure" and event.category to "authentication" to see the answer

![image](https://github.com/user-attachments/assets/9bc875f6-ca04-490b-b83b-c5094118307c)

```Answer = service_admin```
____________________________________________________________________________________________________________________

</details>

<details>
<summary> How many failed logon attempts were observed? </summary>
  <p></p>

____________________________________________________________________________________________________________________
With the same results filtered as the previous question, look at the number of "hits"

![image](https://github.com/user-attachments/assets/195212e2-ec9e-4a4a-a84f-b0f58b313567)

```Answer = 6791```
____________________________________________________________________________________________________________________

</details>

<details>
<summary> What is the IP address of Glitch? </summary>
  <p></p>

____________________________________________________________________________________________________________________
By following the tutorial for this day it will lead you to 6802 events. filtering out the most common source IP will provide the answer.

![image](https://github.com/user-attachments/assets/2caf0312-fb53-43a4-949b-1c0b25fa3946)

![image](https://github.com/user-attachments/assets/dbc0919e-8a1f-4933-97b4-f85696cd92e0)

![image](https://github.com/user-attachments/assets/ac30cf16-4c96-4f07-b896-ce69c869bb06)


```Answer = 10.0.255.1```
____________________________________________________________________________________________________________________

</details>

<details>
<summary> When did Glitch successfully logon to ADM-01? Format: MMM D, YYYY HH:MM:SS.SSS </summary>
  <p></p>

____________________________________________________________________________________________________________________
Filtering event.outcome to "success" and adding a filter to the Glitch's IP (10.0.255.1) found in the previous question gives you the answer

![image](https://github.com/user-attachments/assets/5fceaec5-dfa1-4670-bbcf-afeee2420f6a)

```Answer = Dec 1, 2024 @ 08:54:39.000```
____________________________________________________________________________________________________________________

</details>

<details>
<summary> What is the decoded command executed by Glitch to fix the systems of Wareville? </summary>
  <p></p>

____________________________________________________________________________________________________________________
The command can be found by resetting the time zone back to 29th Nov - Dec 3rd and removing all filters. This, with the collums applied in the screenshot below will show the encoded string that Glitch supposedly used.

![image](https://github.com/user-attachments/assets/53fdd7a1-2a0d-43fc-a1ce-275f0118af0f)

Chucking the string in cyberchef with the recipe of from base64 coupled with "Remove Null Bytes" will give the answer.

```Answer = Install-WindowsUpdate -AcceptAll -AutoReboot```
____________________________________________________________________________________________________________________

</details>

##  Day 3: Even if I wanted to go, their vulnerabilities wouldn't allow it.

<details>
<summary> Where was the web shell uploaded to? </summary>
  <p></p>

____________________________________________________________________________________________________________________

As we know this is a web shell upload, we can stick with "message: "shell.php"" in the KQL search bar. This gives us a number of alerts, the top result gives us the answer.

![image](https://github.com/user-attachments/assets/d7422662-1a2e-459f-8a2b-75823ed75dc8)

```Answer = /media/images/rooms/shell.php```
____________________________________________________________________________________________________________________


</details>


<details>
<summary> What IP address accessed the web shell? </summary>
  <p></p>

____________________________________________________________________________________________________________________
By exploring the alerts, we can find one that accessed a full directory and inputted a command into the web shell. The IP can be found at the beginning of the "message" field of this alert.

![image](https://github.com/user-attachments/assets/c8fcaf47-bba1-4bcd-8933-b1a86e6a2257)

```Answer = 10.11.83.34```
____________________________________________________________________________________________________________________


</details>


<details>
<summary> What is the contents of the flag.txt? </summary>
  <p></p>

____________________________________________________________________________________________________________________

This can be found by using the search bar on the browser to go to the same directory that shell.php is stored in, but swapping "shell.php" for "flag.txt"

![image](https://github.com/user-attachments/assets/4cf5282c-f568-453d-a2a3-34f62ac75b58)

```Answer = THM{Gl1tch_Was_H3r3}```
____________________________________________________________________________________________________________________

</details>
