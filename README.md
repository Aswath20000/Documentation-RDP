RDP MITM Attack Project
----------------------------


Objective
----------


Demonstrate a Man-in-the-Middle (MITM) attack on a Remote Desktop Protocol (RDP) session to capture sensitive data and highlight the importance of securing remote connections.

Prerequisites
----------------
Operating System: Kali Linux (3 virtual machines)
Tools:
----------------

PyRDP (RDP MITM tool)

Ettercap (ARP spoofing)

Remmina (RDP client)

Wireshark (optional, for traffic analysis)

xRDP (RDP service on the server machine)


Installation Steps
------------------------------

Set up the environment:


Machine A (Server): 

Install xRDP:

"sudo apt update && sudo apt install xrdp"

Machine B (Client): 

Install Remmina:

"sudo apt update && sudo apt install remmina"

Machine C (MITM): 

Install PyRDP and Ettercap:

Clone PyRDP: 

"git clone https://github.com/GoSecure/pyrdp.git && cd pyrdp"

Install dependencies: 

"sudo pip3 install -r requirements.txt"

Install Ettercap: 

"sudo apt install ettercap-graphical"

Configure ARP spoofing:


Launch Ettercap on Machine C:

"sudo ettercap -G"

Perform ARP poisoning to redirect traffic between Machine A and Machine B.

Launch MITM attack:


Start PyRDP on Machine C:

"pyrdp-mitm --output-folder logs"

Establish an RDP connection using Remmina on Machine B to Machine A.


View captured traffic in PyRDP’s logs (e.g., mitm.log, ntlmssp.log).
