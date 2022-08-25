<p align="center">
  <img src="https://user-images.githubusercontent.com/66912443/186184549-6e5854f9-6ff6-4883-aca8-0c53c57b4a94.png">
</p>

____________________________________________________________________________________________________________________

## Level 1 

<details>
<summary> 48bb6e862e54f2a795ffc4e541caed4d </summary>

____________________________________________________________________________________________________________________

  <p></p>
  
  Using hashes.com, we can identify this hash as an MD5 hash.
  
  ![image](https://user-images.githubusercontent.com/66912443/186166155-2bf7be2f-0ace-46a8-a94a-6425344bbe84.png)

  Now we know the type of hash, we can put it in hashcat using rockyou.txt as the dictionary to crack the hash.
  
  ``` hashcat -m 0 -a 0 48bb6e862e54f2a795ffc4e541caed4d /usr/share/wordlists/rockyou.txt ```
  
  ![image](https://user-images.githubusercontent.com/66912443/186166005-5c9ad0a4-d8ae-4c0e-af74-2185102948a7.png)

  
  <p></p>
  Alternatively, https://crackstation.net/ immediately cracks this hash
  
  ____________________________________________________________________________________________________________________
</details>

<details>
<summary> CBFDAC6008F9CAB4083784CBD1874F76618D2A97 </summary>

____________________________________________________________________________________________________________________

  <p></p>
  
  Using hash-identifier, we can ascertain that the hash is "SHA1" which, when using the hashcat hash types table we can see that this requires "-m 100" instead of "-m 0" like above.
  
  ![image](https://user-images.githubusercontent.com/66912443/186172578-a7a8f548-1587-41fe-854e-3567e1db0862.png)

  Now we know the type of hash, we can put it in hashcat using rockyou.txt as the dictionary to crack the hash.
  
  ``` hashcat -m 100 -a 0 CBFDAC6008F9CAB4083784CBD1874F76618D2A97 /usr/share/wordlists/rockyou.txt ```
  
  ![image](https://user-images.githubusercontent.com/66912443/186172982-a38b23bd-5e39-4893-b29c-a6c28f6f6fb7.png)

  
  Alternatively, using hashes.com immediately identifies and tells us the hash.
  
  ![image](https://user-images.githubusercontent.com/66912443/186169319-cece8fbc-4700-4c9c-af7b-07369a362e20.png)
  
  ____________________________________________________________________________________________________________________
</details>

<details>
<summary> 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 </summary>

____________________________________________________________________________________________________________________

  <p></p>
  
  Using hash-id we can work out that this hash is encrypted using SHA-256
  
  ![image](https://user-images.githubusercontent.com/66912443/186173198-7973eeaa-0703-4a32-8cb6-687ea1d07350.png)
  
  Using the hashcat table again we can see that the code for SHA-256 is 1400
  
  ![image](https://user-images.githubusercontent.com/66912443/186174013-bf91bf8e-2b34-402b-ae98-89135b748d48.png)

  Now we know the type of hash and the code, we can put it in hashcat using rockyou.txt as the dictionary to crack the hash.
  
  ``` hashcat -m 1400 -a 0 1C8BFE8F801D79745C4631D09FFF36C82AA37FC4CCE4FC946683D7B336B63032 /usr/share/wordlists/rockyou.txt ```
  
![image](https://user-images.githubusercontent.com/66912443/186173873-aabcb898-738d-461d-9d3c-57cabde353d2.png)

  ____________________________________________________________________________________________________________________
  
</details>

<details>
<summary> $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom </summary>

____________________________________________________________________________________________________________________

  <p></p>
  Using hash-id, we can see that this hash is encrypted using 'Blowfish':
  <p></p>
  
  ![image](https://user-images.githubusercontent.com/66912443/186167016-037ff407-050d-47e9-8bfa-30723d8b745d.png)
  
  Now we know this, we can use hashcat's hash type table to workout the flag code:
  
  ![image](https://user-images.githubusercontent.com/66912443/186172325-5d3ea250-1455-47d0-99da-c9c1cccea863.png)
  
  Using the command below the hash will start and eventually be cracked, this is completely dependent on the speed of your machine: (this one may take forever)
  
 ``` hashcat -m 3200 -a 0 $2y$12$Dwt1BZj6pcyc3Dy1FWZ5ieeUznr71EeNkJkUlypTsgbX1H68wsRom /usr/share/wordlists/rockyou.txt ```
  
  Answer = bleh
  
 ____________________________________________________________________________________________________________________ 
 
</details>

<details>
<summary> 279412f945939ba78ce0758d3fd83daa </summary>

____________________________________________________________________________________________________________________

  <p></p>
 
Using hash-identifier we can work out this hash is MD4, referencing the hashcat table once again we know to use "-m 900" for use in hashcat.
  
![image](https://user-images.githubusercontent.com/66912443/186174489-291599a1-7dc3-4073-973a-bbd9b0e818bb.png)

``` hashcat -m 900 -a 0 279412f945939ba78ce0758d3fd83daa /usr/share/wordlists/rockyou.txt ```
  
Just like all times before, we know the type of hash and the code so we can put it in hashcat using rockyou.txt as the dictionary to crack the hash.
  

  
Alternitively, Hashes.com immediately tells us this again.

![image](https://user-images.githubusercontent.com/66912443/186169603-5361aec2-9321-4e7b-bf11-f00ff90699c7.png)

  ____________________________________________________________________________________________________________________
  
  </details>

## Level 2

<details>
<summary> F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85 </summary>

____________________________________________________________________________________________________________________

  <p></p>
  Using Hashes.com we can work out the algorithm used is SHA256
  <p></p>
  
  ![image](https://user-images.githubusercontent.com/66912443/186175646-c3f54f75-ea8d-4ca7-b4ba-abd234a4bd42.png)

  From the previous examples we know the SHA256 flag code is "1400". Therefore the command for hashcat is as follows:
  
  ``` hashcat -m 1400 -a 0 F09EDCB1FCEFC6DFB23DC3505A882655FF77375ED8AA2D1C13F640FCCC2D0C85 /usr/share/wordlists/rockyou.txt ```
  
![image](https://user-images.githubusercontent.com/66912443/186176107-0ec6c284-f6d1-481c-8cbc-1641fe889c5e.png)

____________________________________________________________________________________________________________________
  
</details>

<details>
  <summary> 1DFECA0C002AE40B8619ECF94819CC1B </summary>
  
  ____________________________________________________________________________________________________________________
  
  <p></p>
Hashes.com identifies this algorithm as "NTLM"
  <p></p>
  
![image](https://user-images.githubusercontent.com/66912443/186176288-fa2f2fe1-728a-43e3-8b6e-0800a08b8e5c.png)

In the hashcat hash type table, the code is revealed as "1000"
  
![image](https://user-images.githubusercontent.com/66912443/186176560-6876326f-e40c-487d-a67e-693876939bc7.png)
  
With all this knowledge we can put the command together as follows:
  
``` hashcat -m 1000 -a 0 1DFECA0C002AE40B8619ECF94819CC1B /usr/share/wordlists/rockyou.txt ```
  
![image](https://user-images.githubusercontent.com/66912443/186176905-c4b21681-cd55-4e9d-86ee-f882e2b74fe6.png)

____________________________________________________________________________________________________________________ 

</details>

<details>
<summary> $6$aReallyHardSalt$6WKUTqzq.UQQmrm0p/T7MPpMbGNnzXPMAXi4bJMl9be.cfi3/qxIf.hsGpS41BqMhSrHVXgMpdjS6xeKZAs02.</summary>

____________________________________________________________________________________________________________________

  <p></p>
By looking at the first 3 characters "$6$" and searching this up in the hash types table we can see this is a salted hash of type SHA-512. This allows us to get the flag code of 1800.
  <p></p>

![image](https://user-images.githubusercontent.com/66912443/186177634-1510ac78-3258-4535-b4ca-d178bf08f28d.png)

Below is the command you may use, personally I created a "hash.txt" file and put the hash within there as it was far too long for command line but worked fine once in that file. As this is a SHA-512 hash this will take some time to complete.  

``` hashcat -m 1800 -a 0 hash.txt /usr/share/wordlists/rockyou.txt ```

Answer = waka99

____________________________________________________________________________________________________________________

</details>


<details>
<summary> e5d8870e5bdd26602cab8dbe07a942c8669e56d6:tryhackme </summary>

____________________________________________________________________________________________________________________

<p></p>
Using hashes.com, we can identify this hash as another SHA1 hash. The difference here however is that this is a salted SHA1 so when it comes to using the table it will be slightly different.
<p></p>

![image](https://user-images.githubusercontent.com/66912443/186183213-c813c9fd-f177-4754-9ae3-ccf9b7339449.png)

As seen previously, in the hash type table SHA1 is hash mode "100". However, as this time it is salted we will be using code "160" instead (HMAC-SHA1).

HMAC stands for "Hash-Based Message Authentication" and it operated using a shared secret key which in this instance is "tryhackme" (used as the salt).

![image](https://user-images.githubusercontent.com/66912443/186183425-e3b4a21e-1554-45ba-8d58-a6ebcbc0d11d.png)

From this point onwards its pretty much as normal. Once again I have put the hash inside a text file instead to make sure it works properly with hashcat.

``` hashcat -m 160 -a 0 hash.txt /usr/share/wordlists/rockyou.txt ```

![image](https://user-images.githubusercontent.com/66912443/186182309-8d77349a-f326-4a17-86fa-192eee50f184.png)

____________________________________________________________________________________________________________________

</details>



