
# OpenClaw AWS EC2 Setup Guide

> Complete step-by-step guide to deploy OpenClaw on AWS EC2 with automation scripts, cloud-init, API configuration, and production-ready infrastructure.

---

## 🔥 What This Repository Solves

This project provides a **production-ready deployment framework** for installing and running OpenClaw on AWS EC2.

It includes:

- Automated EC2 provisioning support
- cloud-init bootstrapping
- Secure SSH configuration
- OpenRouter integration
- ElevenLabs integration
- Brave Search API support
- ZAI API support
- Telegram Bot integration
- Optional Ollama local model support
- Production deployment best practices

If you are searching for:

- OpenClaw AWS setup
- OpenClaw EC2 deployment
- Install OpenClaw on AWS
- Deploy OpenClaw on cloud server
- OpenClaw production configuration

This guide covers everything.

---

# 🏗 Architecture Overview

```

User → Browser (localhost tunnel)
↓
SSH Port Forwarding
↓
AWS EC2 (Ubuntu)
↓
OpenClaw Gateway
↓
APIs (OpenRouter / Brave / ElevenLabs / ZAI)

````

---

# 🧰 Tech Stack

- AWS EC2
- Ubuntu Server
- Node.js LTS
- OpenClaw
- Ollama (optional local models)
- SSH Port Forwarding
- REST APIs

---

# 📦 Step 1 — Launch AWS EC2 Instance

1. Go to AWS Console → EC2
2. Launch Ubuntu 22.04 LTS
3. Instance type: m7i-flex.large (recommended)
4. Storage: 30 GiB
5. Allow SSH (Port 22)

After launch:

```bash
sudo apt update && sudo apt upgrade -y
````

---

# ⚙ Step 2 — Run Automated Setup

```bash
bash scripts/ec2-setup.sh
bash scripts/install-openclaw.sh
```

---

# 🌐 Step 3 — Access OpenClaw Web UI

```bash
ssh -i <pem-file> -N -L 18789:127.0.0.1:18789 ubuntu@<public-ip>
```

Open:

```
http://localhost:18789
```

---

# 🔑 Step 4 — Configure API Keys

Copy template:

```
examples/openclaw-config.example.json
```

Edit:

```
~/.openclaw/config.json
```

Add:

* OPENROUTER_API_KEY
* ELEVENLABS_API_KEY
* BRAVE_SEARCH_API_KEY
* ZAI_API_KEY

---

# 🤖 Step 5 — Telegram Bot Integration

1. Open Telegram
2. Search @BotFather
3. Create new bot
4. Get token
5. Run:

```bash
openclaw pairing approve telegram <bot-username>
```

---

# 🧠 Optional — Run Local Models with Ollama

```bash
ollama serve
ollama run llama3
```

---

# 🧹 Cleanup

Terminate EC2 instance to stop billing.

---

# 🎯 SEO Keywords (For Search Engines)

OpenClaw AWS EC2 setup
OpenClaw cloud deployment
Install OpenClaw on AWS
Deploy OpenClaw server
OpenClaw production setup
OpenClaw EC2 tutorial

---

# 📈 Why This Repository Ranks

* Exact keyword match in repository name
* Long-form documentation
* Technical depth
* Infrastructure automation
* High intent deployment search targeting

---

# ⭐ If this helped you, star the repo!

```

---

# 📊 Add GitHub Topics (IMPORTANT FOR VIRALITY)

After creating the repo, add these topics:

```

openclaw
aws
ec2
cloud
deployment
ai-agent
devops
automation
ubuntu-server
ollama

```

---

# 🏆 Viral Growth Strategy (Real Strategy)

To push this toward top search results:

1. Write a Medium article:
   “How to Deploy OpenClaw on AWS EC2 (Step-by-Step Guide)”
   Link to your repo.

2. Upload YouTube video:
   Title: “OpenClaw AWS EC2 Setup Tutorial”

3. Post on:
   - Reddit (r/devops, r/aws, r/selfhosted)
   - Dev.to
   - Hashnode

4. Add screenshots to README.
5. Add architecture diagram PNG.
6. Keep updating the repo.

Google ranks freshness + backlinks.

---

# 🔥 Next Level (Optional Upgrades)

If you want serious credibility:

- Add Docker support
- Add Terraform
- Add GitHub Actions CI
- Add Nginx reverse proxy
- Add HTTPS (Let's Encrypt)
- Add monitoring

---

# 🥇 Final Professional Setup

Repository Name:
```

