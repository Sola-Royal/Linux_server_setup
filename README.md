# Linux_server_setup
Provisioning and Securing a Linux Web Server on the Cloud Using Nginx, UFW Firewall, and Let's Encrypt SSL — From Zero to a Live HTTPS Website.


# 🚀 Linux Server Setup & Nginx Configuration
### HNG DevOps Track — Stage 0 | Complete Step-by-Step Guide

> **Author:** SolaRoyal | **Date:** April 2026 | **Live Demo:** https://solaroyal.duckdns.org

---

## 📌 Topic

**Provisioning and Securing a Linux Web Server on the Cloud Using Nginx, UFW Firewall, and Let's Encrypt SSL — From Zero to a Live HTTPS Website.**

---

## 📖 Description

This guide documents a complete hands-on process of building a production-ready Linux server from scratch on Microsoft Azure's free tier. No Docker. No automation tools. No shortcuts. Just a bare Linux server and your hands — exactly how it is done in real professional environments.

Every command is explained in plain English with real-life analogies so that even someone who has never touched a server before can follow along and understand what they are doing and why.

> 💡 **Think of it this way:** We are building a house on the internet. The Azure VM is the plot of land. Ubuntu is the building. UFW is the security system. Nginx is the receptionist. The SSL certificate is the official safety certification.

---

## 🎯 Aim & Objectives

**Aim:** Give absolute beginners practical real-world experience in Linux server administration, web server configuration, and cloud security.

**By the end of this guide you will:**
1. Provision a Linux VM on Microsoft Azure's free tier
2. Connect to a remote server securely using SSH key-based authentication
3. Create and manage Linux user accounts with appropriate privilege levels
4. Configure passwordless sudo for specific commands required by automation bots
5. Harden SSH — disable root login and password authentication
6. Configure UFW firewall to allow only necessary network ports
7. Install and configure Nginx to serve a static HTML website
8. Configure Nginx to serve a JSON API endpoint with correct HTTP headers
9. Obtain a free browser-trusted SSL certificate using Let's Encrypt + Certbot
10. Enforce HTTPS-only access with a permanent 301 redirect
11. Understand, explain, and troubleshoot every command and tool used

---

## 🌍 Who Needs This?

| Role | Why They Need This |
|---|---|
| DevOps Engineers | They provision and maintain servers daily — this is core to the job |
| Backend Developers | They need to deploy their own APIs to real servers |
| Startup Founders | They need to host products cheaply without expensive managed services |
| System Administrators | They manage fleets of servers and must know how to lock them down |
| Cloud Engineers | Azure, AWS, GCP — all use Linux VMs as the foundation |
| Freelance Developers | They deploy client websites and must configure hosting independently |
| IT Students | This is core curriculum for networking and systems courses |
| Cybersecurity Analysts | They need to understand server hardening to identify vulnerabilities |

---

## 🎬 Real-Life Scenarios

### Scenario 1 — The Lagos Startup Developer
Chidi just finished building a fintech app. He needs to host his backend API without paying $50/month for a managed platform. Using this guide, he spins up an Azure free tier server, configures Nginx to serve his API at `/api`, secures it with HTTPS, and locks down the firewall. Total monthly cost: ₦0. His API is live, secure, and accessible worldwide.

### Scenario 2 — The Freelance Web Developer
Amaka is a freelancer. Her client wants a portfolio website with a real domain and the SSL padlock. Without SSL, browsers show a red "Not Secure" warning that scares visitors. Using this guide, Amaka gets the certificate for free. Client sees the green padlock. Amaka gets paid.

### Scenario 3 — The DevOps Intern on Day One
Tunde just got his first DevOps internship. On day one, the senior engineer asks him to provision a Linux server and configure SSH key auth and firewall rules. Because Tunde completed this project, he knows exactly what to do. He impresses the team on day one.

### Scenario 4 — The E-Commerce Business
A small online store wants to accept payments. Payment processors like Paystack and Stripe **require HTTPS** — they refuse to load on plain HTTP pages. Their developer uses this guide to set up SSL. Without it, the business cannot collect online payments.

### Scenario 5 — The University Student
Blessing is a final-year CS student. Her project requires a live backend server. Rather than screenshots, she deploys a real live server with a real HTTPS URL. Her supervisor visits `/api`, sees the JSON, and sees the padlock. Full marks.

---

## 🏗️ Architecture Overview

