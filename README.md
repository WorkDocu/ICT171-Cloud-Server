# ICT171 Cloud Server Project
**Student:** Bishnu Maya Ghalley  
**Student Number:** 35805427  
**University:** Murdoch University  
**Unit:** ICT171 – Introduction to Server Environments and Architectures  
**Server IP:** 15.134.204.1  
**HTTP URL:** http://ict171bishnu.duckdns.org  
**HTTPS URL:** https://ict171bishnu.duckdns.org  

---

## Project Overview
This project is a cloud-based web server hosted on AWS EC2 running Ubuntu 24.04 LTS with Apache as the web server. The website is accessible via a custom domain name with SSL/TLS encryption enabled through Let's Encrypt.

---

## Step 1 — Launch EC2 Instance
- Provider: Amazon Web Services (AWS)
- Instance type: t3.micro
- OS: Ubuntu Server 24.04 LTS
- Region: Asia Pacific (Sydney) — ap-southeast-2
- Storage: 8GB SSD

---

## Step 2 — Connect to Server via SSH
```bash
chmod 400 ~/Downloads/cloud-server.pem
ssh -i ~/Downloads/cloud-server.pem ubuntu@15.134.204.1
```

---

## Step 3 — Update Server
```bash
sudo apt update
```

---

## Step 4 — Install Apache Web Server
```bash
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl status apache2
```

---

## Step 5 — Upload Website
```bash
sudo nano /var/www/html/index.html
```
Paste the HTML content and save with Control+X, Y, Enter.

---

## Step 6 — Domain Name Setup
- Provider: DuckDNS (free — duckdns.org)
- Domain: ict171bishnu.duckdns.org
- Points to IP: 15.134.204.1
- Cost: $0 — completely free

---

## Step 7 — SSL Certificate
```bash
sudo apt install certbot python3-certbot-apache -y
sudo certbot --apache -d ict171bishnu.duckdns.org
```
- Certificate Provider: Let's Encrypt (free)
- Expires: 2026-08-25 (auto-renews)
- HTTPS URL: https://ict171bishnu.duckdns.org

---

## Step 8 — Bash Script
Script location: ~/server_check.sh

### Purpose
Checks if Apache is running and displays server uptime,
disk usage, memory usage, and current date and time.

### Create and run the script
```bash
nano ~/server_check.sh
chmod +x ~/server_check.sh
./server_check.sh
```

### Script contents
```bash
#!/bin/bash
# ICT171 Server Check Script
# Student: Bishnu Maya Ghalley
# Student Number: 35805427
# Purpose: Checks Apache status and displays server info

echo "================================"
echo "  ICT171 Server Status Check"
echo "  Bishnu Maya Ghalley (35805427)"
echo "================================"

if systemctl is-active --quiet apache2; then
    echo "Apache is RUNNING"
else
    echo "Apache is NOT running — starting it..."
    sudo systemctl start apache2
fi

uptime    # Server uptime
df -h /   # Disk usage
free -h   # Memory usage
date      # Current date and time
```

---

## Video Explainer

https://drive.google.com/file/d/1GgXFf4MDTzKpD_v-vUnyUEy3WDg-ehGd/view?usp=drive_link


---

## References
- Amazon Web Services. (2026). Amazon EC2. https://aws.amazon.com/ec2/
- Canonical. (2026). Ubuntu Server 24.04 LTS. https://ubuntu.com/server
- Apache Software Foundation. (2026). Apache HTTP Server. https://httpd.apache.org/
- DuckDNS. (2026). Free dynamic DNS. https://www.duckdns.org/
- Let's Encrypt. (2026). Free SSL/TLS certificates. https://letsencrypt.org/
