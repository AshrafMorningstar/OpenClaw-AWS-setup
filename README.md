# OpenClaw Setup Guide

A concise, step-by-step README to create and configure `setup-openclaw` — a repo containing scripts, docs, and automation for installing and running OpenClaw on an AWS EC2 instance.

> 🎬OpenClaw AI Agent: The Ultimate AWS EC2 Deployment Guide
>

---

## Table of Contents

1. [Overview](#overview)
2. [Prerequisites](#prerequisites)
3. [AWS EC2 Setup](#aws-ec2-setup)
4. [Install OpenClaw](#install-openclaw)
5. [Configure OpenRouter & Voices](#configure-openrouter--voices)
6. [Onboard OpenClaw](#onboard-openclaw)
7. [Telegram Bot Integration](#telegram-bot-integration)
8. [Brave Search & ZAI APIs](#brave-search--zai-apis)
9. [Connect to EC2 (SSH / Port Forwarding)](#connect-to-ec2-ssh--port-forwarding)
10. [OpenClaw Command Reference](#openclaw-command-reference)
11. [Uninstall / Cleanup](#uninstall--cleanup)
12. [Resources & Links](#resources--links)
13. [Contributing & License](#contributing--license)

---

## Overview

This repository (`setup-openclaw`) houses the documentation, scripts, and example configurations to quickly spin up an OpenClaw instance on EC2, connect model & TTS providers, and pair messaging integrations (Telegram). Use it as a base for automations, infra-as-code, or educational demos.

---

## Prerequisites

* A working account with AWS.
* Basic Linux command-line knowledge (SSH, `chmod`, `curl`).
* API keys for any third-party services you plan to use (OpenRouter, ElevenLabs, Brave Search, ZAI).
* (Optional) `ssh` / `scp` client on your workstation.

---

## AWS EC2 Setup

1. Open the AWS Console → **EC2** → Launch instance.
2. Recommended instance settings:

| Setting           | Value                                             |
| ----------------- | ------------------------------------------------- |
| **Name**          | `openclaw_test`                                   |
| **OS**            | Ubuntu 22.04 LTS (or similar LTS)                 |
| **Instance Type** | `m7i-flex.large` (or GPU/CPU variant you prefer)  |
| **Key Pair**      | `openclaw_test_aiwithhassan.pem` (store securely) |
| **Storage**       | `30 GiB` (adjust to model/data needs)             |

3. Security group: allow SSH (22) and the OpenClaw local port (default `18789`) only from trusted IPs.
4. Update instance packages after launch:

```bash
sudo apt update && sudo apt upgrade -y
```

> ⚠️ Keep your `.pem` key secure — losing it prevents SSH access.

---

## Install OpenClaw

Official site: `https://openclaw.ai/`

**Linux / macOS:**

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
source ~/.bashrc
```

**Windows (PowerShell as Admin, or via WSL):**

```powershell
irm https://openclaw.ai/install.ps1 | iex
# or using WSL:
curl -fsSL https://openclaw.ai/install.sh | bash
```

Verify install:

```bash
openclaw --help
```

---

## Configure OpenRouter & Voices

1. Create an account at OpenRouter and generate an API key.
2. Create an account at ElevenLabs and generate a TTS API key.
3. Add keys to OpenClaw config during onboarding or by editing `~/.openclaw/config.json` (or the file the onboarding creates).

---

## Onboard OpenClaw

Run the onboarding wizard:

```bash
openclaw onboard
```

The wizard will prompt for:

* User name and default assistant persona
* API keys (OpenRouter, ElevenLabs, Brave, ZAI)
* Preferences and defaults

**Suggested first message (example):**

> Hi, my name is **[Your Name]**. I am a **[Your Profession]**. Your assistant name is **[AI Name]**. I like updates on **[topics]**. Tone: **[professional/friendly/etc.]**.
> *(Do not share secret credentials in prompts.)*

---

## Telegram Bot Integration

1. Install Telegram on your device/desktop.
2. Create a bot via `@BotFather` in Telegram: `/newbot` → name & username → copy the bot token.
3. Pair with OpenClaw:

```bash
openclaw pairing approve telegram <your-bot-username>
# or use pairing command shown by `openclaw onboard`
```

---

## Brave Search & ZAI APIs

* Brave Search API: sign up and generate an API key; add it to OpenClaw config. (See Brave docs.)
* ZAI API: sign up and generate an API key; add it to OpenClaw config.

(Replace placeholders in config with the real keys — store secrets securely.)

---

## Connect to EC2 (SSH / Port Forwarding)

**Linux / macOS:**

```bash
chmod 400 <path-to-pem-file>
ssh -i <path-to-pem-file> ubuntu@<ec2-public-ip>
# For port forwarding (local browser to remote OpenClaw UI)
ssh -i <pem> -N -L 18789:127.0.0.1:18789 ubuntu@<ec2-public-ip>
# Then open http://localhost:18789
```

**Windows (PowerShell):**

```powershell
icacls <path-to-pem-file> /inheritance:r /grant:r "%USERNAME%:R"
ssh -i <path-to-pem-file> ubuntu@<ec2-public-ip>
```

---

## OpenClaw Command Reference

| Command                    | Purpose                       |
| -------------------------- | ----------------------------- |
| `openclaw onboard`         | Run setup wizard              |
| `openclaw tui`             | Launch terminal UI            |
| `openclaw gateway`         | Start API gateway             |
| `openclaw model configure` | Configure/backends for models |
| `openclaw skills`          | List/manage skills            |

### Run with local models (Ollama)

To run local models:

```bash
# start ollama server
ollama serve
# run a model
ollama run <model-name>
```

(Replace `<model-name>` with the model you have locally.)
*Tip:* `ollama` is useful for self-hosted experiments or offline demos.

---

## Uninstall / Cleanup

**Uninstall OpenClaw:**

```bash
npm uninstall -g openclaw
```

**Terminate EC2 instance** from the AWS Console to stop billing. Revoke/delete any API keys no longer needed.

---

## Resources & Links

* OpenClaw — Official docs & downloads.
* AI With Hassan — video walkthrough.
* OpenRouter — model routing & API keys.
* ElevenLabs — TTS/voice API.
* AWS — EC2 infra.
* Brave Search API — add to OpenClaw for search results.
* ZAI API — optional model/feature provider.

---

## Example repo layout

```
setup-openclaw/
├─ docs/
│  └─ README.md          # this document
├─ scripts/
│  ├─ ec2-setup.sh       # optional automation for EC2 provisioning
│  └─ install-openclaw.sh
├─ examples/
│  └─ openclaw-config.example.json
├─ .gitignore
└─ LICENSE
```

---

## Contributing

1. Fork the repo.
2. Create a feature branch `feat/<short-desc>`.
3. Open a PR with a clear description and test steps.
4. Keep secrets out of commits — use environment variables or CI secrets.

---

## License

Include an appropriate license file (MIT / Apache-2.0 / etc.). Add `LICENSE` to the repo root. If unsure, `MIT` is permissive and commonly used.

---