```
Internet User
      |
      v
http://solaroyal.duckdns.org  --301 Redirect-->  https://solaroyal.duckdns.org
                                                           |
                                                    Azure VM (Ubuntu 22.04)
                                                           |
                                                      UFW Firewall
                                                  (Ports 22, 80, 443 only)
                                                           |
                                                   Nginx Web Server
                                                      /          \
                                                GET /            GET /api
                                             index.html       JSON Response
```

---

## 🧰 Technologies Explained

### Microsoft Azure
A cloud platform where you rent virtual computers over the internet by the hour. The free tier gives 750 hours/month — enough to run this project at zero cost.
- Reference: https://azure.microsoft.com/en-us/free/
- Analogy: Airbnb for computers. Rent the room, use it, walk away.

### Ubuntu Linux 22.04 LTS
A free open-source server OS used by Netflix, Uber, and Airbnb. LTS = Long-Term Support (5 years of security updates).
- Reference: https://ubuntu.com/server/docs

### SSH (Secure Shell)
A protocol for securely connecting to and controlling a remote computer over the internet. Uses a key pair: Private key (stays on your laptop) + Public key (goes on the server).
- Reference: https://www.ssh.com/academy/ssh
- Analogy: A secure phone call to your server. Only your key can open the lock.

### sshd (SSH Daemon)
The background program on your server listening on port 22 for incoming SSH connections. `sshd -T` prints the active config — used by the HNG grading bot to verify your security settings.

### UFW (Uncomplicated Firewall)
Firewall management tool built into Ubuntu. Controls which traffic is allowed in/out. Without UFW, all server ports are exposed to the internet.
- Reference: https://help.ubuntu.com/community/UFW
- Analogy: A security guard — only lets traffic through doors 22, 80, and 443.

### Nginx (Engine-X)
A high-performance web server. Receives incoming web requests and serves back HTML pages or API responses. Used by Dropbox, Netflix, WordPress.com.
- Reference: https://nginx.org/en/docs/
- Analogy: A hotel receptionist handling 10,000 guests simultaneously without slowing down.

### Let's Encrypt & Certbot
Let's Encrypt is a free non-profit Certificate Authority that issues SSL certificates trusted by all browsers. Certbot automates getting, installing, and renewing those certificates.
- Reference: https://letsencrypt.org/docs/ and https://certbot.eff.org/docs/
- Analogy: A free government ID card — Certbot handles all the paperwork for you.

### DuckDNS
A free dynamic DNS service that gives your server a human-readable domain name instead of a raw IP address.
- Reference: https://www.duckdns.org/

---

## 🔐 The Sudoers Rule — Fully Explained

```
hngdevops ALL=(root) NOPASSWD:/usr/sbin/sshd,/usr/sbin/ufw
```

| Part | Plain English Meaning |
|---|---|
| `hngdevops` | This rule applies to the user called hngdevops |
| `ALL=` | Applies from any terminal or location on this server |
| `(root)` | The commands run with root (administrator) privileges |
| `NOPASSWD:` | Do NOT ask for a password for the following commands |
| `/usr/sbin/sshd` | The SSH daemon program — allowed without password |
| `,` | AND also |
| `/usr/sbin/ufw` | The UFW firewall program — allowed without password |

**Why only these two?** Principle of Least Privilege — grant the minimum permissions needed. The HNG bot only needs `sshd -T` and `ufw status`. NOPASSWD for ALL commands would be a serious security risk.

---

## 💡 HTTP Status Codes

| Code | Name | Meaning | Analogy |
|---|---|---|---|
| 200 | OK | Request succeeded | You knocked, door opened, you got what you came for |
| 301 | Moved Permanently | Permanently redirect to new URL | Shop permanently moved — always go to new address |
| 302 | Found (Temporary) | Temporarily redirected | Shop is temporarily elsewhere today only |
| 404 | Not Found | The resource does not exist | You knocked on a door that does not exist |
| 500 | Server Error | Server crashed processing your request | The receptionist fainted |

> ⚠️ The assignment requires **301** — NOT 302. A 301 tells browsers this redirect is permanent and they should always use HTTPS. A 302 is temporary and fails the grading bot.

---

---

# COMPLETE STEP-BY-STEP EXECUTION GUIDE

> Every phase. Every step. Every command. In exact order of execution.

---

## PHASE 1 — Create Your Free Domain on DuckDNS

### Step 1: Get a Free Domain

