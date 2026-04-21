# 🐧 Linux Server Setup — Nginx Configuration
### A Complete Beginner's Guide — Step by Step, Command by Command

**DevOps Track** | Author: SolaRoyal | April 2026 | Live: https://solaroyal.duckdns.org

---

## 1. Topic & Description

### Topic

Provisioning and Securing a Linux Web Server on the Cloud Using Nginx, UFW Firewall, and Let's Encrypt SSL — From Zero to a Live HTTPS Website.

### Description

This guide documents a complete, hands-on process of building a production-ready Linux server from absolute scratch on Microsoft Azure's free tier. We cover everything a beginner needs: creating the server on the cloud, connecting to it remotely, creating users, locking it down for security, installing a web server, serving a real website and API endpoint, and securing it with a real SSL certificate that makes the padlock appear in every browser.

No Docker. No automation tools. No shortcuts. Just a bare Linux server and your hands — exactly how it is done in real professional environments.

> **Real-life analogy:** Think of this as building and securing a real house on the internet. We start with an empty plot of land (the cloud VM), construct the building (Ubuntu Linux), install a security system (UFW Firewall), hire a receptionist (Nginx), and get the building officially certified as safe (SSL certificate).

---

## 2. Aim & Objectives

### Aim

To give absolute beginners practical, real-world experience in Linux server administration, web server configuration, and cloud security — the foundational skills required for a career in DevOps, System Administration, or Cloud Engineering.

### Objectives

By the end of this project, you will be able to:

- Provision a Linux Virtual Machine on Microsoft Azure's free tier
- Connect to a remote server securely using SSH and key-based authentication
- Create and manage Linux user accounts with appropriate privilege levels
- Configure passwordless sudo for specific commands required by automation bots
- Harden SSH security by disabling root login and password-based authentication
- Configure UFW (Uncomplicated Firewall) to allow only necessary network ports
- Install Nginx and configure it to serve a static HTML website
- Configure Nginx to serve a JSON API endpoint with correct HTTP headers
- Obtain a free, browser-trusted SSL certificate using Let's Encrypt and Certbot
- Enforce HTTPS-only access with a permanent HTTP-to-HTTPS 301 redirect
- Understand, explain, and troubleshoot every command and tool used

---

## 3. Who Needs This?

| Role | Why They Need This |
|---|---|
| DevOps Engineers | They provision and maintain servers daily. This is core to their job. |
| Backend Developers | They need to deploy their own APIs to real servers. |
| Startup Founders (Tech) | They need to host their product cheaply without expensive managed services. |
| System Administrators | They manage fleets of servers and must know how to lock them down. |
| Cloud Engineers | Azure, AWS, and GCP all use Linux VMs as the foundation of cloud infra. |
| Freelance Developers | They deploy client websites and must configure hosting independently. |
| IT Students | This is core curriculum for networking and systems administration courses. |
| Cybersecurity Analysts | They need to understand server hardening to identify vulnerabilities. |
| Anyone with a Web Project | Anyone who wants a live website with HTTPS needs to know this. |

---

## 4. Real-Life Scenarios

### Scenario 1 — The Lagos Startup Developer
Chidi is a software developer in Lagos who just finished building a fintech app. He needs to host his backend API but doesn't want to pay $50/month for a managed platform. Using this guide, Chidi spins up an Azure free tier server in 10 minutes, configures Nginx to serve his API at `/api`, secures it with HTTPS so his mobile app can connect securely, and locks down the firewall so hackers can't probe the server. Total monthly cost: ₦0. His API is live, secure, and accessible to users worldwide.

### Scenario 2 — The Freelance Web Developer
Amaka is a freelancer in Ibadan. Her client wants a portfolio website deployed on a real server with a real domain and the SSL padlock visible in the browser. Without SSL, modern browsers show a red 'Not Secure' warning that scares visitors away. Using this guide, Amaka provisions a server, installs Nginx, serves the HTML files, and gets a free Let's Encrypt certificate. The client sees the padlock and the professional HTTPS URL. Client is impressed. Amaka gets paid.

### Scenario 3 — The DevOps Intern on Day One
Tunde just got his first DevOps internship at a Lagos tech company. On day one, the senior engineer asks him to provision a Linux test server for the dev team, set up SSH key authentication, lock down the firewall, and configure a simple web endpoint. Because Tunde completed this project, he knows exactly what to do. He impresses the team within the first hour. This guide is what separates candidates who can talk theory from those who can actually do the work.