openclaw-aws-ec2-setup

```

Visibility:
Public

Include:
- README
- Node .gitignore
- MIT License

---
# OpenClaw Setup Guide

A step-by-step guide to setting up [OpenClaw](https://openclaw.ai/) on an AWS EC2 instance.

---

## 1. Setup AWS EC2

1. Go to the [AWS Console](https://console.aws.amazon.com/) and navigate to **EC2**.
2. Launch a new instance with the following settings:

| Setting | Value |
|---|---|
| **Name** | openclaw_test |
| **OS** | Ubuntu |
| **Instance Type** | m7i-flex.large |
| **Key Pair** | openclaw_test_aiwithhassan.pem |
| **Storage** | 30 GiB |

> ⚠️ **Keep your .pem key file safe** — you'll need it to SSH into the instance.

3. Update the system packages:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## 2. Install OpenClaw

Website: [https://openclaw.ai/](https://openclaw.ai/)

**🐧 Linux / 🍎 Mac:**

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
source ~/.bashrc
```

**🪟 Windows (PowerShell as Administrator):**

```powershell
irm https://openclaw.ai/install.ps1 | iex
# Or using curl:
curl -fsSL https://openclaw.ai/install.sh | bash   # (via WSL)
```

> 💡 Press Ctrl + C to cancel if it starts running in the terminal after install.

---

## 3. Setup OpenRouter

