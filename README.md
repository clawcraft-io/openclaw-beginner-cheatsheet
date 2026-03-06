# OpenClaw Beginner Cheatsheet

> The guide I wish I had when starting.

**Part of [ClawCraft](https://clawcraft.substack.com) - Building OpenClaw skills in public.**

---

## 🚀 Quick Start (5 Minutes)

```bash
# 1. Install OpenClaw
npm i -g openclaw

# 2. Check installation
openclaw --version

# 3. Start the Gateway
sudo openclaw gateway start

# 4. Verify it's running
openclaw status
AutoClawSkills, [3/2/2026 10:55 PM]

Expected output: Gateway: running ✅

───

💰 Real Cost Breakdown

| Item            | Monthly | Notes                       |
| --------------- | ------- | --------------------------- |
| VPS (Hostinger) | ~$5     | Cheapest plan works fine    |
| API Usage       | ~$10-30 | Depends on model & usage    |
| Total           | ~$15-35 | Less than a coffee per week |

Startup cost: ~$25 (VPS + initial API credits)

───

🤖 Model Selection Guide

| Model       | Best For              | Cost | When to Use                              |
| ----------- | --------------------- | ---- | ---------------------------------------- |
| Kimi K2.5   | Learning, general use | $    | Just starting, good balance              |
| GPT-4o      | Coding, complex tasks | $$$  | Professional code, budget less important |
| Claude 3.5  | Analysis, writing     | $$   | Long documents, nuanced tasks            |
| GPT-3.5     | Simple Q&A            | $    | Already working, quick answers           |
| Local Llama | Privacy, free         | FREE | Tech-savvy, have good computer           |

Recommendation: Start with Kimi K2.5 (~$0.50-2 per session)

───

📱 Channel Setup

Telegram (Easiest)

# 1. Message @BotFather on Telegram
# 2. Create new bot → Get token
# 3. Configure OpenClaw:
openclaw configure --section telegram
# 4. Enter token when prompted
# 5. Message your bot to test!

Discord

# 1. Go to discord.com/developers/applications
# 2. New Application → Bot → Get token
# 3. Enable MESSAGE CONTENT INTENT (important!)
# 4. Configure:
openclaw configure --section discord

───

❌ Common Mistakes (And Fixes)

"Gateway not running"

# Fix:
sudo openclaw gateway start

# Or check status:
openclaw gateway status

"Permission denied"

# Gateway needs sudo:
sudo openclaw gateway start

"Model API errors"

# Check your API key has credits:
openclaw configure --section moonshot  # or openai/anthropic

"Bot not responding"

• Telegram: Did you message the bot FIRST? Bots can't initiate
• Discord: Is the bot invited to your server? (Not just created)

"Port 8080 in use"

# Check what's using it:
sudo lsof -i :8080

# Or change OpenClaw port in config:
~/.openclaw/openclaw.json

───

📚 Free Resources

| Resource             | Link                   | Description                    |
| -------------------- | ---------------------- | ------------------------------ |
| This Cheatsheet      | You're here!           | Quick reference                |
| ClawCraft Newsletter | clawcraft.substack.com | Weekly updates, deep dives     |
| Twitter              | @clawcraft_io          | Daily tips, building in public |
| Setup Wizard         | Coming Mar 15          | Complete guided setup          |

───

🛠️ What's Next?

I'm building tools to make OpenClaw easier:

Launching March 15 on ClawHub (https://clawhub.com/):

| Skill                 | Price  | What It Does                                 |
| --------------------- | ------ | -------------------------------------------- |
| learning-companion    | $5-10  | Helps AI assistants teach OpenClaw concepts  |
| openclaw-setup-wizard | $20-25 | Complete setup with Hostinger-specific steps |
| clawhub-scanner       | $15-20 | Find skill gaps and market opportunities     |

Why paid?

• Save you 2-3 hours of confusion
• Hostinger-specific (not generic)
• Model selection guide included
• Troubleshooting help

───

🤝 Contributing

Found a mistake? Want to add something?

1. Fork this repo
2. Make your changes
3. Submit a pull request

Or just open an issue (https://github.com/clawcraft-io/openclaw-beginner-cheatsheet/issues).

───

📬 Stay Updated

• Newsletter: clawcraft.substack.com (https://clawcraft.substack.com/)
• Twitter: @clawcraft_io (https://twitter.com/clawcraft_io)
• New skills: Launching March 15 🚀

───

📝 License

MIT License - Use freely, give credit if you want.

───

Built with 💙 by Daham (https://twitter.com/clawcraft_io) as part of ClawCraft (https://clawcraft.substack.com/).

---

## 🚨 Common Issues & Fixes

### "Gateway keeps stopping"

**Why:** VPS resource limits, memory pressure, or auto-restart loops

**Fix:**
```bash
# Check resources
free -h
df -h

# Monitor with auto-restart
# Install vps-monitor skill for automatic alerts

Prevention:

• Use VPS with 2GB+ RAM
• Monitor disk space (keep 20% free)
• Set up alerts with vps-monitor skill

───

"False alerts every 5 minutes"

Why: Gateway briefly restarts during checks, monitor too sensitive

Fix - Increase interval:
crontab -e
# Change */5 to */30 (every 30 min instead of 5)
*/30 * * * * /opt/vps-monitor/check-health.sh

Fix - Add cooldown:
Add to monitor script to only alert once per hour.

───

"Can't connect to Gateway"

Symptoms: "Connection refused", commands timeout

Check:
openclaw gateway status
sudo lsof -i :8080
sudo ufw status

Fixes:
# Restart Gateway
sudo openclaw gateway start

# Open firewall port
sudo ufw allow 8080/tcp

───

"Model API errors"

Symptoms: "Invalid API key", "Rate limit exceeded"

Fixes:

• Add credits to API account
• Switch to cheaper model (Kimi vs GPT-4)
• Check model name spelling

───

💰 Cost Optimization

Reduce API Costs

Use cheaper models:

• Kimi K2.5: ~$0.50-2/session (learning)
• GPT-3.5: ~$0.10-0.50/session (simple tasks)
• GPT-4o: ~$3-8/session (only for complex code)

Reduce VPS Costs

Start small:

• 1GB RAM VPS: $3-5/month (minimum)
• Use swap space instead of more RAM

───

🔒 Security Best Practices

Basic VPS Hardening
# Update system
sudo apt update && sudo apt upgrade -y

# Create non-root user
sudo adduser yourname
sudo usermod -aG sudo yourname

# Enable firewall
sudo ufw allow 22/tcp
sudo ufw allow 8080/tcp
sudo ufw enable

───

🔄 Best Practices for 24/7 Uptime

Use Systemd Service

Create /etc/systemd/system/openclaw-gateway.service:
[Unit]
Description=OpenClaw Gateway
After=network.target

[Service]
Type=simple
User=root
ExecStart=/usr/local/bin/openclaw gateway start
Restart=always
RestartSec=10

[Install]
WantedBy=multi-user.target

Enable:
sudo systemctl enable openclaw-gateway
sudo systemctl start openclaw-gateway

Regular Backups
# Backup your workspace
tar -czf backup-$(date +%Y%m%d).tar.gz ~/.openclaw/

───

🆘 Getting Help

When stuck:

1. Check docs: https://docs.openclaw.ai (https://docs.openclaw.ai/)
2. Search issues: github.com/openclaw/openclaw/issues (http://github.com/openclaw/openclaw/issues)
3. Ask community:
  • OpenClaw Discord: https://discord.com/invite/clawd
  • r/selfhosted (for VPS questions)

Debug steps:
openclaw status
openclaw gateway logs --tail 50
openclaw doctor

───

Want the complete guided setup? Check out my openclaw-setup-wizard skill on ClawHub (https://clawhub.com/) - launching March 15 🚀


Last updated: March 2026
