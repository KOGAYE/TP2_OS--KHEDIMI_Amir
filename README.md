# TP2_OS--KHEDIMI_Amir

#Partie II

## 1.Files and users

Repertoire personnel

````bash
koga@vbox:~$ cd /home/koga/
koga@vbox:~$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
````


Permission de ce repertoire

```` bash
koga@vbox:~$ ls -l
total 32
drwxr-xr-x 2 koga koga 4096 Feb  5 14:17 Desktop
drwxr-xr-x 2 koga koga 4096 Feb  5 14:17 Documents
drwxr-xr-x 2 koga koga 4096 Feb  5 14:17 Downloads
drwxr-xr-x 2 koga koga 4096 Feb  5 14:17 Music
drwxr-xr-x 2 koga koga 4096 Feb  5 14:17 Pictures
drwxr-xr-x 2 koga koga 4096 Feb  5 14:17 Public
drwxr-xr-x 2 koga koga 4096 Feb  5 14:17 Templates
drwxr-xr-x 2 koga koga 4096 Feb  5 14:17 Videos
````



Le chemin du fichier ssh

````bash
koga@vbox:~$ find / -name "sshd_config"
/etc/ssh/sshd_config
````



Utilisateur marmotte

````bash
root@vbox:/home/koga# /usr/sbin/useradd -m marmotte -s /bin/bash
koga@vbox:/$ cd /home/
koga@vbox:/home$ ls
marmotte  koga
root@vbox:/home# passwd marmotte
New password:
Retype new password:
passwd: password updated successfully
koga@vbox:~$ sudo mkdir /home/papier_alu
koga@vbox:/home$ sudo mv /home/marmotte /home/papier_alu/
koga@vbox:/home$ ls
koga  papier_alu
koga@vbox:/home$ cd papier_alu/
koga@vbox:/home/papier_alu$ ls
marmotte
````



Prouver que le user a été cree 

````bash
koga@vbox:/etc$ cat passwd | grep marmotte
marmotte:x:1001:1001::/home/marmotte:/bin/bash
````


hash psswd marmotte

````bash
koga@vbox:/etc$ sudo cat shadow | grep marmotte
marmotte:$y$j9T$y5PJWCMntZQPfllgvMoD3.$9JgK.zYKeuJIWeWGGN2X7oy1/D0yuAXtJZK9Y.Oko5A:20125:0:99999:7:::
````



connexion new user

````bash
koga@vbox:~$ su marmotte
Password:
marmotte@vbox:/home/koga$ exit
exit
koga@vbox:/home$
````


mechant permission denied

````bash
marmotte@vbox:~$ ls /home/koga/
ls: cannot open directory '/home/koga/': Permission denied
````


Lancer un processus sleep

````bash
koga@vbox:~$ sleep 1000
````


Dans un autre terminal

````bash
ps -fe | grep sleep
koga        2294    2217  0 13:12 pts/0    00:00:00 sleep 1000
koga        2329    2321  0 13:13 pts/1    00:00:00 grep sleep
````

Terminez le processus sleep depuis le deuxième terminal

````bash
koga@vbox:~$ kill 2294
koga@vbox:~$ sleep 1000
Terminated
````


Lancer un nouveau processus sleep, mais en tâche de fond

````bash
koga@vbox:~$ sleep 1000 &
[1] 2363
koga@vbox:~$ ps -fe | grep sleep
koga        2363    2217  0 13:17 pts/0    00:00:00 sleep 1000
koga        2398    2390  0 13:18 pts/1    00:00:00 grep sleep
````

Trouver le chemin du sleep

````bash
koga@vbox:~$ sudo find / -name "sleep"
[sudo] password for koga:
find: ‘/run/user/1000/gvfs’: Permission denied
find: ‘/run/user/114/gvfs’: Permission denied
/usr/lib/klibc/bin/sleep
/usr/bin/sleep
````

Trouver la commande .bashrc

````bash
koga@vbox:~$ sudo find / -name ".bashrc"
/etc/skel/.bashrc
find: ‘/run/user/1000/gvfs’: Permission denied
find: ‘/run/user/114/gvfs’: Permission denied
/root/.bashrc
/home/koga/.bashrc
/home/papier_alu/marmotte/.bashrc
````

Verification

````bash
koga@vbox:~$ which sleep ssh ping
/usr/bin/sleep
/usr/bin/ssh
/usr/bin/ping
````

Installer le paquet Firefox

````bash
koga@vbox:~$ sudo apt install firefox-esr -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
firefox-esr is already the newest version (128.4.0esr-1~deb12u1).
firefox-esr set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
````

lancer Firefox

````bash
koga@vbox:~$ Firefox
````


Determiner d'où viennent les paquets

````bash
koga@vbox:~$ cat /etc/apt/sources.list
#deb cdrom:[Debian GNU/Linux 12.7.0 _Bookworm_ - Official amd64 NETINST with firmware 20240831-10:38]/ bookworm contrib main non-free-firmware

deb http://deb.debian.org/debian/ bookworm main non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm main non-free-firmware

deb http://security.debian.org/debian-security bookworm-security main non-free-firmware
deb-src http://security.debian.org/debian-security bookworm-security main non-free-firmware

# bookworm-updates, to get updates before a point release is made;
# see https://www.debian.org/doc/manuals/debian-reference/ch02.en.html#_updates_and_backports
deb http://deb.debian.org/debian/ bookworm-updates main non-free-firmware
deb-src http://deb.debian.org/debian/ bookworm-updates main non-free-firmware

# This system was installed using small removable media
# (e.g. netinst, live or single CD). The matching "deb cdrom"
# entries were disabled at the end of the installation process.
# For information about how to configure apt package sources,
# see the sources.list(5) manual.
````

## Recup le fichier

````bash
koga@vbox:~/Downloads$ wget https://gitlab.com/it4lik/b1-os/-/raw/main/tp/2/meow
--2025-02-07 13:46:43--  https://gitlab.com/it4lik/b1-os/-/raw/main/tp/2/meow
Resolving gitlab.com (gitlab.com)... 172.65.251.78, 2606:4700:90:0:f22e:fbec:5bed:a9b9
Connecting to gitlab.com (gitlab.com)|172.65.251.78|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 18016947 (17M) [application/octet-stream]
Saving to: ‘meow’

meow                          100%[=================================================>]  17.18M  5.20MB/s    in 3.4s

2025-02-07 13:46:47 (5.01 MB/s) - ‘meow’ saved [18016947/18016947]
````