1. Go to https://www.duckdns.org
2. Click "sign in" using your Google account
3. In the "sub domain" box, type a name (e.g. `solaroyal`)
4. Click "add domain"
5. You now have: `yourname.duckdns.org`

> Keep this tab open — you will return to paste your server IP address here after creating the Azure VM.

---

## PHASE 2 — Provision the Azure Virtual Machine

### Step 2: Create the VM on Azure

1. Go to portal.azure.com and sign in
2. Click **Create a resource** → search **Virtual Machine** → click **Create**
3. Fill in these settings:

| Field | Value | Why |
|---|---|---|
| Resource Group | Create new → `hng-devops` | Groups all related resources |
| VM name | `hng-server` | Name for your server |
| Region | Closest to you | Closer = lower latency |
| Image | **Ubuntu Server 22.04 LTS** | The Linux OS we will use |
| Size | **Standard_B1s** | Free tier eligible |
| Authentication | **SSH public key** | More secure than password |
| Username | **hngdevops** | The admin username on the server |
| Key pair name | `hng-key` | Name for your SSH key pair |
| Inbound ports | **22, 80, 443** | Allow SSH, HTTP, HTTPS |

4. Click **Review + Create** → **Create**
5. When prompted: click **"Download private key and create resource"** — downloads `hng-key.pem`

> ⚠️ CRITICAL: The `.pem` file is your ONLY way into this server. Lose it = locked out permanently. Save it to Desktop AND a backup location immediately.

### Step 3: Get Your Server's IP Address

1. Click "Go to resource" after deployment finishes
2. On the Overview page, copy the **Public IP address** (e.g. `20.10.5.123`)

### Step 4: Point Your Domain to the Server

1. Go back to your DuckDNS tab
2. Paste your Azure IP in the "current ip" field next to your domain
3. Click "update ip"
4. Your domain now points to your server

---

## PHASE 3 — Connect to Your Server via SSH

### Step 5: Connect from Your Laptop

**On Mac or Linux — open Terminal:**
```bash
# Navigate to where you downloaded the key
cd ~/Downloads

# Fix key permissions — SSH refuses keys that are too open to others
chmod 400 hng-key.pem
```

> `chmod 400` = make this file readable ONLY by the owner. SSH security requires this.

```bash
# Connect to your server
ssh -i hng-key.pem hngdevops@YOUR_SERVER_IP
```

**On Windows — open PowerShell:**
```powershell
ssh -i hng-key.pem hngdevops@YOUR_SERVER_IP
```

**Command breakdown:**
- `ssh` = the program that creates a secure remote connection
- `-i hng-key.pem` = use this key file as authentication
- `hngdevops` = the username on the remote server
- `@YOUR_SERVER_IP` = the IP address of your server

When you see: `hngdevops@hng-server:~$` — you are now inside the server.

---

## PHASE 4 — Update the Server & Set Up the User

### Step 6: Update All System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

| Part | What It Does |
|---|---|
| `sudo` | Run as administrator (Super User DO) |
| `apt` | Ubuntu package manager — like an app store for the terminal |
| `update` | Refresh list of available packages |
| `&&` | Only run next command if previous one succeeded |
| `upgrade` | Download and install all available updates |
| `-y` | Automatically answer "yes" to all confirmation prompts |

### Step 7: Set a Password for hngdevops

```bash
sudo passwd hngdevops
```

Type your password when prompted. You will not see characters as you type — that is normal. Press Enter. Type again to confirm.

### Step 8: Verify sudo Privileges

```bash
sudo -l
```
Expected: shows `NOPASSWD: ALL` or `(ALL : ALL) ALL`

```bash
groups hngdevops
```
Expected: `sudo` appears in the group list.

---

## PHASE 5 — Configure Passwordless Sudo for sshd and ufw

**Why?** The HNG grading bot SSHes into your server as `hngdevops` and runs `sudo sshd -T` and `sudo ufw status`. Robots cannot type passwords. We pre-approve exactly these two commands.

### Step 9: Create the Sudoers Rule

```bash
sudo visudo -f /etc/sudoers.d/hngdevops
```

> `visudo` is a special safe editor for sudoers files. It validates syntax before saving — preventing errors that could lock you out of sudo entirely.

Type this EXACTLY in the editor:
```
hngdevops ALL=(root) NOPASSWD:/usr/sbin/sshd,/usr/sbin/ufw
```

