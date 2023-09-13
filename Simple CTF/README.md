How many services are running under port 1000?

![image](https://github.com/ollijri/TryHackMe-Write-Ups/assets/66912443/4289d311-19ab-4dce-a63a-b0a77b3e60e3)

initially it shows 2 services and an EtherNet adapter, so while there may be 3 services running (ssh included) as one is currently showing as just an adapter the answer is 2

What is running on the higher port?

If we take the port of the adapter and run an abrasive scan on it using nmap, it is revealed to be ssh

![image](https://github.com/ollijri/TryHackMe-Write-Ups/assets/66912443/06bf66c5-ef5c-4b0a-ba57-7a434fb71470)


What's the CVE you're using against the application? 

One of the services running is http, so browings to the IP in the browser brings an apache web page

![image](https://github.com/ollijri/TryHackMe-Write-Ups/assets/66912443/5e241e1c-c56f-48dd-9c55-aafd7522d357)




To what kind of vulnerability is the application vulnerable?



What's the password?



Where can you login with the details obtained?
