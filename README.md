# BetterPrivacy

A client-side, purely visual privacy toolkit for Discord, built as a [Vencord](https://vencord.dev/) userplugin.

BetterPrivacy blurs, hides, or locks the parts of Discord that can identify you or the people you talk to — profiles, messages, servers, and DMs — entirely on your own machine. It never talks to a server, never changes what Discord itself receives, and doesn't collect any data or telemetry.

> **Heads up:** this is purely a visual layer on top of Discord's normal UI. It does not encrypt messages, protect against external screen-recording/screenshot tools, secure your account, or stop Discord's servers from receiving anything. It only changes what *you* see rendered on your own screen.

---

## Features

### Privacy modes
- **Normal** — nothing hidden unless you've turned a category on
- **Screenshot Mode** — slightly stronger blur, good for a quick screenshot
- **Streamer Mode** — stronger still, for streaming/screensharing
- **Maximum Privacy** — blurs everything at once
- **Custom** — just use your own toggles below, no extra intensity applied

### Panic hotkey
`Ctrl+Shift+P` instantly jumps to a privacy mode of your choice and switches to the Friends tab. Press it again to return to *exactly* whatever mode/settings you were using before — it never overwrites your saved configuration. Works even when Discord isn't the focused window.

### What you can hide or blur
- Display names, usernames, avatars, badges, bio, join/friend-since dates
- Mutual friends and mutual servers (independently)
- Message content
- The member list sidebar
- Server names (including the hover tooltip) and server icons

### Per-user & per-server "always hide"
Right-click any user for a submenu with independent checkboxes: **Hide Avatar**, **Hide Username**, **Hide Messages**. This protection is permanent and applies wherever that person shows up, regardless of your general category settings.

Right-click a server icon for **Always Hide Server**, which works the same way.

Manage everyone/everything you've protected from **Settings → BetterPrivacy → Manage permanently protected users/servers**, with a Remove button for each.

### PIN-protected locking
- Set a PIN under **Settings → BetterPrivacy** (hashed locally with SHA-256 + a random salt — the PIN itself is never stored or transmitted anywhere)
- Right-click a **server** → Lock This Server (locks every channel inside it)
- Right-click a **channel** → Lock This Channel
- Right-click a **person in a DM** → Lock This Chat (works for both 1:1 and group DMs)

When you open something locked, a blurred silhouette overlay covers it — you can see shapes/colors behind it but can't click or type into anything until the correct PIN is entered. Unlocking is per-session: it re-locks the next time Discord restarts.

### Zero-flash design
Protection is applied via CSS the instant an element exists, not scanned and patched afterward — so there's no brief flash of unprotected content before blur kicks in.

---

## Installation

This is a **userplugin** for Vencord, which means you need a local Vencord development setup (not just the regular installer) to use it.

1. Clone Vencord if you haven't already:
   ```bash
   git clone https://github.com/Vendicated/Vencord
   cd Vencord
   pnpm install
   ```

2. Copy this plugin folder into your userplugins directory:
   ```bash
   mkdir -p src/userplugins
   cp -r betterPrivacy src/userplugins/betterPrivacy
   ```

   Your folder structure should look like:
   ```
   Vencord/
   └── src/
       └── userplugins/
           └── betterPrivacy/
               ├── index.tsx
               ├── native.ts
               └── styles.css
   ```

3. Build and inject:
   ```bash
   pnpm build
   pnpm inject
   ```

4. **Fully quit Discord** from the tray icon (not just close the window), then reopen it.

5. Go to **Discord Settings → Vencord → Plugins**, find **BetterPrivacy**, and toggle it on.

### Updating the plugin
Whenever you get a new version of these files, replace them in `src/userplugins/betterPrivacy/`, then repeat steps 3–4 (`pnpm build`, `pnpm inject`, fully restart Discord).

---

## Configuration

All settings live under **Discord Settings → Vencord → Plugins → BetterPrivacy** (click the plugin name, not just the toggle, to open its settings).

| Section | What's there |
|---|---|
| **General** | Master on/off switch, protection method (blur/pixelate/hide), blur strength |
| **Profile / Message / Server toggles** | Individual category switches |
| **Security** | PIN setup, panic hotkey settings |
| **Manage** | List/remove permanently protected users and servers |

---

## Limitations

- This is a visual-only tool. It cannot protect against screen recording software, physical shoulder-surfing, or anything happening outside Discord's own rendering.
- Some selectors are matched against Discord's internal DOM structure, which can occasionally change after a Discord update and stop matching. If something stops blurring after a Discord update, that's usually why.
- Vencord itself is an unofficial client modification and sits outside Discord's Terms of Service. Enforcement has historically been lax, but this isn't a guarantee.
- This is a early version, not the final build. You may encounter bugs, or elements that arent hidden. If you do find anything please open a ticket on our Discord server.

---

## Support / Issues

If something isn't working or you run into a bug, come find us in the support Discord:

**[discord.gg/c4C8qEucja](https://discord.gg/c4C8qEucja)**
