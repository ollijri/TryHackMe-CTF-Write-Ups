## Investigating Windows

<details>
<summary> Whats the version and year of the windows machine? </summary>
  <p></p>

____________________________________________________________________________________________________________________   
The command ``` winver ``` opens an 'About Windows' box that tells you all you need to know:

![image](https://user-images.githubusercontent.com/66912443/186721361-8fb008bb-147b-4e5f-a580-1abdb8b30668.png)

____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> Which user logged in last? </summary>
  <p></p>

____________________________________________________________________________________________________________________    
Using powershell, running ``` Get-LocalUser | select * ``` will grab all users and the information about them and display that from within the powershell window. From this you can ascertain that Administrator was the last account logged in (yourself not included).
  
![image](https://user-images.githubusercontent.com/66912443/186725969-82e64b11-5eef-4402-bd87-52b16b10ef3e.png)

____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> When did John log onto the system last? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
Using powershell (or cmd, either works) using the command ``` net user john ``` shows all the information you need to know. net user allows the managing of windows local user accounts.

![image](https://user-images.githubusercontent.com/66912443/189335189-c25b2bea-1a19-4414-9495-766d44cf0297.png)

____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> What IP does the system connect to when it first starts? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
 The following cmd window opens when the machine first starts:
 
 ![image](https://user-images.githubusercontent.com/66912443/189335804-9ec41fb1-b48e-4a0a-b760-d9b6623328b7.png)


____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> What two accounts had administrative privileges (other than the Administrator user)? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
The command ``` net localgroup Administrators ``` will print out a list of all administrators on the machine:
  
![image](https://user-images.githubusercontent.com/66912443/189336462-88bbddae-8ed4-4b00-8231-49e6a038927a.png)


____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> Whats the name of the scheduled task that is malicous. </summary>
  <p></p>

____________________________________________________________________________________________________________________  
 'Task Scheduler' can be used to see all scheduled tasks, as the name suggests. In the bottom section, 'Active Tasks' there is a task named 'clean file system' which unlike most tasks, does not use correct capitalisation and is not located in the \Microsoft\ folder.
  
![image](https://user-images.githubusercontent.com/66912443/189337465-3467dcd7-457c-464b-a17b-ff2b732af90a.png)


____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> What file was the task trying to run daily? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
By double clicking the suspicious file, we can see more information about it. From the tabs that appear at the top, we can see it starts the program nc.ps1 which from the looks of it starts a reverse shell.
  
![image](https://user-images.githubusercontent.com/66912443/189337785-51cad53a-7327-40e4-867b-94b4966543d1.png)


____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> What port did this file listen locally for? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
``` Answer = 1348 ```  

____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> When did Jenny last logon? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
Using the command ``` net user jenny ``` we can see jenny has NEVER logged on.
  
![image](https://user-images.githubusercontent.com/66912443/189338166-568ba8ea-d255-490d-a8c6-7f16140a6491.png)

____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> At what date did the compromise take place? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
Still in the task scheduler, scrolling to the very right allows you to view the creation date of the task:
  
![image](https://user-images.githubusercontent.com/66912443/189338598-f8def953-8124-467d-acf3-2ed46775488d.png)

____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> At what time did Windows first assign special privileges to a new logon? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
The previous tasks lets us know the compromise took place on the 3/2/2019 so using the event viewer we can look for special privileges being assigned around that time. There was a lot of special privilges assigned at this time so i must admit I dont fully understand why this one in particular is the one.
  
![image](https://user-images.githubusercontent.com/66912443/189341060-4be0a48c-1523-4b17-92cd-d21afba21f3f.png)

____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> What tool was used to get Windows passwords? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
Along with 'clean file system' there was other suspicious files susch as 'checked logged in' and 'GameOver'. Checking the actions of the 'GameOver' task reveals it is using the 'mim' executable to output the passwords to 'o.txt'.
  
![image](https://user-images.githubusercontent.com/66912443/189342107-fff4be46-c85e-4663-84ec-f1094751bf13.png)

Checking the contents of what should be "o.txt" (called mim-out.txt) exposes the program that was used:
  
![image](https://user-images.githubusercontent.com/66912443/189342376-d7b85915-b06b-4024-98ab-1cad72b34f9a.png)
  
____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> What was the attackers external control and command servers IP? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
The explanation for this can be found in the last question.
  
``` Answer = 76.32.97.132 ```

____________________________________________________________________________________________________________________  
</details>

<details>
<summary> What was the extension name of the shell uploaded via the servers website? </summary>
  <p></p>

____________________________________________________________________________________________________________________ 

 
  
____________________________________________________________________________________________________________________  
  
</details>

<details>
<summary> What was the extension name of the shell uploaded via the servers website? </summary>
  <p></p>

____________________________________________________________________________________________________________________ 

 
  
____________________________________________________________________________________________________________________  
  
</details>
  
  
</details>

<details>
<summary> Check for DNS poisoning, what site was targeted? </summary>
  <p></p>

____________________________________________________________________________________________________________________  
DNS Poisining involves an attacker replacing a DNS database entry with a malicious IP so that when the user would regularly want to go to google.com for example, they would be redirected to an attackers IP instead, which is exactly what is seen below.
  
Using the command ``` Get-DnsClientCache ``` we can view the DNS cache of the computer. As seen in the below screenshot, it is mostly normal except for 'google.com' which has had its ip changed from the standard '8.8.8.8' to '76.32.97.132'.
  
![image](https://user-images.githubusercontent.com/66912443/189345380-77a81275-9b1e-4b90-9610-30cdc6a11c1f.png)


____________________________________________________________________________________________________________________  
  
</details>