Save: **Ctrl+X → Y → Enter**

### Step 10: Test It Works

```bash
sudo sshd -T | head -3
sudo ufw status
```

If neither command asks for a password — configuration is correct.

---

## PHASE 6 — Set Up SSH Keys for hngdevops

### Step 11: Create the SSH Directory and Keys File

```bash
mkdir -p ~/.ssh
```
> Make the .ssh folder. `-p` = don't error if it already exists.

```bash
chmod 700 ~/.ssh
```
> 700 = Owner can read/write/enter. Group and Others cannot. SSH requires this permission level.

```bash
touch ~/.ssh/authorized_keys
```
> Create the file that stores authorized public keys.

```bash
chmod 600 ~/.ssh/authorized_keys
```
> 600 = Owner can read and write. Nobody else can do anything. SSH requires this.

### Step 12: Add Your Public Key

```bash
echo "YOUR_AZURE_PUBLIC_KEY_HERE" >> ~/.ssh/authorized_keys
```

> `>>` = append to file without overwriting existing content.

> Later: When the HNG team posts their public key in #track-devops, add it using the same echo command.

---

## PHASE 7 — Harden SSH Security

### Step 13: Edit the SSH Configuration File

```bash
sudo nano /etc/ssh/sshd_config
```

> `nano` = simple terminal text editor. `sshd_config` = the main SSH configuration file.

**In nano:**
- `Ctrl+W` = search for text
- Arrow keys = move cursor
- `Ctrl+X` → `Y` → `Enter` = save and exit

Find and change these four lines (use Ctrl+W to search for each):

> IMPORTANT: If a line starts with `#`, remove that `#`. A `#` makes the line a comment — it is completely ignored by the system.

| Find This | Change It To | Why |
|---|---|---|
| `#PermitRootLogin ...` | `PermitRootLogin no` | Nobody can SSH in as root — root compromises are catastrophic |
| `#PasswordAuthentication yes` | `PasswordAuthentication no` | Disable password login — SSH keys cannot be brute-forced |
| `#PubkeyAuthentication yes` | `PubkeyAuthentication yes` | Explicitly enable key-based authentication |
| `KbdInteractiveAuthentication yes` | `KbdInteractiveAuthentication no` | Disable keyboard-interactive auth (another form of password auth) |

> ⚠️ WARNING: Before closing your terminal after making these changes, open a SECOND terminal and test you can still connect. If you made a mistake, fix it from the first session before closing it.

### Step 14: Save and Apply Changes

```bash
# Restart SSH to apply the new configuration
sudo systemctl restart ssh

# Enable SSH to auto-start if the server ever reboots
sudo systemctl enable ssh

# Verify root login is now disabled
sudo sshd -T | grep permitrootlogin
# Expected: permitrootlogin no

# Verify password authentication is now disabled
sudo sshd -T | grep passwordauthentication
# Expected: passwordauthentication no
```

---

## PHASE 8 — Configure UFW Firewall

### Step 15: Set Up All Firewall Rules

```bash
# Block ALL incoming traffic by default
sudo ufw default deny incoming

# Allow all outgoing traffic
sudo ufw default allow outgoing

# Open port 22 — SSH (MUST do this FIRST before enabling firewall)
sudo ufw allow 22

# Open port 80 — HTTP web traffic
sudo ufw allow 80

# Open port 443 — HTTPS secure web traffic
sudo ufw allow 443

# Activate the firewall
sudo ufw enable
```

> It will ask you to confirm — type `y` and press Enter.

```bash
# Verify the configuration
sudo ufw status
```

Expected:
```
Status: active

To                         Action      From
--                         ------      ----
22                         ALLOW       Anywhere
80                         ALLOW       Anywhere
443                        ALLOW       Anywhere
```

---

## PHASE 9 — Install & Configure Nginx Web Server

### Step 16: Install Nginx

```bash
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
```

Look for: **`Active: active (running)`**

> Quick test: Open your browser and go to `http://YOUR_SERVER_IP` — you should see the default Nginx welcome page.

### Step 17: Create the Website HTML File

```bash
sudo mkdir -p /var/www/hng
sudo nano /var/www/hng/index.html
```

Paste this (replace `YOUR_HNG_USERNAME`):
```html
<!DOCTYPE html>
<html>
<head>
    <title>HNG DevOps Stage 0</title>
</head>
<body>
    <h1>YOUR_HNG_USERNAME</h1>
    <p>HNG DevOps Track — Stage 0</p>
</body>
</html>
```