1. Go to [OpenRouter](https://openrouter.ai/) and create an account.
2. Generate an **API key** from the dashboard.
3. Keep the key handy — you'll use it during OpenClaw onboarding.

---

## 4. Setup ElevenLabs

1. Go to [ElevenLabs](https://elevenlabs.io/) and create an account.
2. Generate an **API key** from the dashboard.

---

## 5. Onboard OpenClaw

Run the onboarding wizard to configure your OpenClaw instance:

**🐧 Linux / 🍎 Mac / 🪟 Windows:**

```bash
openclaw onboard
```

> This walks you through setting your name, AI persona, API keys, and preferences.

### Suggested First Message

Use something like this as your initial prompt to personalize OpenClaw:

> Hi, my name is **[Your Name]**. I am a **[Your Profession/Role]**. Your name is **[AI Name]**. I like to stay updated on **[Your Interests, e.g., AI, tech, finance]**. Our relationship vibe should be **[e.g., professional yet friendly]**. I think of you as my personal assistant who helps me stay organized, informed, and productive throughout the day. Add much information here as possible (DONT SHARE SECRET INFORMATION)

---

## 6. Setup Telegram Bot

### Install Telegram
- [Android (Google Play)](https://play.google.com/store/apps/details?id=org.telegram.messenger)
- [iOS (App Store)](https://apps.apple.com/app/telegram-messenger/id686449807)
- [Windows / Mac / Linux (Desktop)](https://desktop.telegram.org/)

### Create a Bot
1. Open Telegram and search for [@BotFather](https://t.me/BotFather).
2. Send `/start`, then `/newbot`.
3. Give your bot a **name** and a **username**.
4. Copy the bot token provided by BotFather.

### Connect Bot to OpenClaw

**🐧 Linux / 🍎 Mac / 🪟 Windows:**

```bash
openclaw pairing approve telegram <your-bot-username>
```

---

## 7. Setup Brave Search API

1. Go to [Brave Search API](https://brave.com/search/api/) and create an account.
2. Generate an API key and add it to your OpenClaw configuration.

---

## 8. Setup ZAI API

1. Go to the [ZAI API Portal](https://zai.com/) and generate an API key.

---

## 9. Connect to EC2

### Via SSH (Terminal)

**🐧 Linux / 🍎 Mac:**

```bash
# Set correct permissions on your key file
chmod 400 <path-to-pem-file>

# Connect to the instance
ssh -i <path-to-pem-file> ubuntu@<public-ip-of-ec2>
```

**🪟 Windows (PowerShell):**

```powershell
# Set correct permissions on your key file
icacls <path-to-pem-file> /inheritance:r /grant:r "%USERNAME%:R"

# Connect to the instance
ssh -i <path-to-pem-file> ubuntu@<public-ip-of-ec2>
```

**🪟 Windows (Command Prompt):**

```cmd
# Connect to the instance (use PuTTY or OpenSSH)
ssh -i <path-to-pem-file> ubuntu@<public-ip-of-ec2>
```

### Via Browser (Port Forwarding)

**🐧 Linux / 🍎 Mac:**

```bash
ssh -i <path-to-pem-file> -N -L 18789:127.0.0.1:18789 ubuntu@<public-ip-of-ec2>
```

**🪟 Windows (PowerShell / CMD):**

```powershell
ssh -i <path-to-pem-file> -N -L 18789:127.0.0.1:18789 ubuntu@<public-ip-of-ec2>
```

Then open `http://localhost:18789` in your browser.

---

## 10. OpenClaw Commands Reference

All commands work the same on **Linux**, **Mac**, and **Windows**.

| Command | Description |
|---|---|
| `openclaw onboard` | Run the onboarding/setup wizard |
| `openclaw tui` | Launch the terminal UI |
| `openclaw gateway` | Start the API gateway |
| `openclaw model configure` | Configure AI models |
| `openclaw skills` | Manage and view available skills |

### Run with Ollama (Local Models)

**🐧 Linux / 🍎 Mac:**

```bash
ollama serve
ollama run <model-name>
```

**🪟 Windows (PowerShell / CMD):**

```powershell
ollama serve
ollama run <model-name>
```

---

## 11. Uninstall OpenClaw

**🐧 Linux / 🍎 Mac:**

```bash
npm uninstall -g openclaw
```

**🪟 Windows (PowerShell / CMD):**

```powershell
npm uninstall -g openclaw
```

---

## 🙌 Shoutouts
A huge thanks to the amazing community and creators pushing the boundaries with OpenClaw!

### 🌟 Community Highlights
| Who | What They Built | Link |
|---|---|---|
| 🧠 OpenClaw Team | The core platform powering personal AI agents | [openclaw.ai](https://openclaw.ai/) |

### 🔗 Useful Resources
- 📖 [OpenClaw Documentation](https://openclaw.ai/docs)
- 💬 [OpenClaw Community / Discord](https://openclaw.ai/community)
- 🐦 [OpenClaw on Twitter/X](https://x.com/openclaw)
- 🌐 [Community Shoutouts Page](https://openclaw.ai/shoutouts)

---
> ⭐ **If you found this guide helpful, give it a star and share it with others!**


---





## 🤝 Connect & Support

<div align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/ashraf_morningstar)
[![Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://x.com/ams_morningstar)
[![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white)](https://instagram.com/ashraf_morningstar)
[![Discord](https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/ashraf_morningstar)
[![YouTube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtube.com/@ashraf_morningstar)

<br />

---


### ☕ Fuel My Work

[![BuyMeACoffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-ffdd00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/ashraf_morningstar)
[![PayPal](https://img.shields.io/badge/PayPal-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/ashraf_morningstar)
[![Patreon](https://img.shields.io/badge/Patreon-F96854?style=for-the-badge&logo=patreon&logoColor=white)](https://patreon.com/ashraf_morningstar)

</div>

<br />


---



### **"Transforming ideas into immersive 3D realities through code and creativity"**

⭐ **Star my repositories if you find them inspiring or useful!**  
🔄 **This README dynamically updates with my latest work**

<!-- Footer with 3D effect -->
<svg width="100%" height="60" xmlns="http://www.w3.org/2000/svg">
  <defs>
    <linearGradient id="footerGradient" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" style="stop-color:#3b82f6;stop-opacity:0.2" />
      <stop offset="50%" style="stop-color:#8b5cf6;stop-opacity:0.2" />
      <stop offset="100%" style="stop-color:#ec4899;stop-opacity:0.2" />
    </linearGradient>
  </defs>
  <rect width="100%" height="2" y="29" fill="url(#footerGradient)"/>
  <text x="50%" y="50%" text-anchor="middle" dy=".3em" font-family="'Segoe UI', Arial, sans-serif" font-size="14" fill="#94a3b8">
    Crafted with ❤️ using 3D elements • Last updated: December 2024
  </text>
</svg>

</div>

---

<!-- Visitor Counter with 3D Effect -->
<p align="center">
  <img src="https://komarev.com/ghpvc/?username=AshrafMorningstar&label=PROFILE+VIEWS&color=2c5364&style=flat-square" alt="Profile Views" />
</p>

</div>



---

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=100&section=footer&text=END%20OF%20LINE&fontSize=30&fontAlign=50&fontColor=ffffff" width="100%" />
  
  <p>© 2025 Ashraf Morningstar. The Code is the Law.</p>
</div>


<!--
  *** ASHRAF MORNINGSTAR // SYSTEM ROOT ***
  *** ARCHITECTURE: SINGULARITY_V3.0 ***
  *** STATUS: ONLINE ***
-->
