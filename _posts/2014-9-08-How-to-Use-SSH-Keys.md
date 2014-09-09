---

layout: post
title: How To Use SSH Keys
excerpt: A short writeup on how to use SSH keys for authentication

---

##  {{page.title}}
### Short summary of SSH keys
The ssh authentication method works like the digital analogy of the [real-world lock and key system](http://www.gregmiller.net/locks/mitguide/chapter2.html). 

The bronze key I use to unlock my front door at home uniquely matches the interior of that lock with a series of peaks and valleys etched on the top of the key. If I lose my key and I don't have any backups, I have to replace the lock because there is no way to reverse-engineer the key from the lock. 

The ssh system works in a similar way by generating a pair of files related through a that are analogous to a key and lock. The first file is private, only to be used when trying to "unlock the door." The second file is public and is basically a digital "lock," which you can distribute to as many "doors" as you want. 

To authenticate with a server, you first install your public key with it. Then, each time you care to authenticate, you securely send your private key to the server and it uses an algorithm to confirm that it matches with your public key. Since the relationship is unique, there isn't a way that someone else could guess your private key, and impersonate you. 

### How to Use SSH Keys

**Make an SSH directory**

If you've never used ssh before, create a `.ssh` folder in your home directory. This location isn't required, but it's accepted practice. 

	$ mkdir ~/.ssh

**Generate SSH Keys**

Use the following command to go to your .ssh directory generate an SSH key pair using the [RSA algorithm](http://en.wikipedia.org/wiki/RSA_%28cryptosystem%29). 

	$ cd ~/.ssh 
	$ ssh-keygen -t rsa 
You will need to name the file and give a passcode for the keys. 
	
	Enter file in which to save the key (/Users/DesmondPC/.ssh/id_rsa): <Your Key Name>
	Enter passphrase (empty for no passphrase):
	Enter same passphrase again:
	Your identification has been saved in blah.
	Your public key has been saved in blah.pub.
	The key fingerprint is:	
	1b:69:20:15:a9:2b:46:9d:65:30:38:23:10:ca:df:d6
	The key's randomart image is:
	+--[ RSA 2048]----+
	|+. .o.oo         |
	|+ +  o+          |
	|.o +.=.          |
	|  o =... .       |
	| . . + ES        |
	|  o o  . o       |
	| . .    .        |
	|                 |
	|                 |
	+-----------------+	
	
Now, you should have two files in `~/.ssh`, one with a file extension of .pub (your public key) and the other without (your private key). 

**Using your SSH keys for Authentication**

Use the following command to tell ssh to use your new ssh key. 

	$ ssh-add ~/.ssh/<YourKey>

**Using SSH with Github**	

To use your newly generated ssh key with a service like Github, all you need to do is copy and paste your public key into the appropriate place. 

![Github Add Key](/img/ssh_1.png)

![Github Add Key](/img/ssh_2.png)

**Common Problems**

To check to see if ssh is using a key
	
	$ ssh-add -l
	
If it's working, you should see something like: 

	2048 aa:01:aa:01:aa:01:aa:01:aa:01:aa:01:aa:01 /Users/myPC/.ssh/id_rsa (RSA)
	
One common issue that people run into while trying to authenticate using SSH keys is the following error: 

	$ ssh-add -l
	> This agent has no identities
	
This means you didn't tell ssh to use your key. Solve it with `$ ssh-add ~/path/to/key`

Another problem gives the following:
	
	$ ssh-add ~/.ssh/<YourKey>
	> Could not open a connection to your authentication agent
	
This means that you need to turn on your ssh agent. Run the following: 

	$ eval $(ssh-agent)
	$ ssh-add ~/.ssh/<YourKey>


**Did I get something wrong?  [Let me know if I did](mailto:desmondrduggan@gmail.com)!**