### Scenario 4 — The E-Commerce Business
A small online store in Abuja wants to accept payments on their website. Payment processors like Paystack and Stripe require HTTPS — they will refuse to load on plain HTTP pages. Their developer uses this guide to set up a secure Linux server, configure Nginx, and install an SSL certificate. Without this setup, the business literally cannot collect online payments. With it, customers see the padlock, trust the site, and checkout confidently.

### Scenario 5 — The University Final Year Project
Blessing is a final-year Computer Science student at UNILAG. Her project requires a live backend server accessible from the internet so her supervisor can test it. Rather than submitting screenshots, she uses this guide to deploy a real live server with a real HTTPS URL. Her supervisor opens it in a browser, sees the padlock, visits `/api` and gets the JSON response. She scores full marks.

---

## 5. Problems This Guide Solves

| Problem | How This Guide Solves It |
|---|---|
| 'How do I host my app without paying $50/month?' | Azure free tier + Nginx replaces expensive managed hosting — cost: $0 |
| 'My site shows Not Secure in Chrome' | Let's Encrypt SSL certificate adds HTTPS and the padlock — for free |
| 'Someone accessed my server as root and broke everything' | We disable root SSH login entirely — nobody can log in as root remotely |
| 'My server keeps getting brute-force password attacks' | We disable password authentication — only SSH keys work, making attacks useless |
| 'My server got port-scanned and attackers found open services' | UFW firewall closes ALL ports except 22, 80, 443 — everything else is invisible |
| 'My API doesn't tell the browser it's JSON' | Nginx `add_header Content-Type application/json` fixes this correctly |
| 'Users keep using http:// and their data is unencrypted' | 301 permanent redirect forces ALL traffic to HTTPS automatically |
| 'I don't know what user permissions to use for my server' | Non-root user with targeted sudo is the industry standard — we implement it here |
| 'The grading bot can't check my server config' | Passwordless sudo for sshd and ufw allows automated checks without a password |

---

## 6. Technologies & Tools Explained

### 6.1 Microsoft Azure

Azure is Microsoft's cloud computing platform — a massive worldwide network of data centres you can rent computers from over the internet. Instead of buying a physical server, you rent a Virtual Machine (VM) from Azure and pay only for what you use. The free tier gives you 750 hours per month of a small VM — enough to run this entire project permanently at zero cost.

> **Analogy:** Azure is like Airbnb for computers. You rent the room, use it, and walk away. You don't own the building, and you don't maintain it.

**Reference:** https://azure.microsoft.com/en-us/free/

### 6.2 Ubuntu Linux 22.04 LTS

Ubuntu is a free, open-source operating system based on Linux — the most widely used server OS in the world, used by Netflix, Uber, Airbnb, and millions of other services. LTS stands for Long-Term Support, meaning Canonical guarantees security updates for 5 years. Version 22.04 is supported until 2027.

> **Analogy:** If Windows is a luxury car with a fancy dashboard, Ubuntu Server is a Formula 1 race car — stripped of everything unnecessary, extremely fast and powerful, but you need to learn to drive it properly.

**Reference:** https://ubuntu.com/server/docs

### 6.3 SSH (Secure Shell)

SSH is a network protocol that allows you to securely connect to and control a remote computer over the internet. It encrypts everything — your commands, the server's responses, and your credentials.

SSH uses a key pair for authentication:
- **Private Key:** Stays on your laptop. Never share this. It is your house key.
- **Public Key:** Goes on the server in a file called `authorized_keys`. It is the lock on the door.

> **Analogy:** SSH is a secure telephone call to your server. The encryption ensures nobody can eavesdrop, and the key pair ensures only you can call.

**References:** https://www.ssh.com/academy/ssh | https://www.openssh.com/manual.html

### 6.4 sshd — The SSH Daemon

`sshd` (SSH Daemon) is the background program running silently on your server, listening for incoming SSH connection attempts on port 22.

- `sshd -T` — Prints the complete active SSH configuration
- `sshd_config` — The file at `/etc/ssh/sshd_config` where all SSH rules are defined
- `systemctl restart ssh` — Restarts sshd to apply config changes

> **Analogy:** `sshd` is the doorman at your server's front entrance. It checks credentials before letting anyone in, and `sshd -T` is you asking the doorman to read out his current rulebook.

### 6.5 UFW — Uncomplicated Firewall

UFW is a firewall management tool built into Ubuntu. Without a firewall, every port on your server is potentially accessible, and automated bots constantly scan for open ports to exploit.