Save: **Ctrl+X → Y → Enter**

> ⚠️ The assignment checker looks for your username as **visible text** on the page. Do NOT put it in HTML comments or hidden elements.

### Step 18: Configure Nginx to Serve Site and API

```bash
sudo nano /etc/nginx/sites-available/default
```

Delete ALL existing content and replace with this (replace `YOUR_DOMAIN` and `YOUR_USERNAME`):
```nginx
server {
    listen 80;
    server_name YOUR_DOMAIN;

    location / {
        root /var/www/hng;
        index index.html;
    }

    location /api {
        add_header Content-Type application/json;
        return 200 '{"message":"HNGI14 Stage 0","track":"DevOps","username":"YOUR_USERNAME"}';
    }
}
```

| Line | What It Does |
|---|---|
| `server { }` | Container for rules for one specific domain |
| `listen 80;` | Listen for traffic on port 80 (HTTP) |
| `server_name YOUR_DOMAIN;` | This block handles requests only for this domain |
| `location / { }` | Rules when someone visits the homepage URL |
| `root /var/www/hng;` | Serve files from this folder |
| `index index.html;` | Serve this file as the default page |
| `location /api { }` | Rules when someone visits /api URL |
| `add_header Content-Type application/json;` | Tell the browser: this response is JSON data |
| `return 200 '...';` | Reply with HTTP 200 (success) and the JSON content |

Save: **Ctrl+X → Y → Enter**

### Step 19: Test and Reload Nginx

```bash
# ALWAYS test config before applying — catches syntax errors without breaking anything
sudo nginx -t
```

Expected:
```
nginx: configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

```bash
# Apply new configuration
sudo systemctl reload nginx
```

---

## PHASE 10 — Get SSL Certificate (Let's Encrypt)

> ⚠️ Before running Certbot, your domain MUST be pointing to your server IP. Certbot proves domain ownership by making an HTTP request to your domain. If the domain doesn't resolve to your server, the request fails.

Test your domain resolves:
```bash
ping YOUR_DOMAIN
```
The IP shown must match your Azure server's public IP.

### Step 20: Install Certbot

```bash
sudo apt install certbot python3-certbot-nginx -y
```

| Package | What It Does |
|---|---|
| `certbot` | Communicates with Let's Encrypt servers and gets your certificate |
| `python3-certbot-nginx` | Allows Certbot to automatically update your Nginx config |

### Step 21: Obtain and Install the Certificate

```bash
sudo certbot --nginx -d YOUR_DOMAIN
```

Follow the prompts:
1. Enter your email address
2. Agree to Terms of Service → type `A` + Enter
3. Share email with EFF → type `N` + Enter

Certbot automatically: verifies domain, downloads certificate, updates your Nginx config with SSL settings and 301 redirect.

### Step 22: Test Auto-Renewal

```bash
sudo certbot renew --dry-run
```

> Let's Encrypt certs expire every 90 days. Certbot sets up auto-renewal. This command simulates renewal to confirm it will work when needed.

---

## PHASE 11 — Add the HNG Public Key

### Step 23: Add HNG's Grading Key

Go to **#track-devops** channel and copy the public SSH key posted by HNG, then:

```bash
echo "PASTE_HNG_PUBLIC_KEY_HERE" >> ~/.ssh/authorized_keys

# Verify both keys are present
cat ~/.ssh/authorized_keys
```

You should see at least 2 separate SSH public keys listed.

---

## PHASE 12 — Verify Everything

### Step 24: Run the Complete Verification

```bash
echo "=== WHO AM I ===" && whoami && \
echo "=== UFW STATUS ===" && sudo ufw status && \
echo "=== ROOT LOGIN ===" && sudo sshd -T | grep permitrootlogin && \
echo "=== PASSWORD AUTH ===" && sudo sshd -T | grep passwordauthentication && \
echo "=== AUTHORIZED KEYS ===" && cat ~/.ssh/authorized_keys && \
echo "=== NGINX STATUS ===" && sudo systemctl status nginx | grep Active && \
echo "=== API TEST ===" && curl -s https://YOUR_DOMAIN/api && echo "" && \
echo "=== HTTP REDIRECT ===" && curl -sI http://YOUR_DOMAIN | grep -E "301|Location"
```

| Section | Expected Output |
|---|---|
| WHO AM I | `hngdevops` |
| UFW STATUS | `Status: active` with ports 22, 80, 443 |
| ROOT LOGIN | `permitrootlogin no` |
| PASSWORD AUTH | `passwordauthentication no` |
| AUTHORIZED KEYS | 2 or more keys shown |
| NGINX STATUS | `active (running)` |
| API TEST | Correct JSON with your exact username |
| HTTP REDIRECT | `HTTP/1.1 301 Moved Permanently` |

### Step 25: Additional Checks

```bash
# Test API returns HTTP 200
curl -o /dev/null -s -w "%{http_code}" https://YOUR_DOMAIN/api
# Expected: 200

