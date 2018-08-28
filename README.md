<img src="/identity/yls_cyber_center_lock_logo.png" width="220px" align="right" />

# Cybersecurity @ Yale Law School
https://cyber.yale.edu

## Overview
These are design plans for a Cybersecurity classroom at Yale Law School in 40 Ashmun (Baker Hall).  Scott J. Shapiro and Sean O'Brien are developing the curriculum for [Cybersecurity 20310](https://courses.law.yale.edu/courses/course/2161) in Fall 2018 and will be assisted by a Cyber Fellow.

Cybersecurity 20310 is an introduction to cybersecurity, privacy, anonymity, and cryptography via hands-on activities.  We will train students to understand cybersecurity and networking concepts, so that they may better engage issues at the policy and regulatory level.

## Design
Our design allows for the exploration of cybersecurity, pentesting, and cryptographic concepts within a safe learning environment.  It is a scaled-down version of a penetration testing lab, introducing students to simple exercises through a command line interface (CLI).  Wherever possible, we have used interchangeable parts, compatible Free and Open-Source Software (FOSS), and industry-standard configurations and protocols.

<img src="/diagrams/classroom_diagram01.png" width="100%" />

The diagram above and description below refer to the design of one airgapped Local Area Network (LAN).  This design can be duplicated as necessary to accommodate more students.  Cybersecurity 20310 requires that this design be repeated for four identical LANs, to accomodate 18-20 student devices (and a maximum of 32 devices for potential guests or work outside of the scope of the class).

