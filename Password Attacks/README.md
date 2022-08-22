## Password Attacking Techniques 

<details>
<summary> Which type of password attack is performed locally? </summary>
<p></p>
Between 'Password Cracking' and 'Password Guessing', <i>'Password Cracking'</i> is the correct answer as this usually involves cracking hashes on the attackers local machine.

</details>

## Password Profiling #1 - Default, Weak, Leaked, Combined , and Username Wordlists

<details>
<summary> What is the Juniper Networks ISG 2000 default password? </summary>
<p></p>

Keeping the default credentials on your device is a huge security risk, and this is exactly what this question is about. By not changing the password you leave your device open to anyone who can do a quick google search and find the user's guide to the device:

<p align="center">
  <img src="https://user-images.githubusercontent.com/66912443/185885338-5fca362b-1de2-4a72-a77f-d1cb88977969.png" >
</p>

This, from the aformentioned official user guide to the 'Juniper Networks ISG 2000' reveals both the username and password to be 'netscreen'
  <p></p>
  
  ``` Source = https://www.juniper.net/documentation/hardware/netscreen-systems/netscreen-systems50/ug_isg_2000.pdf ```

</details>

## Password Profiling #2 - Keyspace Technique and CUPP

<details>
<summary> Run the following crunch command: crunch 2 2 01234abcd -o crunch.txt. How many words did crunch generate? </summary>
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

</details>

## Offline Attacks - Dictionary and Brute-Force

<details>
<summary> 
Considering the following hash: 8d6e34f987851aa599257d3831a1af040886842f. What is the hash type? </summary>
<p></p>

The tool of choice to identify hashes, 'hashid' was not installed on my Linux system by default. This can be fixed with the following command:
  
  ``` sudo apt install hashid ```
  
  Running the following revealed the answer:
  
  ![image](https://user-images.githubusercontent.com/66912443/185891467-ebcb94f8-a836-442f-9316-c7eeec0e9aca.png)

</details>

<details>
<summary> Perform a dictionary attack against the following hash: (The same one) What is the cracked value? Use rockyou.txt. </summary>
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
  
</details>

<details>
<summary> Perform a brute-force attack against the following MD5 hash: e48e13207341b6bffb7fb1622282247b. What is the cracked value? Note the password is a 4 digit number: [0-9][0-9][0-9][0-9] </summary>
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

</details>

## Offline Attacks - Rule-Based

<details>
<summary> What would (be) the syntax you would use to create a rule to produce the following: "S[Word]NN  where N is Number and S is a symbol of !@? </summary>
<p></p>
  
"Az" Specifies there is a word here 
  
  
  "[0-9]" Specifies there is a number. There must be quotations on either side of the closed square brackets and the brackets can be put next to each other for more numbers  
  
  
  "^" Means append a special character to the beginning of each word  
  
  
  "$" Means append a special character to the end of each word
  
  With this all in mind, it can be put together to create the following:
  
  
``` Az"[0-9][0-9]" ^[!@] ``` 

</details>

## Online password attacks

<details>
<summary> Can you guess the FTP credentials without brute-forcing? What is the flag? </summary>
<p></p>

Sometimes FTP servers have an 'anonymous' account left open. This allows access to a server to get information that is publically available, however in this case it can be used for more harm than good. As seen below using the username 'anonymous' with no password gave me access to this ftp server.

  ![image](https://user-images.githubusercontent.com/66912443/185905336-bb588089-1d99-4759-b50f-d12ae52c5447.png)
  
  Listing all reveals a directory known as 'files' which within there lies the flag...
  
  ![image](https://user-images.githubusercontent.com/66912443/185905628-bc810e0d-8669-40ba-a88a-b23a376e3192.png)
  
  Using 'get' the flag is transferred to my machine and the flag is revealed 
  
  ``` THM{d0abe799f25738ad739c20301aed357b} ```
  
</details>

<details>
<summary> What is the password? Note that the password format is as follows: [symbol][dictionary word][0-9][0-9]. </summary>
<p></p>


</details>

<details>
<summary> Perform a brute-forcing attack against the phillips account for the login page at [ip]/login-get using hydra? What is the flag? </summary>
<p></p>


</details>

<details>
<summary> Perform a rule-based password attack to gain access to the burgess account. Find the flag at the following website: [ip]/login-post/. What is the flag? </summary>
<p></p>


</details>


