# AWS EC2 Ubuntu Instance Creation & SSH Access (Complete Guide)

> **Purpose:** This README provides **end-to-end steps** to create an **AWS EC2 Ubuntu instance**, configure security, connect via **SSH**, and perform **basic OS setup**. Written for **beginners**, **hands-on practice**, and **interview prep**.

---

## 📌 Prerequisites

Before starting, ensure:

* AWS account is created and verified
* Valid payment method added (Free Tier is enough)
* Laptop/PC with:

  * Windows / Linux / macOS
  * Internet access
* Basic terminal knowledge

---

## 1️⃣ Login to AWS Console

1. Open browser
2. Go to:

   ```
   https://aws.amazon.com/console/
   ```
3. Click **Sign In to the Console**
4. Login using your AWS credentials

✅ You will land on **AWS Management Console**

---

## 2️⃣ Select AWS Region

* Top-right corner → Select region

Recommended:

* **ap-south-1 (Mumbai)** – low latency for India

📌 Region matters for:

* EC2 availability
* Pricing
* Latency

---

## 3️⃣ Open EC2 Service

1. In search bar, type **EC2**
2. Click **EC2 – Virtual Servers in the Cloud**

You will see EC2 Dashboard

---

## 4️⃣ Launch EC2 Instance

1. Click **Launch instance**

---

## 5️⃣ Name and Tags

### 🔹 Instance Name

Example:

```
ubuntu-jenkins-server
```

📌 Naming helps identify purpose easily

---

## 6️⃣ Choose AMI (Operating System)

Select:

✔ **Ubuntu Server 22.04 LTS (Free Tier Eligible)**

📌 Why Ubuntu?

* Stable
* Most tutorials available
* Jenkins, Docker, Java friendly

---

## 7️⃣ Choose Instance Type

Select:

✔ **t2.micro** (Free Tier)

Specifications:

* 1 vCPU
* 1 GB RAM

📌 Good for:

* Learning
* Jenkins
* Small apps

---

## 8️⃣ Create Key Pair (SSH Access)

### 🔐 Key Pair is REQUIRED for SSH

1. Click **Create new key pair**
2. Key pair name:

   ```
   ubuntu-keypair
   ```
3. Key pair type:

   * RSA
4. Private key file format:

   * `.pem`
5. Click **Create key pair**

⬇️ `.pem` file will download automatically

⚠️ **IMPORTANT:**

* Do NOT delete or share this file
* Without this, SSH is impossible

---

## 9️⃣ Network Settings (Security Group)

### ✔ Allow required traffic

Configure:

* SSH → Port **22** → Source: **My IP**
* HTTP → Port **80** → Source: **Anywhere** (optional)
* HTTPS → Port **443** → Source: **Anywhere** (optional)

📌 Security Group acts as **Firewall**

---

## 🔟 Configure Storage

Default:

* 8 GB (Free Tier)

Recommended:

* 20 GB (safe for Jenkins, logs)

---

## 1️⃣1️⃣ Launch Instance

1. Review all details
2. Click **Launch instance**

✅ Instance state → **Running**

---

## 1️⃣2️⃣ Get Public IP Address

1. Go to **EC2 → Instances**
2. Select your instance
3. Copy:

   * **Public IPv4 address**

Example:

```
13.xxx.xxx.xxx
```

---

## 1️⃣3️⃣ Connect to EC2 via SSH (Ubuntu)

---

### 🪟 Windows (Using Git Bash / PowerShell)

1. Open Git Bash
2. Go to folder where `.pem` file is saved

```bash
cd Downloads
```

3. Set permissions:

```bash
chmod 400 ubuntu-keypair.pem
```

4. SSH command:

```bash
ssh -i ubuntu-keypair.pem ubuntu@<PUBLIC-IP>
```

---

### 🐧 Linux / macOS

```bash
chmod 400 ubuntu-keypair.pem
ssh -i ubuntu-keypair.pem ubuntu@<PUBLIC-IP>
```

---

✅ Successful login shows:

```
ubuntu@ip-172-31-xx-xx:~$
```

---

## 1️⃣4️⃣ Basic Ubuntu OS Setup

### Update system

```bash
sudo apt update
sudo apt upgrade -y
```

---

### Install basic tools

```bash
sudo apt install -y git curl wget unzip
```

---

### Check OS version

```bash
lsb_release -a
```

---

## 1️⃣5️⃣ Install Java (Required for Jenkins)

```bash
sudo apt install -y openjdk-17-jdk
java -version
```

---

## 1️⃣6️⃣ Common SSH Issues & Fixes

### ❌ Permission denied (publickey)

✔ Check:

* Correct `.pem` file
* Correct username → `ubuntu`

---

### ❌ Connection timeout

✔ Check:

* Security Group allows SSH (port 22)
* Correct Public IP

---

## 1️⃣7️⃣ EC2 Interview Notes

* EC2 = Elastic Compute Cloud
* AMI = OS template
* Security Group = Virtual firewall
* Key Pair = SSH authentication
* t2.micro = Free Tier instance
* Ubuntu user = `ubuntu`

---

## 1️⃣8️⃣ Best Practices

✔ Stop instance when not in use
✔ Never expose port 22 to public
✔ Keep `.pem` file secure
✔ Use Elastic IP for static IP (optional)

---

## ✅ Summary Flow

```
AWS Account
   ↓
EC2 Service
   ↓
Launch Ubuntu Instance
   ↓
Create Key Pair
   ↓
Configure Security Group
   ↓
SSH Login
   ↓
Ubuntu Setup
```

---

## 🚀 Next Steps

* Install Jenkins
* Install Docker
* Setup CI/CD
* Connect GitHub repository

---

📘 **This README can be directly used in GitHub repositories**

---

✍️ *Author: sona*
