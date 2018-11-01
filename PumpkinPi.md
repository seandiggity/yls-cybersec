# Seasonal Hacking
## The Pumpkin Pi Project
### Yale Law School Cybersecurity (LAW 20301), Fall 2018
### Prepared by [Laurin Weissinger](https://twitter.com/LB_W_), Cyber Fellow

<img src="/img/pumpkin_pi_06.jpg" width="220px" align="right" />

### Concept
Build an easy and fun to hack excercise, which serves as a fun introduction to active IT Security research. As the class was one day before Halloween, a hackable Pumpkin was the obvious choice.

Furthermore, the exercise was meant to introduce the students to the process of security research, including steps like information gathering -- but also the idea of attaining specific objectives (rather than just breaking things).

Next week, we will be using virtual machines running metasploitable to demonstrate and have the students execute various attacks, and this was meant to be a fun teaser and introduction.

### Hardware
I needed for a small enough device to fit into a Pumpkin, and a  Raspberry Pi we had on site was suitable.

The LED module had to be ordered and shipped quickly, and had to have an easy to use interface / API. The students have learned a lot in this class but are still beginners. Furthermore, this exercise had to be completed within about 30 minutes. Unfortunately, we had no soldering tools on site, which is why a prebuilt solution was necessary in order to complete this project in time.

Due to these requirements, I ordered the PiTraffic Shield (usually meant to simulate an intersection) from SB Components. The PiTraffic shield offers 12 LEDs, four yellow, four red, and four green. All these LEDs can be controlled individually via simple and easily understandable python control scripts.

### Software Configuration
The Paspberry Pi ran on a standard Raspbian Stretch Lite (4.14), with one small modification: I allowed root access via SSH and set a simple, seasonal root password. The students are used to Kali Linux where the standard user is root, and they know the concept of the root user. This was to streamline the class and also part of the exercise.

I prepared the necessary scripts provided by SB Components on github and wrote a simple python script that simulates flames when running (see attached an early version of the effect, using a small kitchen container to soften/diffuse the effect). The script cycles through the yellow and red LEDs in a seemingly random manner, providing a sufficiently realistic flame effect. I also created a "maintenance" script, which turns off the yellow and red lights, and instead turns of the green lights. The objective for the students was to deactivate the flame effect and turn on the green lights.

### Exercise
The Pumpkin sat on a table in class, with the red and yellow LEDs simulating a candle. The objective I gave to students was to trigger the green lights, rather than just shutting the LEDs / the Pumpkin down (someone did anyway, which was interesting and followed by an explanation about objectives in hacking and security research...) Physical access was not allowed.

The first step was to figure out what we were trying to hack. Using "nmap", we tried to detect the operating system and other useful details. The students were then tasked to evaluate their target.

They quickly realised that this was a Raspberry Pi (MAC matching) running an up-to-date Linux. Therefore, it would be difficult to exploit.

As we all know, many administrators do use weak credentials, and luckily, the PumpkinPi administrator set a very weak and seasonal password. Using "hydra" and a wordlist, the students were able to brute force the password and gain access to the device.

However, this was not enough! As mentioned before, I set a specific objective while not denying the root user any rights. Indeed, one student just used the "shutdown" command and turned off the Pi. I then explained that in hacking and security research, it is important to know one's objectives and not simply "break things", while restarting the PumpkinPi.

On the system, I left some clues in the form of maintenance notes from one administrator to another -- an all too realistic scenario as many of us know too well. Using these notes, the students learned how to trigger python scripts via SSH. They also located the "maintenance" script I prepared, and successfully attained the objective of turning the light green. 

### Video

* [MP4 format](pumpkin_pi.m4v)

### Photos

<img src="/img/pumpkin_pi_06.jpg" width="220px" align="center" />

<img src="/img/pumpkin_pi_01.jpg" width="220px" align="center" />

<img src="/img/pumpkin_pi_02.jpg" width="220px" align="center" />

<img src="/img/pumpkin_pi_03.jpg" width="220px" align="center" />

<img src="/img/pumpkin_pi_04.jpg" width="220px" align="center" />

<img src="/img/pumpkin_pi_05.jpg" width="220px" align="center" />

<img src="/img/pumpkin_pi_vid.png" width="220px" align="center" />