# Test API returns correct Content-Type
curl -sI https://YOUR_DOMAIN/api | grep -i content-type
# Expected: content-type: application/json

# Test SSL is valid
curl -vI https://YOUR_DOMAIN 2>&1 | grep "SSL certificate verify"
# Expected: SSL certificate verify ok
```

---

## PHASE 13 — Submit Your Work

### Step 26: Final Checklist

- [ ] `https://yourdomain.com` loads with your HNG username visible as text on the page
- [ ] `https://yourdomain.com/api` returns correct JSON with your exact username
- [ ] `http://yourdomain.com` redirects to HTTPS with HTTP status 301 (not 302)
- [ ] SSL certificate is valid — green padlock visible in browser
- [ ] UFW is active with ONLY ports 22, 80, 443 open
- [ ] `hngdevops` is the logged-in user
- [ ] Root SSH login is disabled (`permitrootlogin no`)
- [ ] Password SSH auth is disabled (`passwordauthentication no`)
- [ ] `hngdevops` can run `sudo sshd -T` without a password prompt
- [ ] `hngdevops` can run `sudo ufw status` without a password prompt
- [ ] HNG's public key is in `~/.ssh/authorized_keys`

### Step 27: Submit

Go to the **#track-devops** channel and type:
```
/submitdevopsstage0
```

Submit:
- **Live domain:** `https://solaroyal.duckdns.org`
- **HNG username:** `SolaRoyal` (exact casing!)

> ⚠️ The `username` field in your JSON at `/api` must EXACTLY match your registered HNG username. Wrong casing fails the grading bot check.

---

## 🔍 Complete Commands Reference

| Command | Category | What It Does |
|---|---|---|
| `ssh -i key.pem user@ip` | SSH | Connect to a remote server using a key file |
| `chmod 400 key.pem` | Permissions | Make key file readable only by owner (SSH requirement) |
| `chmod 700 ~/.ssh` | Permissions | Set .ssh folder to owner-only access |
| `chmod 600 ~/.ssh/authorized_keys` | Permissions | Set keys file to owner read/write only |
| `whoami` | User | Print the name of the current logged-in user |
| `sudo passwd user` | User | Set or change a user's password |
| `sudo -l` | User | List all sudo permissions for current user |
| `groups username` | User | List all groups a user belongs to |
| `sudo visudo -f /path` | Sudoers | Safely edit a sudoers file with syntax validation |
| `sudo apt update` | Packages | Refresh list of available packages |
| `sudo apt upgrade -y` | Packages | Install all available updates |
| `sudo apt install pkg -y` | Packages | Install a specific package |
| `sudo nano /path/file` | Files | Open a file in the nano text editor |
| `cat /path/file` | Files | Display the contents of a file |
| `mkdir -p /path` | Files | Create a directory and parent directories if needed |
| `echo 'text' >> file` | Files | Append text to end of file without overwriting |
| `touch file` | Files | Create an empty file if it does not exist |
| `sudo systemctl start svc` | Services | Start a background service |
| `sudo systemctl restart svc` | Services | Stop and start a service (applies config changes) |
| `sudo systemctl reload svc` | Services | Apply config changes without full restart |
| `sudo systemctl enable svc` | Services | Configure service to auto-start on every reboot |
| `sudo systemctl status svc` | Services | Show whether a service is running or stopped |
| `sudo sshd -T` | SSH | Print the complete active SSH configuration |
| `sudo sshd -T \| grep word` | SSH | Print only lines containing that word |
| `sudo ufw default deny incoming` | Firewall | Block all incoming traffic by default |
| `sudo ufw allow PORT` | Firewall | Open a specific port number |
| `sudo ufw enable` | Firewall | Activate the firewall |
| `sudo ufw status` | Firewall | Show current firewall rules and status |
| `sudo nginx -t` | Nginx | Test Nginx configuration for syntax errors |
| `sudo systemctl reload nginx` | Nginx | Apply new Nginx config without interrupting connections |
| `curl -s https://domain/path` | Testing | Fetch a URL and display the response body |
| `curl -I http://domain` | Testing | Fetch only the HTTP response headers |
| `curl -sI url \| grep 301` | Testing | Check if a URL returns a 301 redirect |
| `sudo certbot --nginx -d domain` | SSL | Obtain and auto-install SSL certificate |
| `sudo certbot renew --dry-run` | SSL | Test that certificate auto-renewal will work |
| `ping domain` | Network | Test that a domain resolves to an IP address |
| `pwd` | Navigation | Print the current directory path |

