This can also be read on my Medium: https://medium.com/@tamilarasann7711/ultratech-tryhackme-walkthrough-a-live-walkthrough-be09226f4e94

<img width="967" height="195" alt="1_tmLW2rzxvqlB95OagiHQDg" src="https://github.com/user-attachments/assets/adaeaefe-02d6-40d7-95b8-7647a3b48b9f" />
Let’s gooo…
<img width="1100" height="146" alt="1_9DF4nETb8KvewZBGntdTTg" src="https://github.com/user-attachments/assets/8b672d5c-e5d3-492f-90ef-e1f7f955df7a" />
It’s gonna be a Pentesting Challenge, we are gonna perform our pentesting skills in the Ultratech company, all we have is the company’s name and their server’s IP address. It’s gonna be like the reader(YOU) and I are gonna solve this room together.

So first we can do the basic port scanning..,

While performing the usual nmap scan, it takes a longer time.,

<img width="1062" height="654" alt="1_AunSrIN1Ehu3d_Hjvit_OA" src="https://github.com/user-attachments/assets/4aed06a3-c279-4c52-81d2-06af6a3303ed" />

So i performed the nmap scan for only the 8081 port as per the question asked(Also ran the nmap scan for the entire port in the background)..,

nmap -sV -p8081 <target-ip>

<img width="940" height="350" alt="1_wMaBxvYBThy_h1o5rWyhHQ" src="https://github.com/user-attachments/assets/dad8c584-13d8-411b-af4e-3943313225e7" />

From here you can see the version that is running the port 8081.

So next we can find which linux distribution is running on the target site by the nmap scan with the flag of OS detection.

nmap -sV — osscan-guess <target-ip>

<img width="1100" height="450" alt="1_m1sKZi9mKTVNMztzt_ZYqg" src="https://github.com/user-attachments/assets/5c52ceac-13f9-45ac-a95c-ce1c5f118345" />

The nmap scan took a much time, so decided to shift to the modern day port scanning tool, the rustscan.

Installed the rustscan from the git and found the open ports in few seconds.

~wget https: //github.com/RustScan/RustScan/ releases/download/2.2.3/rustscan_2.2.3_amd64.deb
~sudo dpkg -i rustscan_2.2.3_amd64.deb

<img width="1100" height="733" alt="1_9vx7fesuGR3PGkLPhzxXCA" src="https://github.com/user-attachments/assets/e5becb97-1a40-4b9e-8f15-8e470199763f" />

To find the software that is used in the port 31331, we can make use of nmap again and find the software used.

nmap -sV -p31331 <target-ip>

<img width="907" height="182" alt="1_RWFiZ8d9srslU4pI-NPBiA" src="https://github.com/user-attachments/assets/1eb19b6c-84af-4c1f-a164-1e75f25b1c62" />

And finally to have to find the number of routes/endpoints of the target sites 8081 port have. To find that we can use the dirb tool. At first i thought that the routes mean a different one and tried the nmap scan with the — script-route, but then after understanding the question properly, understood that the routes and endpoints are the same. The 8081 port uses the REST api and the question asks the number of routes these are connected so that the web application can talk eachother.

Here the dirb will find all the endpoints, from that we can filter which are used by the web application by a common.txt. Anyway both these are just a guesses, in real life we have to dig more.

<img width="750" height="376" alt="1_-YKiJOVTUnu-5IH7uPEV8g" src="https://github.com/user-attachments/assets/80df20c0-9ee2-468c-b483-b52fb667c082" />

So finally the answers for the Enumeration part:
Which software is using the port 8081? → node.js

Which other non-standard port is used? →31331

Which software using this port? →apache

Which GNU/Linux distribution seems to be used? →Ubuntu

The software using the port 8081 is a REST api, how many of its routes are used by the web application? →2

_________________________________________________________________

For the futher proceedings we can use the dirb tool to do a directory search on the 8081 port. From the enumeration part we have done it already and let’s explore these endpoints for any exploits.

<img width="1100" height="589" alt="1_6Eb6Mzluup9vc6g3fC5kuA" src="https://github.com/user-attachments/assets/6ef3bad8-6822-4478-97fe-1ad4568785af" />

<img width="1100" height="589" alt="1_pMvGNDLIOwqk7z5FTxo32w" src="https://github.com/user-attachments/assets/39480720-a18b-48ef-ac0c-72ccb585565a" />

But nothing can be found and got strucked….

Then again searched started from the enumeration part and thought of another port that was open(31331) and performed the directory search over there..,

<img width="1100" height="374" alt="1_deYCXM4wGA0S2qcrVWBnzA" src="https://github.com/user-attachments/assets/fced7d87-6f4a-43d0-9e3e-c29aab19f328" />

From here i found the robots.txt as the interesting part(a traditional way of CTF’s) and found the directory info’s…,

<img width="554" height="209" alt="1_HXqZ6GFkB1HVPMra6_9kfw" src="https://github.com/user-attachments/assets/44fa3291-89cc-42f8-9ab7-57924f5c9920" />

