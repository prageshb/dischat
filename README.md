# Discord Live Chat Bot

## Overview

A modular, privacy-focused Discord bot for anonymous 1-on-1 and group chat (text and voice), with advanced moderation, per-guild configuration, and robust error handling. Built with TypeScript, discord.js, and MongoDB for scalability and reliability.

- **Anonymous chat**: 1-on-1 and group, text and voice
- **Queue-based matching**: FIFO, 7-day repeat protection
- **Per-guild configuration**: All channels and settings are set via slash commands
- **Advanced moderation**: Keyword filters, infractions, chat flagging, mod logging
- **Anti-spam**: Voice join spam protection, timeouts
- **Privacy**: Threads and channels deleted after sessions; flagged chats preserved for review
- **Scalable**: MongoDB backend, sharding-ready

---

## Quick Start

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Discord-Live-Chat
   ```
2. **Install dependencies**
   ```bash
   npm install
   ```
3. **Configure environment**
   ```bash
   cp env.example .env
   # Edit .env with your Discord bot configuration
   ```
4. **Run the bot**
   ```bash
   npm run dev    # Development
   npm start      # Production
   ```

---

## Features

- Anonymous 1-on-1 and group chat (text & voice)
- Queue-based matching (FIFO, 7-day repeat protection)
- Moderation: keyword filters, infractions, chat flagging, mod logging
- Anti-spam: voice join spam protection, timeouts
- Per-guild configuration (all channels set via slash commands)
- Ephemeral threads and voice channels
- Admin and super admin commands
- Scalable MongoDB backend
- Robust error handling and logging

---

## Per-Guild Setup & Configuration

All required channels and categories must be set **per guild** using slash commands:

- `/setlobby <channel>` — Set the lobby channel for queue buttons
- `/setchatchannel <channel>` — Set the chat channel for threads
- `/setmodchannel <channel>` — Set the moderation channel for admin notifications
- `/setvoicecategory <category>` — Set the voice category for voice channels
- `/setvoicelobby <channel>` — Set the required voice lobby channel for voice queues

**Note:** Users cannot join any queue until all required channels are configured. The bot will show an error if any are missing.

---

## Admin Commands

- `/admin stats` — View bot statistics
- `/admin inf add <user> <type> <reason>` — Add infraction
- `/admin inf list <user>` — List user infractions
- `/admin inf delete <user>` — Delete latest infraction
- `/admin active` — View active sessions
- `/admin wait` — View queue status
- `/setlobby`, `/setchatchannel`, `/setmodchannel`, `/setvoicecategory`, `/setvoicelobby` — Per-guild setup (admin only)

## Super Admin Commands

- `/addguild <guild_id>` — Allow a guild to use the bot (super admin only)
- `/removeguild <guild_id>` — Remove a guild from the allowlist (super admin only)
- `/delbot <guild_id>` — Delete all data for a guild (super admin only)
- `/listguilds` — List all allowed guilds (super admin only)

---

## Environment Variables

See `env.example` for all options. Key variables:
- `DISCORD_TOKEN` — Your Discord bot token
- `DISCORD_CLIENT_ID` — Your Discord application client ID
- `MONGO_URI` — MongoDB connection string
- `SUPER_ADMIN_ID` — Discord user ID of the super admin

---

## Channel Structure Example

```
📁 Your Discord Server
├── 📝 #lobby (lobbyChannelId)
│   └── Queue buttons
├── 💬 #chat-sessions (chatChannelId)
│   ├── 🧵 Private Chat - 2 users
│   ├── 🧵 Group Chat - 4 users
│   └── (threads created here)
├── 🛡️ #moderation (modChannelId)
│   └── Admin notifications and flagged content
└── 📁 Voice Channels (voiceCategoryId)
    ├── 🎤 Voice Chat - match_id_1
    └── 🎤 Group Voice - match_id_2
```

---

## Scalability & Sharding

- **Single instance**: Up to 2,500 guilds (Discord's limit)
- **With sharding**: 10,000+ guilds (see discord.js sharding docs)
- **Concurrent users**: 1,000–5,000 per instance is typical; scale horizontally for more
- **MongoDB**: Use a managed cluster (e.g., Atlas) for high concurrency

---

## Privacy & Data Retention

- **Anonymous chats**: No user IDs in chat sessions
- **Ephemeral data**: Threads and voice channels deleted after sessions
- **Flagged chats**: Only flagged sessions are preserved for moderation
- **Per-guild data**: All user/match/infraction data is per-guild

---

## Error Handling & Troubleshooting

- **Comprehensive error handling**: All Discord API and DB calls are wrapped in try/catch
- **Single reply per interaction**: Prevents Discord.js reply errors
- **Clear user feedback**: All errors are shown to users/admins
- **Debug logging**: Enable with `DEBUG=true` in `.env`

See [ERROR_HANDLING.md](ERROR_HANDLING.md) for details.

---

## Development & Contribution

- See [SETUP.md](SETUP.md) for setup instructions
- See [ERROR_HANDLING.md](ERROR_HANDLING.md) for error handling details
- Fork, branch, and PR as usual

---

## License

MIT License. See LICENSE file. 