Ports are like numbered doors into your server:

| Port | Service | Notes |
|---|---|---|
| 22 | SSH | Remote terminal access |
| 80 | HTTP | Unencrypted web traffic |
| 443 | HTTPS | Encrypted web traffic |
| 3306 | MySQL | **NEVER** open to the internet |
| 6379 | Redis | **NEVER** open to the internet |

> **Analogy:** UFW is a security guard at your building's main gate. You give the guard a list: 'Only let people through doors 22, 80, and 443. Everyone else — turn them away immediately.'

**Reference:** https://help.ubuntu.com/community/UFW

### 6.6 Nginx (Engine-X)

Nginx (pronounced Engine-X) is a high-performance web server and reverse proxy. When someone types your domain into their browser, Nginx receives that request and decides what to send back. Companies like Dropbox, Netflix, and WordPress.com use it.

In this project, Nginx does two jobs:
- Serves the static HTML page at `/` (the homepage)
- Returns a JSON response at `/api` with the correct Content-Type header

> **Analogy:** Nginx is a highly efficient hotel receptionist. When any guest (web request) walks in, the receptionist instantly knows exactly which room (content) they need and hands it to them. Even if 10,000 guests arrive simultaneously, the receptionist handles them all without breaking a sweat.

**Reference:** https://nginx.org/en/docs/

### 6.7 Let's Encrypt & Certbot

Let's Encrypt is a free, non-profit Certificate Authority (CA) that issues SSL/TLS certificates trusted by all major browsers. Before Let's Encrypt (launched in 2016), SSL certificates cost $100–500 per year.

Certbot is the official tool (by the EFF) that automates obtaining, installing, and renewing Let's Encrypt certificates.

> **Analogy:** Let's Encrypt is a government office that gives out free, official ID cards (SSL certificates) that every bank (browser) in the world recognises. Certbot is the trusted agent who goes to that office on your behalf, does all the paperwork, and delivers your ID card to your door.

**References:** https://letsencrypt.org/docs/ | https://certbot.eff.org/docs/

### 6.8 DuckDNS

DuckDNS is a free dynamic DNS service. DNS translates human-readable domain names like `solaroyal.duckdns.org` into IP addresses that computers use to find each other. DuckDNS gives you a permanent, free subdomain that always points to your server's IP.

> **Analogy:** DuckDNS is like getting a free business address plaque. Instead of telling customers 'come to building number 20.10.5.123 on server street', you give them 'solaroyal.duckdns.org' — memorable, professional, and always up to date.

**Reference:** https://www.duckdns.org/

---

## 7. The Sudoers Rule — Fully Explained

The assignment requires this specific line in the sudoers configuration:

```
hngdevops ALL=(root) NOPASSWD:/usr/sbin/sshd,/usr/sbin/ufw
```

| Part of the Line | Plain English Meaning |
|---|---|
| `hngdevops` | This rule applies to the Linux user account called hngdevops |
| `ALL=` | This rule applies from ANY terminal, location, or context on this server |
| `(root)` | When these commands run, they will execute with root (administrator) privileges |
| `NOPASSWD:` | Do NOT ask for a password when running the following commands |
| `/usr/sbin/sshd` | Full path to the SSH daemon program. Allowed without password. |
| `,` | AND also the following command |
| `/usr/sbin/ufw` | Full path to the UFW firewall program. Allowed without password. |

> **Why only these two commands?** This is the security principle of **Least Privilege** — you grant the minimum permissions required and nothing more. The HNG grading bot only needs to run `sshd -T` and `ufw status` to verify your configuration.

> **Why does the bot need this?** The HNG grading bot SSHes into your server as `hngdevops`, then runs `sudo sshd -T` and `sudo ufw status`. If it gets asked for a password, it cannot continue — robots cannot type passwords.

---

## 8. Nginx Configuration File — Every Line Explained

```nginx
server {
    listen 443 ssl;
    server_name solaroyal.duckdns.org;

    location / {
        root /var/www/hng;
        index index.html;
    }

    location /api {
        add_header Content-Type application/json;
        return 200 '{"message":"HNGI14 Stage 0","track":"DevOps","username":"SolaRoyal"}';
    }

    ssl_certificate /etc/letsencrypt/live/solaroyal.duckdns.org/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/solaroyal.duckdns.org/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
}

server {
    listen 80;
    server_name solaroyal.duckdns.org;
    return 301 https://$host$request_uri;
}
```

