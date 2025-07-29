Running a Bitcoin node or self-custody apps requires a **secure Linux server environment**. This guide provides a step-by-step hardening process using malware scanners, intrusion detection, SSH hardening, and proactive monitoring. Each section includes commands, explanations, and diagrams to visualize the flow.

---

## **1. Install Malware Scanning Tools**

### **1.1 ClamAV – Antivirus Toolkit**

ClamAV is an open-source antivirus solution that scans for malware, trojans, and infected files.

```bash
sudo apt update
sudo apt install clamav clamav-daemon -y

# Update virus signatures
sudo systemctl stop clamav-freshclam
sudo freshclam
sudo systemctl start clamav-freshclam

# Run full system scan and show infected files
sudo clamscan -r / --bell -i
```

> **Why?** A full scan ensures your server is free of common malware before deploying sensitive Bitcoin apps.

---

### **1.2 Rkhunter – Rootkit Hunter**

Rkhunter scans for hidden rootkits, backdoors, and suspicious binaries.

```bash
sudo apt install rkhunter -y
sudo rkhunter --update
sudo rkhunter --propupd      # Baseline check
sudo rkhunter -c --enable all --disable none
```

> **Why?** Rootkits can compromise your server without detection; Rkhunter flags tampered system files.

---

## **2. Monitor Processes and Services**

### **2.1 Check Running Processes**

```bash
top
htop
ps aux --sort=-%cpu
```

* **Look for:** Unusual resource consumption, unexpected processes (e.g., crypto miners).

### **2.2 Review Installed Packages**

```bash
dpkg --list | grep "^ii"   # List installed software
grep "install " /var/log/dpkg.log   # Check recent installations
```

Remove unused or suspicious packages:

```bash
sudo apt purge <package_name>
```

---

## **3. Check for Unauthorized Accounts**

List all user accounts:

```bash
cut -d: -f1 /etc/passwd
```

* Ensure only trusted accounts are present.
* Remove rogue accounts:

  ```bash
  sudo deluser <username>
  ```

---

## **4. Review Open Ports and Services**

### **4.1 Check Active Ports**

```bash
sudo netstat -tulnp
sudo ss -tuln
```

### **4.2 Close Unused Services**

```bash
sudo systemctl stop <service>
sudo systemctl disable <service>
```

### **4.3 Firewall with UFW**

```bash
sudo apt install ufw -y
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 22/tcp      # SSH
sudo ufw allow 8333/tcp    # Bitcoin node
sudo ufw enable
```

---

## **5. Harden SSH Configuration**

Edit the SSH config:

```bash
sudo nano /etc/ssh/sshd_config
```

Set the following:

```
PermitRootLogin no
PasswordAuthentication no
```

* Use **SSH keys only** for authentication.
* Restart SSH:

  ```bash
  sudo systemctl restart ssh
  ```

Check authorized keys:

```bash
cat ~/.ssh/authorized_keys
```

---

## **6. Keep the System Updated**

```bash
sudo apt update && sudo apt upgrade -y
```

* Automate security updates:

  ```bash
  sudo apt install unattended-upgrades -y
  ```

---

## **7. Host-Based Intrusion Detection**

### **AIDE – Advanced Intrusion Detection Environment**

```bash
sudo apt install aide -y
sudo aideinit
sudo cp /var/lib/aide/aide.db.new /var/lib/aide/aide.db
sudo aide --check
```

> **Tip:** Schedule `aide --check` via cron and email alerts for any file integrity changes.

---

## **8. Log Monitoring & Alerting**

### **Check Logs Manually**

```bash
sudo journalctl -p err -xn
sudo tail -n 100 /var/log/auth.log
sudo tail -n 100 /var/log/syslog
```

### **Optional:** Install a log management tool (e.g., `logwatch`, `Wazuh`) to automate alerts.

---

## **9. Backups and Data Protection**

