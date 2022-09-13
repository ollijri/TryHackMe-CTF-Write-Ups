## Processes 

Opening the file "Logfile.PML" using procmon allows us to answer the following quesions.

### What is the process ID of "notepad.exe"?
 
There are so many processes in this file its advantageous to use the filter tool to filter for the specific process name. 

![image](https://user-images.githubusercontent.com/66912443/189844292-ef950a32-92a8-48ea-becf-00f817315f75.png)

Once you confirm the search you will get your answer as seen below:

![image](https://user-images.githubusercontent.com/66912443/189844640-74331a78-ed40-446c-b7bd-2a5dfceb049b.png)

``` Answer = 5984 ```

### What is the parent process ID of the previous process?

Viewing the event properties of the process (right click and select) and going to the process tab reveals the parent PID:

![image](https://user-images.githubusercontent.com/66912443/189845421-d187963a-27e8-4732-9e3e-9a284a6e6bfb.png)

``` Answer = 3412 ```

### What is the integrity level of the process

From the same window as the previous task, we can see the integrity level is "High".

## Threads 

### What is the thread ID of the first thread created by notepad.exe?

Still filtered, scroll right to the top of the list. The detail of the second notepad process reveals the answer.

![image](https://user-images.githubusercontent.com/66912443/189846490-319867d1-d03e-4b5e-be80-23c107d8fbbe.png)

``` Answer = 5908 ```

### What is the stack argument of the previous thread? 

Viewing the event properties of the process (right click and select) and going to the event tab reveals the 'Thread', this is the stack argument.

![image](https://user-images.githubusercontent.com/66912443/189847015-8839b066-1911-4e1f-ac21-4df6607f1a9f.png)

``` Answer = 6584 ```