### Student Devices
These are [Raspberry Pi](https://www.raspberrypi.org) mini-computers running the homegrown Quillux GNU/Linux operating system provided by [Yale Privacy Lab](https://privacylab.yale.edu).  Quillux is built from [Kali Linux](https://www.kali.org), an industry-standard security and forensics operating system based upon [Debian GNU/Linux](https://debian.org).

These devices are connected to the network via Ethernet cable and feature a small [OLED screen](https://learn.adafruit.com/adafruit-oled-displays-for-raspberry-pi/introduction) that displays  network (IP) address, physical (MAC) address, and bandwidth information.  Students will connect to these devices from a terminal emulator/CLI on their laptop and control them via the Secure Shell (SSH) protocol.

#### Hardware Details
* Raspberry Pi 3 Model B v1.2
* 32 GB SD card
* 0.96" I2C IIC serial 128x64 OLED display

### Networking Devices
Network traffic will be controlled by a [DD-WRT](https://dd-wrt.com) WiFi Router, which will be airgapped (not connected to the Internet or Yale campus network).  Student laptops will connect to the WiFi connection provided by the router (SSID "ylscyber") using WPA2 passphrase security.

An 8-port unmanaged ("dumb") switch will be connected to the router and share the network connection to student Raspberry Pi devices via Ethernet cables.

#### Hardware Details
* TP-Link Archer C7 AC1750 router
* TRENDnet TEG-S80G 8-port unmanaged switch

### Network Analysis Device
One Raspberry Pi will be connected to the network as a [PiRogue](https://www.youtube.com/watch?v=oIcrsuJcTPo), a device configured to intercept and analyze network traffic.  This is useful for demonstrations of Man-in-the-Middle (MITM) attacks as well as general analysis of network traffic and auditing of the privacy and security of applications (i.e. detecting "leaky" privacy settings in an app).  PiRogue is developed by [PiRanhaLysis](https://github.com/PiRanhaLysis/PiRogue) and connects to [PiPrecious](https://github.com/PiRanhaLysis/PiPrecious) for an experimental environment.

#### Hardware Details
* Raspberry Pi 3 Model B v1.2
* 32 GB SD card
* 0.96" I2C IIC serial 128x64 OLED display
* TP-Link TL-WN722N N150 150Mbps USB WiFi

## Prerequisite Configuration

### Student Laptops
Students will bring their own laptops to class and will connect to the network via WiFi (SSID "ylscyber") with WPA2 passphrase security.

#### Command Line Interface
Students will connect to their Raspberry Pi devices from a terminal emulator/CLI on their laptop and control them via the Secure Shell (SSH) protocol.  Students must follow the directions below.

* **Hyper:** Windows users must install [Hyper](https://hyper.is) as a terminal emulator.  macOS, GNU/Linux, and other Unix-like systems already include a terminal emulator.  However, installing Hyper on these systems is recommended unless you are already very familiar with the CLI of your choice.

* **SSH:** A Secure Shell (SSH) client is required to connect to each Raspberry Pi.  Windows and macOS users are encouraged to install the [FileZilla Client](https://filezilla-project.org), which will also provide [PuTTY](https://putty.org) for SSH connections.  GNU/Linux users may install the `filezilla` package, but will also need to install a package such as `openssh-server` to make SSH connections.

* **Config File:** After installing Hyper and FileZilla/PuTTY, a configuration script must be installed for SSH connections.  Windows users must [download this file](https://github.com/zeit/hyper/issues/1375) and save it as `C:\Program Files\hyper\hyper.js`.  Mac users must [download this file](https://github.com/zeit/hyper/issues/1375) and save it as `~\hyper.js`.

## Classes of Attack
Conceptual basis for examples used in the classroom.  Will vary as class develops.

* Regular File Access - access/modification of config/system files, DLLs, kernel image and UEFI boot
* Elevation of Privileges - gaining root access, Web CMS access, SMTP e-mail spoofing/spam
* Information Leakage - Network Analysis via Interception, Man-in-the-Middle (MITM), Spectre/Meltdown
* Denial of Service - Dedicated Denial of Service (DDoS) attacks and Low-Orbit Ion Cannon (LOIC)
* Special File / Database Access - SQL injection, poor input sanitation
* Remote arbitrary code execution - botnets, ransomware, ETERNALBLUE
* Misinformation - covering tracks through log modification, Phishing attempts, Cross-site scripting (XSS)

## Course Outline  

### 1: Getting to Know Your Pi

#### Discussion

* What is an operating system?
* What is a command line interface (CLI)?
* Users, Groups, Filesystem Permissions

#### Activities

* Install and configure CLI on your laptop.
* Connect to your Raspberry Pi via SSH.
* Basic networking commands, 'ifconfig' and 'iwconfig'
* Change hostname to character name from Marvel Comics, DC Comics, Game of Thrones, or Star Wars.

#### Concepts

* Principle of Least Privilege
* Sandboxing / Isolation
* Permissions as a Structural Design for Security
* Network (IP)address, physical (MAC) address

### 2: Normative Structure of the Network

#### Discussion

* What is a computer network?
* What are the rules "governing" the network?
* What protocols power the Internet?
* Network and Internet history

#### Activities

* Networking commands - `ping`, `traceroute`
* Find your default route / network gateway, DNS provider.
* Network protocols, sockets, and ports (TCP, UDP, HTTP, SMTP, FTP, SSH, SSL/TLS).
* Firewalls, `ufw`

#### Concepts

* Networks as regulatory mechanisms
* Network control and infrastructure
* Net Neutrality

### 3: Filesystems &amp; Permissions

#### Discussion
* What is a regular file? A special file?
* Representations of data - binary (hexidecimal, assembly) versus plaintext (ASCII, ISO 8859-1, UTF-8).
* Overview of the Unix filesystem tree.  Comparison between Unix/Unix-like systems (macOS, GNU/Linux) and Windows.
* Principal of Least Privilege.  Securing a multi-user system (sandboxing, `chroot` jails).

#### Activities
* Log into your Raspberry Pi via SSH.  Navigate the filesystem (`ls`, `cd`).  Copy, move, delete, and create directories (`cp`, `mv`, `rm`, `mkdir`).
* Create a file, edit, view, and search it (`touch`, `cat`, pipes, `nano`, `grep`).
* Change file and directory permissions (`chmod`) and ownership (`chown`).  Make a file unreadable by any user.
* Run a superuser command (`sudo`).  Activate the root account, set a root password, and log in as root (`passwd`).  Deactivate the root account.

#### Concepts
* 

### 4: Chain of Trust

#### Discussion
* Hash functions and hash tables (MD5, SHA256, SHA512).  Data verification using hashes.
* The concept of privacy through secrecy and "shared secrets" (passwords, PINs, keys).
* Basics of encryption.  Pubic/private key exchange (PGP/GPG, SSL/TLS, SSH).
* Man-In-The-Middle attacks (MITM). Certificate Authorities (CAs) and certificate pinning.
* Trusted software sources, package management, and reproducible builds.

#### Activities  
* Copy a text file and generate a hash/checksum (`sha256sum`) from it.  Check the value against the original file.  Now edit one character in that file.  Check the value again.
* Generate a PGP/GPG key pair.  Encrypt a file, then decrypt it.  Sign a file and verify its signature.

#### Concepts
* 

### 5: Anonymity &amp; Staying Hidden

#### Discussion
* Overview of the Tor network and the concept of onion routing.
* Use cases (censorship circumvention, free speech, whistleblowing, data exfiltration, surveillance mitigation).
* Hidden .onion services and the Deep (Dark) Web.  Contrast with the regular Web over Tor.
* Comparisons between anonymity networks (I2P, Freenet, mix networks).

#### Activities  
* Install [Tor Browser Bundle](https://www.torproject.org/projects/torbrowser.html.en).  Browse the Web and the Deep Web via [Onion Sites That Don't Suck](https://github.com/alecmuffett/onion-sites-that-dont-suck).
* Connect to a Yale Privacy Lab [FreedomBox](https://freedombox.org) via the [Plinth interface](https://wiki.debian.org/FreedomBox/Manual#FreedomBox.2FManual.2FTor.Anonymity_Network_.28Tor.29) and set up a Tor bridge/relay and hidden .onion service.
* Install [OnionShare](https://onionshare.org) and send a file to another student via the Tor network.

#### Concepts
* Attribution of attacks. In the context of international law?
* Threat Modeling.  Risks and rewards of using these technologies.

### 6: 

#### Discussion
* 

#### Activities  
* 

#### Concepts
* 

### 7: 

#### Discussion
* 

#### Activities  
* 

#### Concepts
* 


## Old Outline  
The examples below are snippets from previous iterations of this document.  

### Web Servers &amp; Web Apps

**Discussion:**
1. Walkthrough of a typical HTTP request/response.  Client and server architecture.
2. Differentiate between The Internet and The Web.  Social media "walled gardens" (Facebook, Twitter).
3. Description of very simple HTML and JavaScript.
4. Overview of the dominant LAMP stack (Linux, Apache, MySQL, PHP) and how a typical Web application ([WordPress](https://wordpress.org)) works. Contrast with other stacks (Win Server/IIS/MS SQL/ASP.NET, NoSQL).

**Activities:**
1. Set up a simple Python-based Web server using [only 16 lines](https://www.linuxjournal.com/content/tech-tip-really-simple-http-server-python).  Then start a Python or PHP server using only 1 line in the CLI.
2. [Set up MediaWiki](https://wiki.debian.org/FreedomBox/Manual#FreedomBox.2FManual.2FMediaWiki.Wiki_.28MediaWiki.29) via the FreedomBox and log in.
3. Set up your own LAMP stack on the Raspberry Pi (`tasksel`).  Write a 1 line "Hello World" file in PHP and view it in your Web browser.

**Hardware:**
* Raspberry Pi 3
* Student laptops
* [FreedomBox](https://freedombox.org)

**Software:**
* GNU/Linux command line interface (CLI)
* [Kali](https://www.kali.org)
* [WordPress](https://wordpress.org)
* [MediaWiki](https://wiki.debian.org/FreedomBox/Manual#FreedomBox.2FManual.2FMediaWiki.Wiki_.28MediaWiki.29)

**Homework:**
1. Figure out how to "harden" your Raspberry Pi's Apache, MySQL, and PHP configuration.  Make sure the Web server only responds to requests from `localhost`.
2. Write a simple HTML webpage that contains at least 20 HTML tag pairs and 1 image.  Be as creative as you like.


### Attacking a Web Application

**Discussion:**
1. Refresher about a typical Web application's design.  Description of a Web browser session.
2. Description of client-side scripting, with JavaScript as the example.  Examples of cross-site scripting attacks (XSS).
3. SQL and relational databases.  Basic SQL syntax.  Examples of SQL injection attacks.

**Activities:**
1. SSH into your Raspberry Pi and launch the Web browser.  Browse to bWAPP on the local network, and try a XSS attack to create a JavaScript popup alert.
2. Try a SQL injection attack on bWAPP to grab data from the MySQL database.
3. Trick bWAPP into letting you log in with an incorrect password.

**Hardware:**
* Raspberry Pi 3
* Student laptops
* Debian VM Host

**Software:**
* [VirtualBox](https://virtualbox.org)
* [Bee-Box/bWAPP](https://sourceforge.net/projects/bwapp/)

**Homework:**
1. Describe one way that XSS attacks can be mitigated against by the Web Developer or System Administrator, in detail.
2. Describe one way that SQL injection attacks can be mitigated against by the Web Developer or System Administrator, in detail.
3. Try [NoScript](https://noscript.net).  How does this protect the end-user from attack?  What are the pros/cons?


### Exploiting a Remote Server to Gain Root Access

**Discussion:**
1. Description of the [Metasploit Framework](https://docs.kali.org/general-use/starting-metasploit-framework-in-kali) and the vulnerable "[Metasploitable](https://github.com/rapid7/metasploitable3)" virtual machine.
2. Examples of real-world remote access exploits.  Botnets and command-and-control malware networks.
3. Reminder about SSH access, root privileges, and encryption keys.

**Activities:**
1. SSH into your Raspberry Pi and then SSH from that machine into the Metasploitable VM, using an insecure port.  Activate the root user, change the password, and generate new SSH keys.
2. Find your target data in a user's `/home/` directory.  Copy the example data and compress it into a tarball or zip.
3. Find at least two ways to exfiltrate the data to your Raspberry Pi's filesystem.  Try to cover up your tracks.

**Hardware:**
* Raspberry Pi 3
* Student laptops
* Debian VM Host

**Software:**
* GNU/Linux command line interface (CLI)
* [Kali](https://www.kali.org)
* [Metasploit](https://docs.kali.org/general-use/starting-metasploit-framework-in-kali)
* [VirtualBox](https://virtualbox.org)
* [Metasploitable](https://github.com/rapid7/metasploitable3)

**Homework:**
1. Describe your method for exfiltrating data, in detail.  Did you leave any traces on the victim's system?  If so, what might they be?
2. Read the example data you exfiltrated.  How private is this information?  How might it be correlated with other data?  How might an attacker use this data after they have it?


### Exploiting a User's Desktop PC

**Discussion:**
1. Examples of real-world phishing techniques and other ways to deliver payloads by tricking end-users.
2. Overview of operating system structure, including kernelspace and userspace.
3. Description of Java, Java Runtime Environments, and Java applets in Web browsers.
4. Windows history with Java and JRE vulnerabilities.

**Activities:**
1. SSH into your Raspberry Pi.  In Kali, run a Metasploit attack that delivers a Java applet payload to the user of a Windows VM.  What will happen when the user clicks on the applet and allows it to run?
2. After the applet runs, try to grab data about the end-user's behavior.  Can you capture keystrokes?  Record the screen?  Turn on the microphone?
3. Save the victim's data on your Raspberry Pi and create a README file, using the CLI, that describes the data.  Package the data and README in a tarball or zip, and copy it to your laptop.

**Hardware:**
* Raspberry Pi 3
* Student laptops
* Debian VM Host

**Software:**
* GNU/Linux command line interface (CLI)
* [Kali](https://www.kali.org)
* [Metasploit](https://docs.kali.org/general-use/starting-metasploit-framework-in-kali)
* [VirtualBox](https://virtualbox.org)
* Windows 10 virtual machine (VM)

**Homework:**
1. How can these types of attacks be stopped by System Administrators?  How would you train a room full of people, who aren't tech-savvy, to defend themselves from this type of attack?
2. Describe recent real-world malware attacks that utilize similar techniques and/or attack vectors.


### Denial-of-Service Attacks

**Discussion:**
1. Basic principle behind denial-of-service.  Relate back to request/response nature of the Web.
2. History of well-known Distributed Denial of Service (DDoS) attacks and tools like [Low Orbit Ion Cannon](https://en.wikipedia.org/wiki/Low_Orbit_Ion_Cannon) (LOIC).
3. Refresher about network topology. Briefly discuss centralization, decentralization, caching methods, and Content Delivery Networks (CDN).

**Activities:**
1. SSH into your Raspberry Pi.  In Kali, download and install Low Orbit Ion Cannon (LOIC).
2. Start a [LAMP Security](https://sourceforge.net/projects/lampsecurity/) VM on the Debian host machine.  From your Raspberry Pi, find the IP address of the VM and any open HTTP ports.  Attack the VM using LOIC.

**Hardware:**
* Raspberry Pi 3
* Student laptops
* Debian VM Host

**Software:**
* GNU/Linux command line interface (CLI)
* [Kali](https://www.kali.org)
* [Low Orbit Ion Cannon](https://en.wikipedia.org/wiki/Low_Orbit_Ion_Cannon)
* [VirtualBox](https://virtualbox.org)
* [LAMP Security](https://sourceforge.net/projects/lampsecurity/) virtual machine (VM)

**Homework:**
1. Describe the real-world risks and fallut of DDoS, for the attacker and victim.  How can such attacks propagate?
2. How can these types of attacks be mitigated against?  Contrast methods of securing Internet of Things (IoT) devices with enterprise Web servers and desktop PCs.