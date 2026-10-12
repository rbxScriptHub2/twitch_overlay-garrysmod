# Twitch Live Stream Overlay + AI Chat for Garry's Mod

**A Twitch-style live stream overlay for Garry's Mod, with an AI-powered chat that reacts to your gameplay.**

Turn your single-player game into a live streaming experience — with a chat sidebar, a streamer panel, viewer count, and AI viewers that talk to each other and to you.

---

## 📸 What It Does

- **Twitch-style overlay** on top of your game — the gameplay stays visible, the UI is drawn around it
- **Chat sidebar** on the right, just like real Twitch: colored nicknames, badges, dividers, header
- **AI viewers** — from 1 to 50 bots, each with its own personality and nickname
- **Live AI-generated messages** through OpenRouter (or any OpenAI-compatible API)
- **Bots grow over time** — new viewers gradually join your stream
- **Bots reply to each other and to you** — you can write in chat with `tv_send`
- **Streamer avatar** — taken from Steam by default, or your own picture
- **Multi-language** — English, Russian, Polish
- **VIP and MOD badges** displayed in chat

---

## ⚡ Quick Start (3 steps)

**Step 1.** Install the addon (see [Installation](#-installation)).

**Step 2.** Open the Garry's Mod console with the `~` key and paste your OpenRouter API key:
```
twitch_ai_apikey sk-or-v1-your-key-here
```
> Get a free API key at [openrouter.ai/keys](https://openrouter.ai/keys).

**Step 3.** Try it out:
```
twitch_ai_test
```
The chat on the right should fill up with AI-generated messages.

That's it — the overlay works.

---

## 📦 Installation

1. Download the addon folder `twitch_stream`.
2. Place it into your Garry's Mod `addons` folder:
   ```
   steamapps/common/GarrysMod/garrysmod/addons/twitch_stream/
   ```
3. Restart Garry's Mod.
4. Launch any map (single-player or sandbox).

The overlay appears automatically once you're in-game.

> **Do not move or rename files inside the folder** — the addon expects them exactly where they are.

---

## 🎮 Chat Commands

### Sending messages

| Command | What it does |
|---|---|
| `tv_send "your message"` | Write a message in chat as yourself. Bots may reply. |
| `twitch_sim_test_message` | Add a fake test message (to check if the chat works). |

### AI viewers

| Command | What it does |
|---|---|
| `twitch_ai_test` | Send a test request to all bots right now. |
| `twitch_ai_restart_agents` | Recreate all bots — new nicknames and badges. |
| `tv_max 15` | Set the maximum number of bots (1 to 50). |
| `twitch_ai_map_hint` | Check if the current map is recognized as something special. |

### Language

| Command | What it does |
|---|---|
| `twitch_lang en` | English (default) |
| `twitch_lang ru` | Russian |
| `twitch_lang pl` | Polish |

Changes **both the interface and the AI prompts**.

### Streamer (name and avatar)

| Command | What it does |
|---|---|
| `twitch_sim_streamer_info` | Show your current streamer name and avatar mode. |
| `twitch_sim_avatar_steam` | Use your Steam avatar. |
| `twitch_sim_avatar_file_mode` | Use a custom image from your `data` folder. |
| `twitch_sim_avatar_reset` | Reset everything back to Steam values. |

### Diagnostics (if something isn't working)

| Command | What it does |
|---|---|
| `twitch_sim_icons_check` | Check if all badge icons loaded correctly. |
| `twitch_sim_agents_dump` | List every bot and its badges. |
| `twitch_sim_force_badges` | Force VIP/MOD badges on the first three bots (for testing). |

---

## 🛠 Configuration (without a menu)

Every setting is a console variable (convars). You can change them by typing in the console. Your changes are saved automatically.

### Basics

| Setting | Default | Description |
|---|---|---|
| `twitch_sim_active` | `1` | Enable or disable the overlay (`1` = on, `0` = off) |
| `twitch_ai_enabled` | `1` | Enable or disable AI viewers |
| `twitch_ai_lang` | `en` | Language: `en`, `ru`, or `pl` |
| `twitch_ai_debug` | `0` | Show API errors in chat (`1` = on) |

### AI model and connection

| Setting | Default | Description |
|---|---|---|
| `twitch_ai_apikey` | *(empty)* | Your API key |
| `twitch_ai_model` | `openai/gpt-4o-mini` | The AI model to use |
| `twitch_ai_endpoint` | `https://openrouter.ai/api/v1/chat/completions` | API URL |
| `twitch_ai_temperature` | `1.25` | How creative the bots are (0.1 – 2.0) |
| `twitch_ai_max_tokens` | `80` | Maximum length of a single reply |

### AI viewers

| Setting | Default | Description |
|---|---|---|
| `twitch_ai_agents` | `3` | Starting number of bots |
| `twitch_ai_max_agents` | `8` | Maximum number of bots (up to 50) |
| `twitch_ai_grow_interval` | `45` | Seconds between new bots joining |
| `twitch_ai_interval` | `8` | Seconds between messages from one bot |
| `twitch_ai_memory` | `6` | How many recent messages bots remember |

### Streamer info

| Setting | Default | Description |
|---|---|---|
| `twitch_sim_streamer_name` | *(empty)* | Your display name (empty = Steam nickname) |
| `twitch_sim_avatar_mode` | `steam` | `steam`, `file`, `url`, or `none` |
| `twitch_sim_avatar_file` | `twitch_avatar.png` | Filename of a custom avatar |
| `twitch_sim_avatar_url` | *(empty)* | Direct link to an avatar image |
| `twitch_sim_category` | `Garry's Mod` | Stream category shown on the info panel |
| `twitch_sim_stream_title` | `Playing GMod` | Stream title shown on the info panel |

---

## 🌍 Supported AI Models

The addon works with **any OpenAI-compatible API**. Here are tested suggestions:

### OpenRouter (recommended — easy, works out of the box)

- `openai/gpt-4o-mini` — fast and cheap
- `openai/gpt-4o` — smarter
- `anthropic/claude-3.5-haiku` — softer, more natural
- `google/gemini-flash-1.5` — very cheap
- `meta-llama/llama-3.2-11b-vision-instruct:free` — **free**

To switch:
```
twitch_ai_model openai/gpt-4o
```

### Local models via Ollama

If you run [Ollama](https://ollama.com/) locally:

```
twitch_ai_endpoint http://127.0.0.1:11434/v1/chat/completions
twitch_ai_model llama3.2
twitch_ai_apikey none
```

---

## 👤 Custom Streamer Avatar

By default, the addon uses your **Steam avatar** and **Steam nickname**. You can override both.

### Use your own picture

1. Copy your image (square, PNG or JPG) to:
   ```
   steamapps/common/GarrysMod/garrysmod/data/twitch_avatar.png
   ```
   > The `data` folder is inside the same `garrysmod` folder as `addons`.

2. In the console:
   ```
   twitch_sim_avatar_mode file
   twitch_sim_avatar_file twitch_avatar.png
   ```

### Use a custom name

```
twitch_sim_streamer_name "Your Name"
```

Leave it empty to go back to your Steam nickname:
```
twitch_sim_streamer_name ""
```

### Go back to Steam avatar

```
twitch_sim_avatar_reset
```

---

## 🎨 Custom Badge Icons

You can replace the Twitch, VIP and MOD icons with your own. Put **three PNG files** into the folder:

```
addons/twitch_stream/materials/icons/
```

with these exact names:

| Filename | Recommended size | What it's for |
|---|---|---|
| `twitch.png` | 32×32 | Small Twitch logo in the header |
| `vip.png` | 18×18 | VIP badge shown in chat |
| `mod.png` | 18×18 | Moderator badge shown in chat |

**If a file is missing or broken** — a colored square with a letter (`V` / `M`) will be shown instead. Nothing will crash.

**After adding new icons**, restart Garry's Mod or type in console:
```
mat_reloadallmaterials
```

To verify the icons loaded:
```
twitch_sim_icons_check
```

You should see:
```
twitch.png error: false
vip.png    error: false
mod.png    error: false
```

If you see `true` — the file wasn't found or is in the wrong format.

---

## ⚡ Full Example Setup

Paste this into the console one line at a time:

```lua
// Your OpenRouter key
twitch_ai_apikey sk-or-v1-abc123...

// Russian interface
twitch_lang ru

// Custom streamer
twitch_sim_streamer_name "MyNickname"
twitch_sim_category "Garry's Mod"
twitch_sim_stream_title "Playing in the evening | !discord"

// More bots
tv_max 15

// Use a cheaper model
twitch_ai_model google/gemini-flash-1.5

// Test everything
twitch_ai_test
```

---

## 🐛 Troubleshooting

### Bots don't write anything

1. Check your API key:
   ```
   twitch_ai_apikey
   ```
   Should show your key. If empty — set it.

2. Turn on debug messages:
   ```
   twitch_ai_debug 1
   ```

3. Force a request:
   ```
   twitch_ai_test
   ```

4. Open the console (`~`) and look for errors — they'll start with `[TwitchAI]`.

### Icons don't appear

```
twitch_sim_icons_check
```

If any line says `error: true` — the file is missing or wrong. Check the folder:
```
addons/twitch_stream/materials/icons/
```

Then reload materials:
```
mat_reloadallmaterials
```

### VIP/MOD badges aren't showing

```
twitch_sim_agents_dump
```

This lists all bots with their badges. If everyone shows `(none)`, the random roll just didn't give any. Force them for testing:
```
twitch_sim_force_badges
```

### The model says "HTTP 402"

You're out of credits. Switch to a free model:
```
twitch_ai_model meta-llama/llama-3.2-11b-vision-instruct:free
```

### The model says "HTTP 429"

Too many requests — you hit a rate limit. Slow down:
```
twitch_ai_interval 15
```

### The overlay doesn't appear at all

```
twitch_sim_active 1
```

Then check the console for errors mentioning `cl_twitch_stream.lua`.

---

## 📋 Requirements

- **Garry's Mod** (any recent version)
- **An API key** from [OpenRouter](https://openrouter.ai/keys) (or any OpenAI-compatible provider)
- **Optional:** custom badge images (`twitch.png`, `vip.png`, `mod.png`) — the addon works without them

---

## 📄 License

MIT — see [`LICENSE`](LICENSE).

---

## 💡 Coming Later

- Real Twitch / YouTube chat integration
- Emotes in messages
- More badge types
- Bot personality presets

---

**Author:** your_github_username
**Version:** 1.0