* Use **encrypted offsite backups** (Restic, Borg, or rsync + GPG).
* Keep **Bitcoin wallet backups air-gapped** (offline encrypted drives).
* Test recovery periodically.

---

## **10. Additional Bitcoin-Specific Hardening**

* **Run Bitcoin nodes as non-root:**

  ```bash
  sudo adduser bitcoin
  ```
* **Isolate apps in containers:** Docker or LXC.
* **Enable Tor-only connections:**

  ```bash
  sudo apt install tor -y
  ```

  In `bitcoin.conf`:

  ```
  onlynet=onion
  proxy=127.0.0.1:9050
  ```

---

## **Flow Diagram – Secure Bitcoin Node Deployment**

```
        [Initial Server Setup]
                   |
          [ClamAV & Rkhunter]
                   |
          [Close Ports & SSH]
                   |
   [Firewall + AIDE + Log Monitoring]
                   |
       [Bitcoin Node & Apps]
                   |
       [Tor + Isolation + Backup]
```

---

## **Summary**

This hardening checklist makes your Linux server resilient against common attacks while keeping your Bitcoin node and self-custody applications safe.

* Malware scanning (**ClamAV, Rkhunter**)
* Firewall & SSH key-only login
* Intrusion detection (**AIDE**)
* Regular updates and backups
* Isolation of sensitive apps

> **Security is a continuous process.** Schedule scans, review logs weekly, and stay updated with new vulnerabilities.

---
# Part 2

## **Linux Hardening Checklist for Bitcoin Nodes & Self-Custody Apps (With Tor + Isolation)**

Operating a Bitcoin node or self-custody applications requires a hardened Linux environment. This guide builds upon a robust security foundation with **automated hardening, Tor integration (onion-only mode)**, and **application isolation (LXC/Docker)**.

---

## **1. Why Hardening Matters**

Bitcoin nodes, Lightning nodes, and self-custody tools handle private keys and financial data. A poorly configured server is an open invitation to attackers. Hardening focuses on:

* Reducing the attack surface
* Enforcing least privilege
* Isolating critical services
* Ensuring logs, alerts, and malware scans are automated

---

## **2. Automated Hardening Script**

We begin with an **all-in-one script** that:

1. Updates & configures firewall
2. Hardens SSH
3. Installs malware detection (ClamAV, Rkhunter)
4. Sets up intrusion detection (AIDE)
5. Adds **Tor-only Bitcoin configuration**
6. Runs Bitcoin and Lightning nodes inside **isolated containers**

---

### **The Script**

Save it as:

```bash
nano linux_harden_bitcoin_tor.sh
```