<img width="1100" height="461" alt="1_O-4pPrb2x-WdKYNYevlWIA" src="https://github.com/user-attachments/assets/2882f3a4-7989-47ed-89f0-d0ed45e1e54b" />

A important clue from this robots.txt .., while exploring the inspect tab of the partners.html, it seems like the credentials that is entered is redirected to the 8081 port.

<img width="1100" height="589" alt="1_w_yO-GFYIQ3m6KMf_4Oo1A" src="https://github.com/user-attachments/assets/e0635951-1e74-482d-b46f-bf7843780580" />

Then i tried the SQLi attack at the redirected port of 8081, but resulted in failure after a lots of try.

<img width="1100" height="507" alt="1_ihah5Hn3DnHSC-lDb9W0gg" src="https://github.com/user-attachments/assets/0b6e0aaf-1c51-4a96-bf25-cc5bfdd8ba2c" />

Then decided to work with another endpoint that was found at 8081 port, that is /ping. That directory name was a bit intriguing and tried for code injection over there and it worked🎉

The page name is /ping.
In networking, a “ping” is a tool used to check if a computer is online by sending a signal to an IP address.
To make a ping tool work, the server must ask you for an IP address. Because you didn’t give it one (your URL ends exactly at /ping), the variable for the IP address was empty (undefined).


<img width="1100" height="102" alt="1_I7GzfSFSzSHEdVmeAUiyeQ" src="https://github.com/user-attachments/assets/61fdb470-d011-439e-b3ab-f1ac833bf56d" />

So next i used my ip in the code injection and got the database name and the hash file.

Backticks(`) are used not the (‘)

ip=`ls`

<img width="884" height="492" alt="1_ynfvtE2TEYK9C68gVcBO6w" src="https://github.com/user-attachments/assets/4db64133-48e8-4e8e-9951-38ae2d639d78" />

ip=`cat utech.db.sqlite`

Press enter or click to view image in full size

user names are r00t and admin, and also the password hashes are given. We can use the hashstation to crack them.

<img width="1100" height="361" alt="1_eJfeOeASytB0sFLeHFaqyA" src="https://github.com/user-attachments/assets/62f77d9e-501e-44f0-9923-d8f63ab9ff4b" />

So finally we got access to the system..,

We can login using the SSH server using the credentials we got from the code injection in 8081 port of the /ping directory.

<img width="1100" height="483" alt="1_xir7CBy8QzRwreE0qJqS5w" src="https://github.com/user-attachments/assets/928eeb3b-a6e9-45b6-b83f-9ff1647edc14" />

We can see that we don’t have the sudo access to gain privelege we can first try sudo -l..,

sudo -l

But we can’t find any clue, so let’s dive deeper.

<img width="539" height="53" alt="1_dYtvMawGQZzuq_qOmK8yQA" src="https://github.com/user-attachments/assets/fdd419cc-592e-437a-80a6-1466a15817a0" />

We can search for any files that has the SUID bit set. If a files SUID bit is set then we can perform privelege users action from the normal users login.

find / -perm -4000 2>/dev/null

<img width="838" height="757" alt="1_s5uXN7hw58jfR78pATyQeA" src="https://github.com/user-attachments/assets/dcae6a74-0d7f-4bcc-8664-a934cd5449db" />

Out of these the /usr/share/pkexec has a vulnerability and it can be exploited.

But we can make it even more simpler, when i first executed the id command i found docker one..,

<img width="546" height="33" alt="1_gIkfik6fvzk5klLTaKU7Kw" src="https://github.com/user-attachments/assets/1173b151-26a4-476c-9d03-f870f2393d86" />

Belonging to the docker group on Linux is a massive privilege escalation vector.

So by searching the docker in the GTFObins we can find the exploit.

<img width="1100" height="445" alt="1_CCOpRnR4l19Hab06f_WjhQ" src="https://github.com/user-attachments/assets/20532492-4cf6-4f4b-af12-de67996edaf9" />

When we run that command we got an error..,

<img width="1100" height="74" alt="1_TkwzrEV23p4WTp2BraPWgw" src="https://github.com/user-attachments/assets/a3b62918-7536-4055-afcf-1d903ee0434b" />

It says that the alpine is not found, so by searchin for docker images we can find the docker image and then we can replace it with the alpine.

<img width="551" height="56" alt="1_-BP6hl1LQVzUKS7Wy1bkLw" src="https://github.com/user-attachments/assets/d4132ef3-3234-404d-b334-b4349a3c138f" />

We found the image named bash so the command will be ..,

docker run -v /:/mnt — rm -it bash chroot /mnt /bin/sh

And there we go we got the root access 🎉🎉🎉🎉🎉

<img width="1100" height="480" alt="1_daOoQw4h6_79l6dPxNxorQ" src="https://github.com/user-attachments/assets/bc0a7966-6cdc-4e59-8292-1bfb9ab0297f" />
