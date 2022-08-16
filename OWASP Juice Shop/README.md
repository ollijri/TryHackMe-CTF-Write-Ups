## Open for business!

<details> 
  <summary> Gaining Access</summary>
  
  Use either openVPN or the hackbox, start the virtual machine and then enter the IP address into the URL bar at the top of your browser
  
  ![image](https://user-images.githubusercontent.com/66912443/184948233-78f2a0d2-ce02-4d9d-ac17-61d77c622098.png)
</details>

## Let's go on an adventure!

<details> 
  <summary> Question #1: What's the Administrator's email address? </summary>
  
  An administrator has left a review on a product logged in as the admin which exposes what the address is
  
  ![image](https://user-images.githubusercontent.com/66912443/184948637-48d4e7eb-fdf7-4f5a-bbdf-753cf4a78ec0.png)
  
  Answer = admin@juice-sh.op 
</details>

<details> 
  <summary> Question #2: What parameter is used for searching? </summary>
  
  by using the search function (magnifying glass) we can easily expose this parameter
  
  ![image](https://user-images.githubusercontent.com/66912443/184950365-ea52ef96-0cdf-402b-a876-f412842e855a.png)

  ![image](https://user-images.githubusercontent.com/66912443/184949876-ae8f27fd-52f9-4ef1-8305-0f620701e5c0.png)
  
  Once anything has been searched, from the URL bar we can see the effect of the search, exposing the parameter "q" that is used before the input
  
  ![image](https://user-images.githubusercontent.com/66912443/184950178-7598108e-ec73-4ddb-ab66-6164f2da31aa.png)

  Answer = q
</details>

<details> 
  <summary> Question #3: What show does Jim reference in his review? </summary>
   
   By looking around the products you can find "jim@juice-sh.op" left a review on the green smoothie.
   
   ![image](https://user-images.githubusercontent.com/66912443/184951521-d0689dd5-a76c-4f9f-a3b8-4d3fc3ffd71f.png)
   
   A simple google search of "replicator" reveals the answer
   
   ![image](https://user-images.githubusercontent.com/66912443/184951832-f732b23c-b908-41c8-8651-5e8a57b448b5.png)
   
   Answer = star trek
   
</details>

## Inject the juice

<details> 
  <summary> Question #1: Log into the administrator account! </summary>
  
  at this point make sure that intercept is on in burpsuite and if using foxyproxy that the option is set to "Burp"
  
  ![image](https://user-images.githubusercontent.com/66912443/184953030-12b1dcc6-10bd-4aeb-bff9-af4fd9e320c4.png)
  ![image](https://user-images.githubusercontent.com/66912443/184953343-2a97460f-6b6e-47a5-8b86-462183be51b8.png)
  
  Now that Burpsuite is up, navigate to "account" (next to the search bar) and enter in anything into the email and password field 
  
  ![image](https://user-images.githubusercontent.com/66912443/184953840-c30265c7-86ee-4cf1-8002-c40a4e967a5e.png)
  
  It may take a couple of goes of forwarding but back in burpsuite you should see that the email and password is sent off in plaintext to the SQL server which makes it easily susceptible to change.
  
  ![image](https://user-images.githubusercontent.com/66912443/184955212-90e6ac93-072d-4099-9eb1-7aacb6eb2a4e.png)
  
  To exploit this, we change the email parameter to "' or 1=1--".
  
  ![image](https://user-images.githubusercontent.com/66912443/184957695-c2a55d78-5f07-4f71-8f3e-7e2bd745f77d.png)

  The first character, the apostrophe, closes the brackets in the initial SQL query that is sent to the server. This is then followed by a second command in the same syntax: "OR" which using logic gates as an example will output true if either side of its input is true which "1=1" will always be, therefore tricking the system into always making the email valid. Finally, the double dashes at the end indicate the start of the comment meaning everything after this initial code will be ignored or "commented out". 
  
  As no email was given, SQL has defaulted to the top user id "0". In a lot of databases, the first user to be created is usually the administrator, as is the case in this challenge as well thus granting us admin access.
  
  ![image](https://user-images.githubusercontent.com/66912443/184960236-c5f5c13b-4728-465c-9565-20bf15417c98.png)
  
  Ans = 32a5e0f21372bcc1000a6088b93b458e41f0e02a
  
</details>


<details> 
  <summary> Question #2: Log into the Bender account! </summary>
   
  Following the exact same method used to get into the admin account, supplement "' or 1=1--" in the email field with "bender@juice-sh.op'--" instead.
  
  You may have noticed that the apostrophe and double dashes have moved next to each other. As this is an actual email, everything after it is commented out instead as calling back to the previous question, the apostrophe marks the closing of brackets to an SQL query.
  
  ![image](https://user-images.githubusercontent.com/66912443/184964819-9958b99b-ccbd-4ba1-8546-c871cdc1c9cf.png)

  
  Answer = fb364762a3c102b2db932069c0e6b78e738d4066
  
  
  
</details>
