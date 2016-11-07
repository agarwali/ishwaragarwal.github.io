---
author: agarwali
comments: true
date: 2016-02-08 04:24:45+00:00
layout: post
title: Setting up Development Environment for OpenMRS
meta:
category: foss
excerpt_separator: <!--more-->
media:
media_source:
tags:
- errors
- FOSS
- guide
- installation
- openMRS
- opensource
---

I know I should have shared this earlier, but here it is. In this post, I am going to share some of my insights and frustrations installing and building OpenMRS in details. <!--more-->

#### Overview


What I considered being a 2-hour job turned to be a 6-hour nightmare uninstalling and installing Java JDK on Linux OS. Not to mention, the problems in campus internet made life even worse.  If you are here to learn how to install OpenMRS, I would recommend that you first go ahead and read [Step by Step Installation for Developers](https://wiki.openmrs.org/display/docs/Step+by+Step+Installation+for+Developers). This is by far the most updated version I could find on installing instructions on OpenMRS. Here I will be writing the detailed process for OpenMRS installation.

Note: If you are an expert in Linux CLI, you may disregard the details like the commands I have written below. Feel free to skip to any section.


####




#### **1. Installing JDK**


If you plan to edit the source code, you will need JDK. Unfortunately, Ubuntu doesn't always install the latest JDK if you use apt-get. I recommend that you install Oracle JDK 8 (Open JDK8 should also work well). First check if you have JDK installed


    <code><span class="pln">javac -version</span></code>


If JDK is not installed try installing from CLI


    <code><span class="pln">sudo apt</span><span class="pun">-</span><span class="pln">get update
    sudo apt</span><span class="pun">-</span><span class="pln">get install oracle</span><span class="pun">-</span><span class="pln">java8</span><span class="pun">-</span><span class="pln">installer</span></code>


If JDK is already installed, I would suggest you remove old JDKs because I faced some maven-java compatibility issues later. If anything doesn't work try installing using the [PPA Repository](http://www.webupd8.org/2012/09/install-oracle-java-8-in-ubuntu-via-ppa.html).

If you do not want to remove old JDK and use JDK8 you can use the following command.


    <code>sudo update-java-alternatives -s java-8-oracle</code>


To be able to use maven later it is important to set Java environment path variable. Use the following command


    <code>sudo apt-get install oracle-java8-set-default</code>


or you can set Java environment path variable manually by editing your .bashrc and adding the following variable


    export JAVA_HOME=/path-to-java/java-8-oracle
    export PATH=$PATH:$JAVA_HOME/bin




#### **2. Installing MySQL**


MySQL server is very common among MySQL users. Don't forget your root password because you will need it later. If you are looking for a tutorial for installing MySQL, here is a very nicely written guide: [How to Install MySQL on Ubuntu 14.04](https://www.linode.com/docs/databases/mysql/how-to-install-mysql-on-ubuntu-14-04).


#### **3. Installing Eclipse Java EE**


Yes, we will be using IDE for our development. I'm not a big fan of IDE's but Eclipse isn't bad. I was surprised to find that you can connect your remote repository and work on a shared repo. It also allows you to run all git commands. The main advantage of using Eclipse is that you can install OpenMRS plugins to generate test cases, in case you were making a new module or testing your changes.

The best way to install eclipse is to download the tar file from [Eclipse](http://www.eclipse.org/downloads/) downloads. Following are some instructions

Unzip and extract downloaded file


    tar xvzf eclipse-jee-mars-1-linux-gtk-x86_64.tar.gz


Move Eclipse to correct location. I installed in /opt/ directory but you don't have to


    sudo mv eclipse /opt/


Create Gnome menu item


    sudo gedit /usr/share/applications/eclipse.desktop


With this contents


    ## Add following content to file and save ##
    [Desktop Entry]
    Encoding=UTF-8
    Name=Eclipse
    Comment=Eclipse SDK 3.6.1
    Exec=eclipse
    Icon=/opt/eclipse/icon.xpm
    Terminal=false
    Type=Application
    Categories=GNOME;Application;Development;
    StartupNotify=true




#### **4. Installing Maven**


We need to install Maven, which is a tool for building and managing any Java-based project.

Before installing maven, I recommend you check Java environment variable value







  1. echo $JAVA_HOME


  2. /Library/Java/JavaVirtualMachines/jdk1.8.0_45.jdk/Contents/Home





First, [download ](http://maven.apache.org/download.html)Maven and then to install maven:


    <span class="pln">tar xzvf apache</span><span class="pun">-</span><span class="pln">maven</span><span class="pun">-</span><span class="lit">3.3</span><span class="pun">.</span><span class="lit">9</span><span class="pun">-</span><span class="pln">bin</span><span class="pun">.</span><span class="pln">tar</span><span class="pun">.</span><span class="pln">gz
    </span>sudo mv <span class="pln">apache</span><span class="pun">-</span><span class="pln">maven</span><span class="pun">-</span><span class="lit">3.3</span><span class="pun">.</span><span class="lit">9 </span>/opt/


Now, add the bin directory of the created directory apache-maven-3.3.9 to the PATH environment variable in your .bashrc


    export MAVEN_HOME=/opt/apache-maven-3.3.9
    export PATH=$PATH:$MAVEN_HOME/bin


Confirm with mvn -v in a new shell. The result should look similar to Apache Maven 3.3.9 (bb52d8502b132ec0a5a3f4c09453c07478323dc5; 2015-11-10T11:41:47-05:00) Maven home: /opt/apache-maven-3.3.9 Java version: 1.8.0_72, vendor: Oracle Corporation Java home: /usr/lib/jvm/java-8-oracle/jre Default locale: en_US, platform encoding: UTF-8 OS name: "linux", version: "3.19.0-43-generic", arch: "amd64", family: "unix"

**5. Check out the core from git
**

Most importantly, you need to get the OpenMRS Platform code from GitHub: [https://github.com/openmrs/openmrs-core](https://github.com/openmrs/openmrs-core)

See [Using Git](https://wiki.openmrs.org/display/docs/Using+Git) for the overall docs.

**
6. Installing OpenMRS maven project**

After fetching the git repo you can compile OpenMRS project in two ways:

**Through Eclipse: ** You need to import OpenMRS as a Maven project in Eclipse IDE and install there. For more detailed instructions and screenshots, you can take a look at this [guide](https://wiki.openmrs.org/pages/viewpage.action?pageId=16318792).

**Through CLI:** move into the "_webapp_" directory and execute the following command.


    mvn clean instal




#### 7. Running OpenMRS


Start your MySQL server first. Following is the command


    <code>sudo /etc/init.d/mysql start</code>


Then in your webapp directory execute the following command (you can also do this from Eclipse but mak sure you see the error log for any errors).


    mvn jetty:run


Wait for the_ [ INFO ] Started Jetty Server message_ and open the web browser at [http://localhost:8080/openmrs](http://localhost:8080/openmrs). Follow the instructions.


#### **8. Configure OpenMRS project for the first time**


You should be able to follow the instructions on the screen. There are also detailed instructions in this [guide](https://wiki.openmrs.org/pages/viewpage.action?pageId=16318792).


Default Login Details for your Locally hosted OpenMRS







  * Username: admin


  * Password: either "Admin123" or "test"


It should look like this:

![Screenshot from 2016-02-07 23:21:36](https://iamishwar.files.wordpress.com/2016/02/screenshot-from-2016-02-07-232136.png)



If you face any problem installing feel free to leave a comment here or at https://talk.openmrs.org
