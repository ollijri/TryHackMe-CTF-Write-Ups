How many services are running under port 1000?

![image](https://github.com/ollijri/TryHackMe-Write-Ups/assets/66912443/4289d311-19ab-4dce-a63a-b0a77b3e60e3)

initially it shows 2 services and an EtherNet adapter, so while there may be 3 services running (ssh included) as one is currently showing as just an adapter the answer is 2

What is running on the higher port?

If we take the port of the adapter and run an abrasive scan on it using nmap, it is revealed to be ssh

![image](https://github.com/ollijri/TryHackMe-Write-Ups/assets/66912443/06bf66c5-ef5c-4b0a-ba57-7a434fb71470)


What's the CVE you're using against the application? 

One of the services running is http, so browings to the IP in the browser brings an apache web page

![image](https://github.com/ollijri/TryHackMe-Write-Ups/assets/66912443/5e241e1c-c56f-48dd-9c55-aafd7522d357)

using dirbuster or gobuster, we can scan the website for hidden/more directories. As can be seen below, the two "/simple" and "/server-status" were discovered.

![image](https://github.com/ollijri/TryHackMe-Write-Ups/assets/66912443/e9ee64e2-ebee-4d08-ae57-dbd1d05cc2b4)

Browsing to "/simple" (chosen as it matches the CTF name), we are presented with the following hidden site. This is a document site for a content management system "CMS made simple". At the bottom of the site, it specifies the version of "CMS Made Simple" is v2.2.8

![image](https://github.com/ollijri/TryHackMe-Write-Ups/assets/66912443/199b9f92-72d5-4d9c-b8d4-de84f1fe5323)

A quick google of an exploit for CMSMS v2.8.8 brings up a page on exploit-db exposing that this version is vulnerable to CVE-2019-9053

![image](https://github.com/ollijri/TryHackMe-Write-Ups/assets/66912443/5e1ea745-3d4d-4871-813b-aaea70783d73)


To what kind of vulnerability is the application vulnerable?

CVE-2019-9053 is an SQL Injection exploit (SQLi)

What's the password?



Where can you login with the details obtained?
