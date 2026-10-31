# Hermes Agent on Hostinger VPS

A personal AI assistant powered by **Hermes Agent**, **OpenAI**, and **Telegram**, deployed on a Hostinger VPS. The bot lets you interact with your AI assistant directly through Telegram.

## 🚀 Project Overview

This project sets up Hermes Agent on a Linux VPS and connects it to OpenAI for AI-powered responses and Telegram for messaging.

### Features

- 🤖 AI-powered conversations using OpenAI
- 💬 Telegram bot integration
- 🖥️ Linux VPS deployment on Hostinger
- 🔄 Background gateway service using systemd
- 🔐 Telegram user allowlist for access control
- ⚙️ Persistent service that can continue running after SSH disconnects

## 🛠️ Tech Stack

- **AI Agent:** Hermes Agent
- **LLM Provider:** OpenAI API
- **Messaging Platform:** Telegram Bot API
- **Server:** Hostinger VPS (Linux)
- **Service Management:** systemd
- **Remote Access:** SSH

## 🏗️ Architecture

```text
User
  |
  v
Telegram Bot
  |
  v
Hermes Agent Gateway
  |
  v
OpenAI API
  |
  v
AI Response
  |
  v
Telegram User
```

## ⚙️ Setup and Configuration

### 1. Connect to the VPS

Connect to your Hostinger VPS using SSH.

```bash
ssh root@YOUR_VPS_IP
```

Replace `YOUR_VPS_IP` with your VPS IP address.

### 2. Install Hermes Agent

Install Hermes Agent by following the official installation instructions:

https://hermes-agent.nousresearch.com/

Verify the installation:

```bash
hermes --help
```

### 3. Configure OpenAI

Configure Hermes to use your OpenAI API key and a supported model.

The standard OpenAI API base URL is:

```text
https://api.openai.com/v1
```

Verify the model configuration:

```bash
hermes config
```

**Security:** Keep your API key private. Never commit API keys or secret configuration files to GitHub.

### 4. Create a Telegram Bot

1. Open Telegram.
2. Search for `@BotFather`.
3. Create a bot using `/newbot`.
4. Copy the bot token and enter it directly into the Hermes setup on your VPS.
5. Obtain your personal Telegram user ID using `@userinfobot`.

Configure Telegram through:

```bash
hermes gateway setup
```

Use your personal numeric Telegram ID for the allowed-user list and home channel.

### 5. Start and Verify the Gateway

Check gateway status:

```bash
hermes gateway status
```

Restart the gateway when configuration changes require it:

```bash
hermes gateway restart
```

Check recent logs:

```bash
journalctl --user -u hermes-gateway.service -n 50 --no-pager
```

Follow logs live:

```bash
journalctl --user -u hermes-gateway.service -f
```

## 🧪 Testing

1. Open your Telegram bot.
2. Send `/start`.
3. Send a message such as:

```text
Hello! Are you working?
```

4. Confirm that the bot returns an AI-generated response.

## 🔐 Security Best Practices

- Never upload Telegram bot tokens or OpenAI API keys to GitHub.
- Restrict bot access using your Telegram user ID.
- Keep secret files out of version control.
- Use a strong SSH authentication method.
- Keep the VPS operating system and software updated.

Before pushing files to GitHub, check that `.env`, private keys, and other secret files are excluded.

Example `.gitignore` entries:

```gitignore
.env
.env.*
!.env.example
*.pem
*.key
__pycache__/
.venv/
venv/
```

Review the files before committing to ensure no credentials are included.

## 🖥️ Deployment

Hermes runs as a background systemd user service on the VPS. This allows the gateway to continue running after you disconnect from SSH, provided the service remains healthy and the VPS is online.

Useful commands:

```bash
hermes gateway status
hermes gateway restart
hermes gateway setup
```

## 📚 Resources

- Hermes Agent: https://hermes-agent.nousresearch.com/
- OpenAI API: https://platform.openai.com/
- Telegram Bot API: https://core.telegram.org/bots/api
- Hostinger VPS: https://www.hostinger.com/vps-hosting

## ✅ Project Status

**Completed:** Hermes Agent installed, OpenAI responses tested, Telegram bot connected, and the gateway configured as a background service.

## 👨‍💻 Author

Created as a personal AI assistant deployment project using open-source agent tooling, OpenAI, Telegram, and Hostinger VPS.