| Line / Directive | What It Does | Plain English |
|---|---|---|
| `server { }` | A server block — container for rules for one domain | A rule set for one specific domain |
| `listen 443 ssl;` | Listen on port 443 and use SSL encryption | Open the HTTPS door and use encryption |
| `listen 80;` | Listen on port 80 (HTTP) | Open the regular HTTP door |
| `server_name domain;` | This block handles requests for this domain only | This ruleset belongs to this specific domain |
| `location / { }` | Rules for requests to the homepage URL | What to do when someone visits the homepage |
| `root /var/www/hng;` | Look for files to serve in this folder | The filing cabinet where website files are stored |
| `index index.html;` | Serve index.html as the default page | Open this file if no specific file is requested |
| `location /api { }` | Rules for requests to /api URL | What to do when someone visits /api |
| `add_header Content-Type application/json;` | Tells the browser this response is JSON | Labels the response: 'This is JSON data' |
| `return 200 '{...}';` | Send back HTTP 200 (success) with JSON body | Reply with: success + the JSON content |
| `ssl_certificate ...pem;` | Path to the SSL certificate file | Here is my official ID card (certificate) |
| `ssl_certificate_key ...pem;` | Path to the SSL private key | Here is the private key that proves the cert is mine |
| `return 301 https://$host$request_uri;` | Permanently redirect HTTP to HTTPS | Tell the visitor: go to the secure version — permanently |

---

## 9. HTTP Status Codes Explained

| Code | Name | Meaning | Real-Life Analogy |
|---|---|---|---|
| 200 | OK | Request succeeded. Here is what you asked for. | You knocked. The door opened. You got what you came for. |
| 301 | Moved Permanently | This URL has permanently moved. Go to the new address forever. | The shop permanently moved. Go to the new address — always. |
| 302 | Found (Temp) | Temporarily redirected. The old address may come back. | The shop is temporarily at a different location today only. |
| 404 | Not Found | The page or resource you asked for does not exist. | You knocked on a door that does not exist in this building. |
| 500 | Server Error | Something went wrong on the server. | The receptionist fainted when you asked your question. |

> ⚠️ **WARNING:** The assignment requires a **301** redirect, NOT 302. A 301 tells browsers and search engines this redirect is PERMANENT. A 302 is temporary and will not satisfy the grading bot.

---

## ══ COMPLETE STEP-BY-STEP EXECUTION GUIDE ══
*Every phase, every step, every command — in the exact order of execution*

---

## PHASE 1 — Create Your Free Domain on DuckDNS

### Step 1: Sign up for DuckDNS

1. Go to https://www.duckdns.org and sign in with your Google account
2. In the 'sub domain' box, type a name you like (e.g., `solaroyal`)
3. Click **Add Domain**
4. You now have a free domain: `yourname.duckdns.org`

> **Keep this tab open.** You will come back to paste your server's IP address here after creating the Azure VM.

---

## PHASE 2 — Provision the Azure Virtual Machine

### Step 2: Create the VM on Azure

