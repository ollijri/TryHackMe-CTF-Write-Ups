![image](https://user-images.githubusercontent.com/66912443/186411817-9886bc1c-184d-4ad7-9dc4-f432223bfa06.png)


____________________________________________________________________________________________________________________

## Uncover and scan the QR code to retrieve the flag!

<details>
<summary> METHOD 1 </summary>
  <p></p>
On starting the machine, we are sent to '/home/ubuntu/confidential/' presenting us with the PDF we need to extract the QR code from.
  <p></p>

![image](https://user-images.githubusercontent.com/66912443/186401405-b90598ea-9e6f-4d56-965c-1865d8b6f6d7.png)

As we know the QR code is hidden within the pdf, it only makes sense to find a tool that makes this possible. Unfortunately for this box access is denied on installing any tools to help so we must move the file out from this VM into another, or your own device to make the use of tools possible.

The first step would be to create a netcat session that will listen and transmit the file:

``` nc -lvnp 2000 < Repdf.pdf ```

![image](https://user-images.githubusercontent.com/66912443/186407875-551c6578-3dc6-4403-bce6-174f63e070e6.png)

On the attacker machine, we then setup another netcat session to accept the file. As seen below the file has been accepted and now sits in the current working directory on the attack machine.

``` nc [source ip] 2000 > examine.pdf ```

![image](https://user-images.githubusercontent.com/66912443/186408034-6b45036a-256c-4826-ae39-d9091caa1db9.png)

Next is to extract the images. For this example I will be using 'pdfimages' with the following command:

``` pdfimages examine.pdf image ```

This will rip the images from the PDF and name them starting with 'image'. As you can see in the picture below this has outputted 3 files. Two of these files are the warning sign seen in the earlier PDF. However, the third image shows off just the message without the covering!

![image](https://user-images.githubusercontent.com/66912443/186410070-cb88df30-5f9a-4f2a-90c1-463743b9fb7c.png)


From this point on you can scan the file using any QR code scanner and find the flag! If you scan with phone its best to copy it and send it to youself as its a long complicated string of characters.

____________________________________________________________________________________________________________________  

</details>

<details>
<summary> METHOD 2 </summary>
  <p></p>
By right clicking the image and chosing 'Save Image As' you can skip all the fuss as this saves the file without the red warning label.

![image](https://user-images.githubusercontent.com/66912443/186406652-36e85cea-fccc-4c2d-92f8-a5e4694eb498.png)

From this point on you can scan the file using any QR code scanner and find the flag! If you scan with phone its best to copy it and send it to youself as its a long complicated string of characters.

____________________________________________________________________________________________________________________

</details>







