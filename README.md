<img src="/img/yls_cyber_center_lock_logo.png" width="220px" align="right" />

# Cybersecurity @ Yale Law School
LAW 20310, Fall 2018

## Overview
These are design plans for a Cybersecurity classroom at Yale Law School in 40 Ashmun (Baker Hall).  Scott J. Shapiro and Sean O'Brien are developing the curriculum for [Cybersecurity (LAW 20310)](https://courses.law.yale.edu/courses/course/2161) in Fall 2018 and will be assisted by Cyber Fellow Laurin Weissinger.

This class is an introduction to cybersecurity, privacy, anonymity, and cryptography via hands-on activities. Students will learn cybersecurity and networking concepts so that they may better engage issues at the policy and regulatory level.

## Design
Our design allows for the exploration of cybersecurity, pentesting, and cryptographic concepts within a safe learning environment.  It is a scaled-down version of a penetration testing lab, introducing students to simple exercises through a command line interface (CLI).  We use interchangeable parts, Open Hardware, Free and Open-Source Software (FOSS), and industry-standard configurations and protocols.

<img src="/img/classroom_diagram_simplified.png" width="100%" />

The diagram above and description below refer to the design of one airgapped Local Area Network (LAN).  This design can be duplicated as necessary to accommodate more students.  Cybersecurity 20310 requires that this design be repeated for four identical LANs, to accomodate 18-20 student devices (and a maximum of 32 devices for potential guests or work outside of the scope of the class).

### Student Devices
These are [Raspberry Pi](https://www.raspberrypi.org) mini-computers running the homegrown Quillux GNU/Linux operating system provided by [Yale Privacy Lab](https://privacylab.yale.edu).  Quillux is built from [Kali GNU/Linux](https://www.kali.org), an industry-standard security and forensics operating system based upon [Debian GNU/Linux](https://debian.org).

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

### Tor Library Kiosks
When students are first introduced to [Tor](https://torproject.org), we will utilize Tor Browser in library kiosks at the [Lillian Goldman Law Library](https://library.law.yale.edu).

### FreedomBox Private Server
For demonstrations of Tor hidden services (.onion), we will utilize [FreedomBox](https://freedombox.org) servers provided by [Yale Privacy Lab](https://privacylab.yale.edu).  FreedomBox runs on Raspberry Pi and other mini-computers, also using Debian GNU/Linux.

#### Hardware Details
* Raspberry Pi 3 Model B v1.2
* 32 GB SD card
* 0.96" I2C IIC serial 128x64 OLED display
* TP-Link TL-WN722N N150 150Mbps USB WiFi

## Technical Requirements for Students

### Student Laptops
Students will bring their own laptops to class and will connect to the network via WiFi (SSID "ylscyber") with WPA2 passphrase security.

### Software Requirements
We will be utilizing a Command Line Interface (CLI) on each laptop.  Students will communicate and control Raspberry Pi mini-computers via the Secure Shell (SSH) protocol.  The software below was chosen for compatibility and consistency across common desktop operating systems,
* [Hyper](https://hyper.is) - Command Line Interface / Terminal Emulator
* [Filezilla Client](https://filezilla-project.org) - SSH / SFTP Client
* [Atom](https://atom.io) - Text Editor
* [Git for Windows](https://gitforwindows.org) - Includes files that may be required for SSH on Windows

## Course Outline 

### Week 1 - Practical Cybersecurity
* Our Approach
* Digital Self-Defense
* Classroom Network Diagram
* Command Line Interface (CLI)
* Raspberry Pi Assembly

### Week 2 - Get to Know Your Mini-Computer
* Command Line Basics
* Controlling Your Raspberry Pi via SSH
* Client/Server Model
* The Filesystem Tree
* Edit a File

### Week 3 - Operating Systems
* Admin / Root Access
* The Kernel
* Userspace
* Processes
* Rootkits

### Week 4 - Ownership & Permissions
* Permissions as a Structural Design for Security
* Creating Users and Groups
* Principle of Least Privilege
* Sandboxing & Isolation
* Privilege Escalation Attacks

### Week 5 - Normative Structure of a Network
* IP Address, Physical Address
* Networking Models & Protocols (OSI Model)
* Internet Infrastructure
* Request/Response via the Web
* Distributed Denial-of-Service (DDoS)

### Week 6 - Network Attacks
* Domain Names
* DNS Poisoning
* Changing Your Pi's Network Identification
* Ports & Firewalls
* Man-in-the-Middle Attacks (MITM)

### Week 7 - Secrecy & Encryption
* Obfuscation & Hashes
* Public/Private Keys
* HTTP Encryption (SSL/TLS)
* E-mail Encryption (PGP/GPG)
* Weaknesses

### Week 8 - Information Security
* Data as a Toxic Asset
* What is InfoSec?
* Confidentiality
* Integrity
* Availability

### Week 9 - Anonymity & The Dark Web
* Onion Routing (Tor)
* Censorship Circumvention
* Tor Config on FreedomBox
* Sharing Files Anonymously
* Cryptomarkets

### Week 10 - Cybercrime
* Cryptocurrency & Transactions
* Ransomware
* Fraud & Phishing
* Data Breaches
* Challenges for Attack Attribution

### Week 11 - Chains of Trust
* Trusted Software Distribution
* Software Verification
* Hardware Assurance
* Free & Open-Source Software
* Static Analysis

### Week 12 - Penetration Testing
* Cross-Site Scripting (XSS)
* SQL Injection Attacks
* Delivering Payloads
* Metasploit Framework
* Using Metasploit

### Week 13 - Threat Modeling
* Risks and Vulnerabilities
* Zero Day Attacks
* Attack Scenarios
* Mitigation
* Operational Security (OPSEC)