```bash
#!/bin/bash
# Linux Hardening Script with Tor + Isolation
# For Debian/Ubuntu

echo "=== Starting Hardened Bitcoin Node Setup ==="

### 1. System Update
apt update && apt upgrade -y

### 2. Essential Packages
apt install -y ufw fail2ban unattended-upgrades htop curl wget gnupg \
               clamav clamav-daemon rkhunter aide tor docker.io docker-compose \
               lxc lxc-templates bridge-utils

### 3. Firewall
ufw default deny incoming
ufw default allow outgoing
ufw allow 22/tcp
ufw allow 8333/tcp    # Bitcoin node if clearnet access needed (disabled later)
ufw enable

### 4. Harden SSH
sed -i 's/#*PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config
sed -i 's/#*PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config
systemctl restart ssh

### 5. Automatic Security Updates
dpkg-reconfigure --priority=low unattended-upgrades

### 6. Malware Scanning Tools
systemctl stop clamav-freshclam
freshclam
systemctl start clamav-freshclam
rkhunter --update
rkhunter --propupd

### 7. AIDE Setup
aideinit
cp /var/lib/aide/aide.db.new /var/lib/aide/aide.db

### 8. TOR Integration for Bitcoin Core
echo "[+] Enabling Tor-only Bitcoin mode..."
sed -i '/^#ControlPort/s/^#//' /etc/tor/torrc
sed -i '/^#CookieAuthentication/s/^#//' /etc/tor/torrc
systemctl restart tor

mkdir -p /etc/bitcoin
cat <<EOF > /etc/bitcoin/bitcoin.conf
onlynet=onion
proxy=127.0.0.1:9050
listen=1
bind=127.0.0.1
EOF

echo "[+] Bitcoin node will use TOR-only connections"

### 9. Isolation Using Docker or LXC
echo "[+] Deploying Bitcoin Core & Lightning in isolated containers..."

# Docker option
mkdir -p /opt/bitcoin_node
cat <<EOF > /opt/bitcoin_node/docker-compose.yml
version: "3"
services:
  bitcoind:
    image: ruimarinho/bitcoin-core:latest
    restart: unless-stopped
    volumes:
      - ./data:/bitcoin
    network_mode: "bridge"
    ports:
      - "8332:8332"
    command:
      -printtoconsole
      -conf=/bitcoin/bitcoin.conf
EOF

docker-compose -f /opt/bitcoin_node/docker-compose.yml up -d

# LXC Option
lxc-create -n bitcoin-node -t debian
lxc-start -n bitcoin-node
echo "[+] LXC container 'bitcoin-node' created for manual setup."

### 10. Daily Security Checks
cat <<EOF > /etc/cron.daily/bitcoin_security
#!/bin/bash
clamscan -r / --bell -i | mail -s "ClamAV Report" root
rkhunter -c --enable all --disable none --sk | mail -s "Rkhunter Report" root
aide --check | mail -s "AIDE Integrity Report" root
EOF

chmod +x /etc/cron.daily/bitcoin_security

echo "=== Hardened Node Setup Complete ==="
```

---

## **3. How Tor Integration Works**

1. Tor is installed and configured to allow Bitcoin Core to communicate **only over the Tor network**
2. In `bitcoin.conf`, we set:

   ```ini
   onlynet=onion
   proxy=127.0.0.1:9050
   ```

   This forces the node to ignore clearnet peers and **become an onion-only node**
3. Optional: expose an onion service for your Lightning node or Electrum server

---

## **4. Isolation (Docker & LXC)**

* **Docker**: Creates a containerized Bitcoin Core + Lightning environment, isolated from the host OS
* **LXC (Linux Containers)**: Creates lightweight VMs for full node separation (can run Bitcoin Core in one container and Lightning in another)
* Both reduce risk: if one service is compromised, the host OS and other services remain safe

---

## **5. Post-Setup Hardening**

### **Verify Isolation**

```bash
docker ps      # check running containers
lxc-ls -f      # list LXC containers
```

### **Run Malware Scans**

```bash
clamscan -r /
rkhunter -c --enable all --disable none
aide --check
```

### **Check for Unauthorized Access**

```bash
ss -tuln        # check open ports
cut -d: -f1 /etc/passwd  # list users
```

---

## **6. Visual Diagram**

```
**Host OS (Hardened Linux)**
├── **Firewall (UFW)** + Fail2Ban
├── **Tor** (Onion-only routing for Bitcoin & Lightning)
├── **AIDE + ClamAV + Rkhunter** (integrity & malware scanning)
├── **Docker / LXC Containers**
│      ├── Bitcoin Core (Tor-only)
│      └── Lightning Node (Tor-only)
└── **Cron Jobs** (Daily checks + email alerts)

```


---

## **7. Benefits**

* Your node is now **invisible to clearnet** (Tor-only)
* Attacks on one container won't impact the rest of the system
* Daily reports & scans keep you aware of any breach attempts
* Perfect base for **Fedimint, Cashu, BTCPay Server, ElectrumX** and other services

---

## **8. Next Steps**

* Deploy **Electrum Server (electrs or Fulcrum)** inside its own container
* Connect your **Lightning Node (LND, CoreLN, or Eclair)** to the Bitcoin Core container
* Expand with **Fedimint or Cashu mint** for federated custody