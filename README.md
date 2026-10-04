# AWS EC2 User Data & Apache Web Server Automation Lab

A hands-on cloud automation project demonstrating how to eliminate manual server configuration by using **EC2 User Data** to automatically bootstrap an Apache web server on an Amazon Linux EC2 instance upon launch[cite: 1].

---

## Lab Overview & Architecture

<p align="center">
  <img src="images/watermarked_img_11790238507745010317.jpg" alt="AWS EC2 User Data Lab Architecture" width="100%">
</p>

---

## What the Automation Script Does

Instead of manually connecting via SSH to update packages and install software, the **User Data** script executes automatically on first boot[cite: 1]:
1. **Updates System Packages:** Runs `yum update -y` to keep the environment secure and up to date[cite: 1].
2. **Installs Apache Web Server:** Downloads and installs `httpd` (`httpd.x86_64`)[cite: 1].
3. **Manages Services:** Starts the Apache service and enables it on boot using `systemctl`[cite: 1].
4. **Deploys Custom Web Content:** Echoes a dynamic `hostname` HTML file straight into `/var/www/html/index.html`[cite: 1].

---

## User Data Script (`user-data.sh`)

```bash
#!/bin/bash
yum update -y
yum install -y httpd.x86_64
systemctl start httpd.service
systemctl enable httpd.service
echo "<h1>Hello from $(hostname -f)</h1>" > /var/www/html/index.html
