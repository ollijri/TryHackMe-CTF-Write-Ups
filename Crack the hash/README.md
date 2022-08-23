## Level 1 

<details>
<summary> 48bb6e862e54f2a795ffc4e541caed4d </summary>
  <p></p>
  
  Using hashes.com, we can identify this hash as an MD5 hash.
  
  ![image](https://user-images.githubusercontent.com/66912443/186166155-2bf7be2f-0ace-46a8-a94a-6425344bbe84.png)

  Now we know the type of hash, we can put it in hashcat using rockyou.txt as the dictionary to crack the hash.
  
  ``` hashcat -m 0 -a 0 48bb6e862e54f2a795ffc4e541caed4d /usr/share/wordlists/rockyou.txt ```
  
  ![image](https://user-images.githubusercontent.com/66912443/186166005-5c9ad0a4-d8ae-4c0e-af74-2185102948a7.png)

  
  <p></p>
  Alternatively, https://crackstation.net/ immediately cracks this hash
  
</details>

<details>
<summary> CBFDAC6008F9CAB4083784CBD1874F76618D2A97 </summary>
  <p></p>
  
  Using hash-identifier, we can ascertain that the hash is "SHA1" which, when using the hashcat hash types table we can see that this requires "-m 100" instead of "-m 0" like above.
  
  ![image](https://user-images.githubusercontent.com/66912443/186172578-a7a8f548-1587-41fe-854e-3567e1db0862.png)

  Now we know the type of hash, we can put it in hashcat using rockyou.txt as the dictionary to crack the hash.
  
  ``` hashcat -m 100 -a 0 CBFDAC6008F9CAB4083784CBD1874F76618D2A97 /usr/share/wordlists/rockyou.txt ```
  
  ![image](https://user-images.githubusercontent.com/66912443/186172982-a38b23bd-5e39-4893-b29c-a6c28f6f6fb7.png)

  
  Alternatively, using hashes.com immediately identifies and tells us the hash.
  
  ![image](https://user-images.githubusercontent.com/66912443/186169319-cece8fbc-4700-4c9c-af7b-07369a362e20.png)
  
</details>

<details>
<summary> 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 </summary>
  <p></p>
  
  Using hash-id we can work out that this hash is encrypted using SHA-256
  
  ![image](https://user-images.githubusercontent.com/66912443/186173198-7973eeaa-0703-4a32-8cb6-687ea1d07350.png)
  
  Using the hashcat table again we can see that the code for SHA-256 is 1400
  
  ![image](https://user-images.githubusercontent.com/66912443/186174013-bf91bf8e-2b34-402b-ae98-89135b748d48.png)

  Now we know the type of hash and the code, we can put it in hashcat using rockyou.txt as the dictionary to crack the hash.
  
  ``` hashcat -m 1400 -a 0 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 /usr/share/wordlists/rockyou.txt ```
  
![image](https://user-images.githubusercontent.com/66912443/186173873-aabcb898-738d-461d-9d3c-57cabde353d2.png)

  
</details>

<details>
<summary> $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom </summary>
  <p></p>
  Using hash-id, we can see that this hash is encrypted using 'Blowfish':
  <p></p>
  
  ![image](https://user-images.githubusercontent.com/66912443/186167016-037ff407-050d-47e9-8bfa-30723d8b745d.png)
  
  Now we know this, we can use hashcat's hash type table to workout the flag code:
  
  ![image](https://user-images.githubusercontent.com/66912443/186172325-5d3ea250-1455-47d0-99da-c9c1cccea863.png)
  
  Using the command below the hash will start and eventually be cracked, this is completely dependent on the speed of your machine: (this one may take forever)
  
 ``` hashcat -m 3200 -a 0 $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom /usr/share/wordlists/rockyou.txt ```
  
  Answer = bleh
  
</details>

<details>
<summary> 279412f945939ba78ce0758d3fd83daa </summary>
  <p></p>
 
Using hash-identifier we can work out this hash is MD4, referencing the hashcat table once again we know to use "-m 900" for use in hashcat.
  
![image](https://user-images.githubusercontent.com/66912443/186174489-291599a1-7dc3-4073-973a-bbd9b0e818bb.png)

``` hashcat -m 900 -a 0 279412f945939ba78ce0758d3fd83daa /usr/share/wordlists/rockyou.txt ```
  
Just like all times before, we know the type of hash and the code so we can put it in hashcat using rockyou.txt as the dictionary to crack the hash.
  

  
Alternitively, Hashes.com immediately tells us this again.

![image](https://user-images.githubusercontent.com/66912443/186169603-5361aec2-9321-4e7b-bf11-f00ff90699c7.png)

  </details>

## Level 2