Go to [portal.azure.com](https://portal.azure.com) → **Create a resource** → search **Virtual Machine** → **Create**

| Field | Value to Enter | Why |
|---|---|---|
| Resource Group | Create new → `hng-devops` | A container to group all related resources |
| Virtual machine name | `hng-server` | The name of your server |
| Region | Any region closest to you | Closer region = lower latency |
| Image | Ubuntu Server 22.04 LTS | The Linux operating system we will use |
| Size | Standard_B1s | The smallest free-tier eligible size |
| Authentication type | SSH public key | Key-based authentication (more secure than password) |
| Username | `hngdevops` | The admin username on the server |
| Key pair name | `hng-key` | The name of your SSH key pair |
| Inbound ports | Allow 22, 80, 443 | Open these three ports for our use |

Click **Review + Create** → **Create** → **Download private key and create resource** (downloads `hng-key.pem`)

> ⚠️ **WARNING:** The `.pem` key file is your ONLY way to access this server. If you lose it, you cannot get back in. Save it somewhere safe.

### Step 3: Get the Server's IP Address

After deployment: **Go to resource** → copy the **Public IP address** (e.g., `20.10.5.123`)

### Step 4: Point Your Domain to the Server

Go back to DuckDNS → paste your Azure IP in the **current ip** box → click **Update IP**

---

## PHASE 3 — Connect to Your Server via SSH

### Step 5: Fix Key Permissions and Connect

**On Mac or Linux — open Terminal:**

```bash
# Navigate to where you downloaded the key
cd ~/Downloads

# Fix the key permissions — SSH refuses keys that are too open
chmod 400 hng-key.pem

# Connect to your server
ssh -i hng-key.pem hngdevops@YOUR_SERVER_IP
```

**On Windows — open PowerShell:**

```powershell
ssh -i hng-key.pem hngdevops@YOUR_SERVER_IP
```

| Part | Meaning |
|---|---|
| `ssh` | Secure Shell — the program that makes the remote connection |
| `-i hng-key.pem` | Use this key file as authentication (`-i` = identity file) |
| `hngdevops` | The username on the remote server |
| `@YOUR_SERVER_IP` | The IP address of your server |

When you see `hngdevops@hng-server:~$` — you are now inside the server.

---

## PHASE 4 — Update the Server & Set Up User

### Step 6: Update All System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

| Part | What It Does |
|---|---|
| `sudo` | Run as administrator (Super User DO) |
| `apt` | The package manager for Ubuntu |
| `update` | Refresh the list of available packages |
| `&&` | Only run the next command if the previous one succeeded |
| `upgrade` | Download and install all available updates |
| `-y` | Automatically answer 'yes' to all confirmation prompts |

### Step 7: Set a Password for hngdevops

```bash
sudo passwd hngdevops
```

Type your new password when prompted. You will not see any characters — that is normal.

### Step 8: Verify the User Has Sudo Privileges

```bash
sudo -l
groups hngdevops
```

You should see `sudo` in the groups list.

---

## PHASE 5 — Configure Passwordless Sudo for sshd and ufw

### Step 9: Create the Sudoers Rule File

```bash
sudo visudo -f /etc/sudoers.d/hngdevops
```

Type this **EXACTLY** in the editor:

```
hngdevops ALL=(root) NOPASSWD:/usr/sbin/sshd,/usr/sbin/ufw
```

Save: `Ctrl+X` → `Y` → `Enter`

### Step 10: Test Passwordless Sudo

```bash
sudo sshd -T | head -3
sudo ufw status
```

If neither command asks for a password, the configuration is correct.

---

## PHASE 6 — Set Up SSH Keys for hngdevops

### Step 11: Create the SSH Directory and Keys File

```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
touch ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

| Command | What It Does |
|---|---|
| `mkdir -p ~/.ssh` | Create the `.ssh` directory (and parents if needed) |
| `chmod 700 ~/.ssh` | Owner can read/write/enter. Group and others cannot. SSH requires this. |
| `touch ~/.ssh/authorized_keys` | Create the authorized keys file if it doesn't exist |
| `chmod 600 ~/.ssh/authorized_keys` | Owner can read/write. Nobody else can. SSH requires this. |

### Step 12: Add Your Public Key

```bash
echo "YOUR_PUBLIC_KEY_HERE" >> ~/.ssh/authorized_keys
```

> **Later:** When the HNG team posts their public key in `#track-devops`, add it the same way using the same `echo` command.

---

## PHASE 7 — Harden SSH Security

### Step 13: Edit the SSH Configuration File

```bash
sudo nano /etc/ssh/sshd_config
```

Use `Ctrl+W` to search for each line. Remove the `#` at the start (commented lines are ignored).

| Find This Line | Change It To | Why |
|---|---|---|
| `#PermitRootLogin ...` | `PermitRootLogin no` | Prevent anyone from SSHing as root. Root compromises are catastrophic. |
| `#PasswordAuthentication yes` | `PasswordAuthentication no` | Disable password login entirely. SSH keys cannot be guessed. |
| `#PubkeyAuthentication yes` | `PubkeyAuthentication yes` | Explicitly confirm key-based authentication is enabled. |
| `KbdInteractiveAuthentication yes` | `KbdInteractiveAuthentication no` | Disable keyboard-interactive auth (another form of password login). |

> ⚠️ **WARNING:** Before closing your current SSH session after making these changes, open a **SECOND** terminal window and test that you can still connect. If both sessions are closed before testing, you may be permanently locked out.

### Step 14: Save and Apply SSH Changes

```bash
# Restart SSH to apply the new configuration
sudo systemctl restart ssh

# Enable SSH to auto-start if the server reboots
sudo systemctl enable ssh

# Verify root login is now disabled
sudo sshd -T | grep permitrootlogin
# Expected output: permitrootlogin no

# Verify password authentication is now disabled
sudo sshd -T | grep passwordauthentication
# Expected output: passwordauthentication no
```

---

## PHASE 8 — Configure UFW Firewall

### Step 15: Install UFW and Configure Rules

```bash
# Check if UFW is installed
sudo ufw status

# Set defaults: block all incoming, allow all outgoing
sudo ufw default deny incoming
sudo ufw default allow outgoing

# Allow only the three required ports
sudo ufw allow 22   # SSH — without this, you lock yourself out!
sudo ufw allow 80   # HTTP
sudo ufw allow 443  # HTTPS

# Activate the firewall
sudo ufw enable

# Verify the configuration
sudo ufw status
```

**Expected output:**

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

**Quick test:** Open your browser and go to `http://YOUR_SERVER_IP` — you should see the default Nginx welcome page.

### Step 17: Create the Website HTML File

```bash
sudo mkdir -p /var/www/hng
sudo nano /var/www/hng/index.html
```

Paste this HTML (replace `YOUR_HNG_USERNAME` with your actual username, e.g. `SolaRoyal`):

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

> ⚠️ **WARNING:** The assignment checker looks for your HNG username as VISIBLE TEXT on the page. Do NOT put it in HTML comments or hidden elements.

### Step 18: Configure Nginx to Serve Your Site and API

```bash
sudo nano /etc/nginx/sites-available/default
```

Delete all existing content and replace with this (replace `YOUR_DOMAIN` and `YOUR_USERNAME`):

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

Save: `Ctrl+X` → `Y` → `Enter`

### Step 19: Test and Reload Nginx

```bash
# ALWAYS run this before reloading — tests config for errors
sudo nginx -t

# Apply the new configuration without fully restarting
sudo systemctl reload nginx
```

---

## PHASE 10 — Get SSL Certificate (Let's Encrypt)

> ⚠️ **WARNING:** Before running Certbot, make sure your domain is correctly pointing to your server's IP. Test it:
> ```bash
> ping YOUR_DOMAIN
> ```
> The IP shown should match your Azure server's public IP.

### Step 20: Install Certbot

```bash
sudo apt install certbot python3-certbot-nginx -y
```

| Package | What It Is |
|---|---|
| `certbot` | The main Certbot program that communicates with Let's Encrypt |
| `python3-certbot-nginx` | The Nginx plugin — lets Certbot automatically edit your Nginx config |

### Step 21: Obtain and Install the Certificate

```bash
sudo certbot --nginx -d YOUR_DOMAIN
```

Certbot will guide you through:
1. Enter your email address (for renewal reminders)
2. Agree to Terms of Service — type `A` and press Enter
3. Choose whether to share email with EFF — type `N` and press Enter

Certbot verifies you own the domain, downloads the certificate, and updates your Nginx config automatically.

### Step 22: Verify Certificate and Auto-Renewal

```bash
# Test that auto-renewal will work (certs expire every 90 days)
sudo certbot renew --dry-run
```

If you see `Congratulations, all renewals succeeded` — your server will automatically renew the certificate before it expires.

---

## PHASE 11 — Add the HNG Public Key

### Step 23: Add HNG's Key to authorized_keys

```bash
echo "PASTE_HNG_PUBLIC_KEY_HERE" >> ~/.ssh/authorized_keys

# Verify both keys are present
cat ~/.ssh/authorized_keys
```

You should see at least 2 separate keys listed.

---

## PHASE 12 — Verify Everything — Full Checklist

Run this single comprehensive check command:

```bash
echo '=== WHO AM I ===' && whoami && \
echo '=== UFW STATUS ===' && sudo ufw status && \
echo '=== ROOT LOGIN ===' && sudo sshd -T | grep permitrootlogin && \
echo '=== PASSWORD AUTH ===' && sudo sshd -T | grep passwordauthentication && \
echo '=== AUTHORIZED KEYS ===' && cat ~/.ssh/authorized_keys && \
echo '=== NGINX STATUS ===' && sudo systemctl status nginx | grep Active && \
echo '=== API TEST ===' && curl -s https://YOUR_DOMAIN/api && echo '' && \
echo '=== HTTP REDIRECT ===' && curl -sI http://YOUR_DOMAIN | grep -E '301|Location'
```

| Section | Expected Output | Pass / Fail Condition |
|---|---|---|
| WHO AM I | `hngdevops` | Must be hngdevops, not root or any other user |
| UFW STATUS | Status: active, ports 22/80/443 listed | Must show active and only these 3 ports |
| ROOT LOGIN | `permitrootlogin no` | Must be 'no' — not 'without-password' or 'yes' |
| PASSWORD AUTH | `passwordauthentication no` | Must be 'no' |
| AUTHORIZED KEYS | 2 or more keys shown | Must include both your key and HNG's key |
| NGINX STATUS | `active (running)` | Must be running |
| API TEST | `{"message":"HNGI14 Stage 0","track":"DevOps","username":"SolaRoyal"}` | Must match exactly — including username casing |
| HTTP REDIRECT | `HTTP/1.1 301 Moved Permanently` | Must be 301, not 302 |

### Step 24: Individual Verification Commands

```bash
# Test the API specifically
curl -s https://YOUR_DOMAIN/api

# Test the 301 redirect
curl -I http://YOUR_DOMAIN

# Test SSL certificate validity
curl -vI https://YOUR_DOMAIN 2>&1 | grep -E 'SSL|certificate'
```

Open `https://YOUR_DOMAIN` in your browser — you should see the padlock and your HNG username visible on the page.

---

## PHASE 13 — Submit Your Work

### Step 25: Final Checklist Before Submitting

- [ ] `https://yourdomain.com` loads with your HNG username visible on the page
- [ ] `https://yourdomain.com/api` returns the correct JSON with your exact username
- [ ] `http://yourdomain.com` redirects to HTTPS with a **301** status code
- [ ] SSL certificate is valid — green padlock visible in browser
- [ ] UFW is active with ONLY ports 22, 80, and 443 open
- [ ] `hngdevops` user exists and is the logged-in user
- [ ] Root SSH login is disabled (`permitrootlogin no`)
- [ ] Password SSH auth is disabled (`passwordauthentication no`)
- [ ] `hngdevops` can run `sshd -T` without a password prompt
- [ ] `hngdevops` can run `ufw status` without a password prompt
- [ ] HNG's public key is in `~/.ssh/authorized_keys`

### Step 26: Submit in the #track-devops Channel

Go to the HNG Discord/Slack server, find `#track-devops`, and type `/submitdevopsstage0`

Submit:
- Your live domain: `https://solaroyal.duckdns.org`
- Your HNG username: `SolaRoyal`

> **Important:** The username in your JSON response at `/api` must **EXACTLY** match your registered HNG username — including uppercase and lowercase letters.

---

## 10. Complete Commands Reference

| Command | Category | What It Does |
|---|---|---|
| `ssh -i key.pem user@ip` | SSH | Connect to a remote server using a key file |
| `chmod 400 key.pem` | Permissions | Make key file readable only by owner (required by SSH) |
| `chmod 700 ~/.ssh` | Permissions | Set .ssh folder to owner-only access |
| `chmod 600 ~/.ssh/authorized_keys` | Permissions | Set authorized_keys to owner read/write only |
| `whoami` | User | Print the name of the currently logged-in user |
| `sudo passwd hngdevops` | User | Set or change the password for a user account |
| `sudo -l` | User | List all sudo permissions for the current user |
| `groups username` | User | List all groups a user belongs to |
| `sudo visudo -f /path` | Sudoers | Safely edit a sudoers file with syntax validation |
| `sudo apt update` | Packages | Refresh the list of available packages |
| `sudo apt upgrade -y` | Packages | Install all available package updates |
| `sudo apt install package -y` | Packages | Install a specific package |
| `sudo nano /path/to/file` | Files | Open a file for editing in the nano text editor |
| `cat /path/to/file` | Files | Display the contents of a file |
| `mkdir -p /path` | Files | Create a directory (and parents if needed) |
| `echo 'text' >> file` | Files | Append text to a file without overwriting it |
| `sudo systemctl start service` | Services | Start a background service |
| `sudo systemctl stop service` | Services | Stop a background service |
| `sudo systemctl restart service` | Services | Restart a service (stop + start) |
| `sudo systemctl reload service` | Services | Reload config without full restart |
| `sudo systemctl enable service` | Services | Set service to auto-start on boot |
| `sudo systemctl status service` | Services | Show current status of a service |
| `sudo sshd -T` | SSH | Print the full active SSH configuration |
| `sudo sshd -T \| grep keyword` | SSH | Print only the line containing the keyword |
| `sudo ufw default deny incoming` | Firewall | Block all incoming traffic by default |
| `sudo ufw default allow outgoing` | Firewall | Allow all outgoing traffic by default |
| `sudo ufw allow PORT` | Firewall | Open a specific port number |
| `sudo ufw enable` | Firewall | Activate the firewall |
| `sudo ufw status` | Firewall | Show current firewall rules and status |
| `sudo nginx -t` | Nginx | Test Nginx configuration for errors |
| `nginx -v` | Nginx | Show the installed Nginx version |
| `curl -s https://domain/path` | Testing | Fetch a URL silently and show response body |
| `curl -I http://domain` | Testing | Fetch only the HTTP headers (not the body) |
| `curl -sI http://domain \| grep 301` | Testing | Check if the URL returns a 301 redirect |
| `sudo certbot --nginx -d domain` | SSL | Obtain and install Let's Encrypt SSL certificate |
| `sudo certbot renew --dry-run` | SSL | Test that certificate auto-renewal will work |
| `ping domain` | Network | Test that a domain resolves to an IP address |
| `pwd` | Navigation | Print the full path of the current directory |
| `ls -la` | Navigation | List all files including hidden ones with permissions |
| `cd /path` | Navigation | Change the current directory to a different path |

---

## 11. Common Problems & Solutions

| Problem | Likely Cause | Solution |
|---|---|---|
| `Permission denied (publickey)` | Wrong key file or wrong permissions | Run: `chmod 400 hng-key.pem` then try again |
| `Failed to restart sshd.service` | On Ubuntu the service is called 'ssh' not 'sshd' | Use: `sudo systemctl restart ssh` |
| `permitrootlogin without-password` | The line in sshd_config still has `#` in front | Remove the `#` — a commented line is ignored |
| API returns 404 | Nginx config uses localhost but no server_name matches | Always test API with the full domain, not localhost |
| Certbot fails with connection error | Domain is not yet pointing to your server's IP | Update DuckDNS with your correct server IP and wait 1–2 minutes |
| `nginx -t` shows error | Syntax error in your Nginx config file | Read the error message — it tells you the exact line number |
| Browser shows 'Not Secure' | SSL certificate not installed or HTTP used instead of HTTPS | Run Certbot again or check Nginx config includes SSL lines |
| sudo asks for password (should not) | Sudoers file has syntax error or wrong path | Re-run: `sudo visudo -f /etc/sudoers.d/hngdevops` and verify |
| Locked out of server after SSH changes | Error in sshd_config prevents SSH from starting | Use Azure portal serial console to fix the config file |

---

## 12. References & Further Reading

### Official Documentation

| Topic | Resource | URL |
|---|---|---|
| Ubuntu Server | Official Ubuntu Server Guide | https://ubuntu.com/server/docs |
| Nginx | Official Nginx Documentation | https://nginx.org/en/docs/ |
| Let's Encrypt | Let's Encrypt Documentation | https://letsencrypt.org/docs/ |
| Certbot | Certbot Official Docs (EFF) | https://certbot.eff.org/docs/ |
| UFW Firewall | Ubuntu Community UFW Guide | https://help.ubuntu.com/community/UFW |
| SSH / OpenSSH | OpenSSH Manual Pages | https://www.openssh.com/manual.html |
| SSH Concepts | SSH Academy | https://www.ssh.com/academy/ssh |
| Azure Free Tier | Microsoft Azure Free Account | https://azure.microsoft.com/en-us/free/ |
| DuckDNS | DuckDNS Official Site | https://www.duckdns.org/ |
| sudoers File | Linux Man Pages — sudoers(5) | https://linux.die.net/man/5/sudoers |
| HTTP Status Codes | MDN Web Docs — HTTP Status | https://developer.mozilla.org/en-US/docs/Web/HTTP/Status |
| Linux Command Line | Ubuntu Beginners Tutorial | https://ubuntu.com/tutorials/command-line-for-beginners |

### Excellent Tutorial References (DigitalOcean)

- [How to Install Nginx on Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-22-04)
- [How to Set Up UFW on Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu)
- [How to Secure Nginx with Let's Encrypt](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04)
- [Initial Server Setup with Ubuntu](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-22-04)

---

## 🎉 Congratulations!

*You have just built and secured a real production-ready Linux web server from scratch.*

You provisioned a cloud VM, created a secure user, hardened SSH, configured a firewall, served a website and API with Nginx, and secured it all with a real SSL certificate.

**That is not beginner work. That is real DevOps.**

---

*Author: SolaRoyal | HNG DevOps Track | April 2026 | Live Server: https://solaroyal.duckdns.org*
