# Packet Tracer #

1. Download the Packet Tracer 64-bit Linux Archive from your module website[1]
2. Save the downloaded .tar.gz file in the same folder that contains this README.md file
3. In a terminal (konsole/gnome-terminal/...) switch to the directory that contains this README.md file (e.g. cd Downloads/packet-tracer)
4. Type ```makepkg``` and press enter
5. If the build fails because of missing dependencies, install them with ```pacman```. After installing missing dependencies go back to step 4.
6. After makepkg finishes successfully, an installable package will have been produced. Install it with e.g.:
```sudo pacman -U packet-tracer-7.1-1-x86_64.pkg.tar.xz```
7. The EULA will be displayed during this process. If you do not agree with its terms, you need to remove the software straight away by uninstalling it with e.g. ```sudo pacman -R packet-tracer```
8. An icon has been created in your desktop environment to start PacketTracer, but you can equally just launch it by typing ```PacketTracer``` or ```PacketTracer7``` in any terminal opened from inside your graphical session.
9. You should now be able to launch Packet Tracer.

[1] https://learn2.open.ac.uk/course/view.php?id=205784&cmid=1105901

## NOTE ##
This package builder was made for Packet Tracer version 7.1. Additional work will be required to port it to other versions.

# Assessments #
Some assessements require your copy of Packet Tracer to communicate with the exam you are performing. You can test your system's readiness from the Cisco NetAcad website [2]

### Required packages: ###
* jre8-openjdk

### Readiness check ###
After downloading the file, open a terminal window and ```cd``` to the directory into which you have downloaded the jnlp file, then type in ```javaws PT-Assessment-Client.jnlp```. One or more security warnings will be displayed. After accepting them, it may take a minute or so before you can see the result of the test in your browser window.

### Packet tracer not found ###
If a warning is displayed that the Packet tracer directory could not be found, then it is possible that you need to log out of your GUI session and back in. The check looks for the PTDIR environment variable which is set during logins only.

[2] https://assessment.netacad.net/check/check.html

# UPDATE # 
I've run ahead to try an exam which uses Packet Tracer and at the moment I am getting an error, as per below
---
Unable To Determine Cisco Packet Tracer Installation Directory

The Packet Tracer Skills Assessment Player was unable to find the directory in which Packet Tracer is installed. Review the setup procedure for Packet Tracer Skills Assessments.

Important Note: If you have recently installed or upgraded Packet Tracer on your computer, you should re-start your computer to ensure that some important information about the Packet Tracer installation has been integrated into your computer's environment settings.

Message ID: XP-ERR-005

---

I will be debugging this later and report back here.
