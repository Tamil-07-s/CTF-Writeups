<img width="916" height="794" alt="1_DJfPNs1QXQ1imO81iu8Ahg" src="https://github.com/user-attachments/assets/f055e6fe-a5ea-48b0-b81f-643ec04c0474" />

As always, by reading the description properly, it strengthen the point that the there is a conflict in type of file. So after downloading the file, tried the following,

exiftool
strings
binwalk
Nothing of the above gave a proper hint to further proceed. By the PDF file has some part of the flag at the second page of the file.

<img width="810" height="643" alt="1_q_Fn8XsajZJhKiqWPuyHGw" src="https://github.com/user-attachments/assets/c1022c96-5094-4546-a8c6-476ed4da4adf" />

To find the remaining part of the flag, i tried to check the file type of the PDF whether to check if the file is corrupted.

Press enter or click to view image in full size

<img width="974" height="49" alt="1_sqhFCcwgQ4OZKoN37P016A" src="https://github.com/user-attachments/assets/a1aa1a3b-6258-404e-8503-5ed8b40cef19" />

It gave the clue that it is a PNG file but the file is in the PDF format, so i tried to change the .pdf to .png extension.

command: mv flag2of2-final.pdf flag2of2-final.png

When i opend the png format, i got the remaining part of the flag.

Hurray🎉🎉🎉🎉…

<img width="492" height="257" alt="1_-sUBacRx22rHN7Gk2enYxg" src="https://github.com/user-attachments/assets/705f95d8-217a-44b5-977f-3102b5d15fcc" />

Knowledge learnt:

Check the file type of the given file, especially in the forensics category, also in whatever the file your dealing with during the analysis of the file in practical real life scenarios.

— Tamil Arasan S

