Description

How about some hide and seek?

<img width="1100" height="533" alt="1_tfXePQFiHZkAHIC6FXf3dw" src="https://github.com/user-attachments/assets/160bbd8f-a172-455b-bc71-cdbe7a12e14a" />

It is a simple challenge, here will understand it in a more beginner-friendly level.

The description mentions that the something is hidden in the jpg file that was given and we have to find the flag from the given jpg.

This kind of questions mostly have the flags hidden in these ways,

Check the exiftool command
binwalk command
steghide extract command
Analyse the image by checking the corners
Check the file format, whether the extension and the the file is correctly matched. If the file is in the JPEG, and the checking the memory if it was not as per the JPEG format then change the value in the memory.
These are the most common ways where the flags will be hidden.

<img width="1100" height="468" alt="1__KAc3TvHwwF2TzPs5ZqwPQ" src="https://github.com/user-attachments/assets/84f4ea58-b6c2-45c5-9d38-f3742a049d8c" />

While analysing the attributing URL, it was visible that it was mostly encoded in the BASE64(Since at last there is two =’s)

<img width="1100" height="533" alt="1_Fxv9dVBUlZTUbRt4a3lYGQ" src="https://github.com/user-attachments/assets/e221b7ed-20fc-4e2b-a324-db30c86f9b15" />

By decoding the BASE64, we got the flag🎉🎉🎉