---

## ❌ Common Problems & Solutions

| Problem | Likely Cause | Solution |
|---|---|---|
| `Permission denied (publickey)` | Wrong key or wrong permissions | Run `chmod 400 hng-key.pem` then retry |
| `Failed to restart sshd.service` | On Ubuntu the service is called `ssh` not `sshd` | Use `sudo systemctl restart ssh` |
| `permitrootlogin without-password` | The line in sshd_config still has `#` prefix | Remove the `#` — commented lines are ignored |
| API returns 404 | Testing with localhost instead of domain | Always test with the full domain URL |
| Certbot fails — connection refused | Domain not yet pointing to server IP | Update DuckDNS IP, wait 2 minutes, retry |
| `nginx -t` shows syntax error | Mistake in Nginx config file | Read the error — it shows the exact line number |
| Browser shows "Not Secure" | SSL not installed or HTTP used | Re-run `sudo certbot --nginx -d YOUR_DOMAIN` |
| sudo asks for password (it should not) | Sudoers file has error or was not saved | Re-run `sudo visudo -f /etc/sudoers.d/hngdevops` |
| Locked out after SSH changes | Syntax error in sshd_config | Use Azure Portal serial console to fix config |
| Username check fails at submission | Wrong casing in JSON username field | Ensure exact match including uppercase and lowercase |

---

## 📚 References (Verified Official Sources)

| Topic | Resource | URL |
|---|---|---|
| Ubuntu Server | Official Ubuntu Server Guide | https://ubuntu.com/server/docs |
| Nginx | Official Nginx Documentation | https://nginx.org/en/docs/ |
| Let's Encrypt | Let's Encrypt Documentation | https://letsencrypt.org/docs/ |
| Certbot | Certbot Official Docs (EFF) | https://certbot.eff.org/docs/ |
| UFW Firewall | Ubuntu Community UFW Guide | https://help.ubuntu.com/community/UFW |
| OpenSSH | OpenSSH Manual Pages | https://www.openssh.com/manual.html |
| SSH Concepts | SSH Academy (ssh.com) | https://www.ssh.com/academy/ssh |
| Azure | Microsoft Azure Free Tier | https://azure.microsoft.com/en-us/free/ |
| DNS | DuckDNS | https://www.duckdns.org/ |
| sudoers | Linux Man Pages sudoers(5) | https://linux.die.net/man/5/sudoers |
| HTTP Status Codes | MDN Web Docs | https://developer.mozilla.org/en-US/docs/Web/HTTP/Status |
| Linux Basics | Ubuntu Beginner Tutorial | https://ubuntu.com/tutorials/command-line-for-beginners |
| Nginx on Ubuntu | DigitalOcean Tutorial | https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-22-04 |
| UFW on Ubuntu | DigitalOcean Tutorial | https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu |
| SSL with Nginx | DigitalOcean Tutorial | https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04 |
| Server Initial Setup | DigitalOcean Tutorial | https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04 |

---

## 🏆 What You Built

By completing this guide you have:

- Provisioned a real cloud server on Microsoft Azure
- Configured SSH key-based authentication from scratch
- Hardened SSH — no root login, no password access
- Built a firewall that blocks everything except what is needed
- Served a real website with Nginx
- Built a real JSON API endpoint with correct headers
- Secured everything with a browser-trusted SSL certificate
- Forced HTTPS for all traffic with a permanent 301 redirect

> "That is not beginner work. That is real DevOps." 🚀

---

**Author:** SolaRoyal | **HNG DevOps Track** | **April 2026**  
**Live Server:** https://solaroyal.duckdns.org
