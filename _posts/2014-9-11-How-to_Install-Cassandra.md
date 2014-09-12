---

layout: post
title: Cassandra and Ubuntu
excerpt: A simple tutorial on getting Cassandra up and running on an Ubuntu build.

---

#  {{page.title}}
According to its original publication, Cassandra is [ "A Decentralized Structured Storage System](https://www.cs.cornell.edu/projects/ladis2009/papers/lakshman-ladis2009.pdf)." Let's break that down. 

Cassandra is a **Structured Storage System**:

Similar to a database like MySQL or Postgres, the Cassandra system stores data that looks a certain way. This means that data values like a 'Bill' or a '94107' are referenced within the data model by their keys, 'first_name' and 'zip_code,' respectively. Furthermore, the Cassandra system has a specific way in which the data model has to be organized. 

That is **Decentralized**:

Decentralized means that the data can be split up among an arbitrary number of servers, typically referred to as "Commodity Servers," since they are viewed as commodities that, for a price, can be easily obtained and added to the network. 

Each server in the system is then declared responsible for a certain portion of the data, determined by a hashing algorithm. 

### Installing Java

To get Cassandra up and running, we need to first install Java 7 or above, as specified by the Cassandra 2.0 documentation. Now, for those of you who are like me and can't keep the Java acronyms together. We specifically want the **Java Platform, Standard Edition (Java SE 7)** or above. 

You can grab the most recent version of Java at [http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html). 

On this page, you will find three version of Java SE: 

1. JDK: used by developers to debug and build Java applications. 
2. **Server JRE**: for deploying Java applications on a server. *(Sounds Familiar)*
3. JRE: runs barebones Java on your system. 

Download the **Server JRE** .tar.gz file. 

*At the time that I'm writing this, the most up to date version for Java is 1.8.0_20, and that's what I'll be using here. You may have to substitute this version where appropriate for you.*

Upload the tarball to your home directory on the server. 

	$ scp server-jre-8u20-linux-x64.tar.gz <user>@your.server.ip.address:~
	
#### Server Installation

Here, you will need sudo privileges:  

	$ sudo su
	
Extract Java to the optional packages directory: 

	$ mkdir /opt/jdk
	$ tar -zxf server-jre-8u20-linux-x64.tar.gz -C /opt/jdk/
	
	# Sanity check
	$ ls /opt/jdk/
	
Let your server know that a new Java installation exists and give each item a priority (of 100 in this case). 

	$ update-alternatives --install /usr/bin/java java /opt/jdk/jdk1.8.0_20/bin/java 100
	$ update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk1.8.0_20/bin/javac 100

Finally, choose the default version of Java to use. This is especially important if you have any previous installations of Java. 

	$ update-alternatives --config java
	
In the case that you *do* have more than one installation, this prompt will show you something like
	
	$ update-alternatives --config java
	There are 3 choices for the alternative java (providing /usr/bin/java).
	
	  Selection    Path                                            Priority   Status
	* 0            /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java   1061      auto mode
	  1            /opt/jdk/jdk1.8.0_20/bin/java                    110       manual mode
	  2            /usr/lib/jvm/java-6-openjdk-amd64/jre/bin/java   1061      manual mode
	  3            /usr/lib/jvm/java-7-openjdk-amd64/jre/bin/java   1051      manual mode
	
	Press enter to keep the current choice[*], or type selection number: 1	
Confirm that everything worked. 

	$ update-alternatives --display java
	...
	$ update-alternatives --display javac
	...

	$ java -version
	java version "1.8.0_20"
	Java(TM) SE Runtime Environment (build 1.8.0_20-b26)
	Java HotSpot(TM) 64-Bit Server VM (build 25.20-b23, mixed mode)


### Installing Cassandra

First, download the Cassandra tarball at [http://cassandra.apache.org/download/](http://cassandra.apache.org/download/), and upload this to your server: 

	$ scp apache-cassandra-2.0.10-bin.tar.gz <user>@your.server.ip.address:~

Or, use wget: 

	$ wget http://apache.mirrors.pair.com/cassandra/2.0.10/apache-cassandra-2.0.10-bin.tar.gz

Then, extract the tarball to a Cassandra folder: 

	$ tar -xvzf apache-cassandra-2.0.10-bin.tar.gz
	$ mv apache-cassandra-2.0.10 ~/cassandra
	
#### Setup
To get Cassandra up and running, we have to do a little setup. 

First, [Cassandra documentation](https://wiki.apache.org/cassandra/GettingStarted) dictates that Cassandra maintains its logs and other data in the following directories: 

	$ sudo mkdir /var/lib/cassandra
	$ sudo mkdir /var/log/cassandra
	$ sudo chown -R $USER:$GROUP /var/lib/cassandra
	$ sudo chown -R $USER:$GROUP /var/log/cassandra

Finally, edit your bash profile to include Cassandra on your $PATH. 
	
	$ vi ~/.bash_profile
	
and add

	# Cassandra path
	CASSANDRA_HOME=~/cassandra
	PATH=$PATH:$CASSANDRA_HOME/bin	
	
Reload your bash profile: 

	$ source ~/.bash_profile

### Running Cassandra

Start the Cassandra process with 
	
	$ cassandra

End the Cassandra process with

	$ pkill -f CassandraDaemon
	
Access the Cassandra shell with 
	
	$ cqlsh
	Connected to Test Cluster at localhost:9160.
	[cqlsh 4.1.1 | Cassandra 2.0.10 | CQL spec 3.1.1 | Thrift protocol 19.39.0]
	Use HELP for help.	

Now, go store some data!

**Did I get something wrong?  [Let me know if I did](mailto:desmondrduggan@gmail.com)!**


Resources:

- [https://wiki.apache.org/cassandra/GettingStarted](https://wiki.apache.org/cassandra/GettingStarted)
- [http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
- [Getting Started with Cassandra](https://wiki.apache.org/cassandra/GettingStarted) 

    