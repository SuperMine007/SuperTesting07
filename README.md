<p align="center">
  <img src="https://media.forgecdn.net/avatars/434/180/637659424855078519.png" width="128" height="128" alt="Minecraft Icon"/>
</p>

<h1 align="center">Ultimate Minecraft Server Actions</h1>

<p align="center">
  <strong>A fully automated, free 24/7-style Minecraft server powered entirely by GitHub Actions, featuring Google Drive automatic backups, Bedrock crossplay, and Discord integration!</strong>
</p>

---

## ✨ Features

- **✅ 100% Free Hosting**: Powered completely by GitHub Actions' free runner tier.
- **✅ 24/7 Auto-Restarts**: The server runs a continuous loop. Every 5.5 hours it restarts itself automatically, creating a near 24/7 experience.
- **✅ Cross-Platform Play**: Java & Bedrock editions play together seamlessly (via Geyser).
- **✅ Auto-Backups**: Every 5.5 hours, your world saves and zips itself straight into Google Drive.
- **✅ High Performance**: Runs on a 4-Core CPU, 16GB RAM runner with 6GB dedicated to the Java heap. 
- **✅ Automated Tunnels**: Instantly generates IP addresses using [Playit.gg](https://playit.gg) without any port forwarding.
- **✅ Discord Integration**: Streams live server console and chat directly to your Discord server via DiscordSRV.
- **✅ Lag-Proof Kick Prevention**: Custom variables (`allow-flight=true`) enabled so high-ping players never get dropped for "flying".

---

## 🛠️ Server Specifications (The Runner)

When you click "Run", GitHub gives your server a temporary virtual machine with the following specs:
*   **Operating System:** Ubuntu Linux (Latest)
*   **CPU:** 4-Core Intel/AMD Processor
*   **RAM:** 16 GB Total (We strictly allocate **6 GB** to Minecraft itself for optimal performance without crashing the runner)
*   **Storage:** 14GB+ High-Speed SSD 
*   **Network:** GitHub's ultra-fast datacenter gigabit internet

> **Note:** GitHub Actions runners have a hard limit of 6 hours. This script runs your server for **5.5 hours**, gives your players a 30-minute and 1-minute warning, safely shuts down, backs up to Google Drive, and then automatically restarts itself for another session!

---

## 🚀 Setup Guide (For Absolute Beginners)

Follow these steps exactly to set up your own server in 10 minutes.

### Step 1: Create the Repository
1. Go to your GitHub Homepage.
2. Click the `+` icon in the top right -> `New repository`.
3. Name it whatever you like (e.g., `SuperSMP-Server`).
4. ⚠️ **CRITICAL:** Set Visibility to **"PUBLIC"**. If it is Private, your Action minutes are limited to 2,000 per month. Public repositories get *unlimited* free minutes!
5. Click `Create repository`.

### Step 2: Install the Script
1. Inside your new repository, click `Add file` -> `Create new file`.
2. In the filename box at the top, type exactly: **`.github/workflows/main.yml`**
3. Paste the provided workflow code into the large text box.
4. Click the green `Commit changes` button.

### Step 3: Prepare the "Plugins" Folder
GitHub does not allow empty folders. We need to create a placeholder so we can upload plugins later!
1. Go back to your repo homepage.
2. Click `Add file` -> `Create new file`.
3. In the filename box, type exactly: **`plugins/placeholder.txt`** 
   *(Typing the slash `/` automatically generates the folder!)*
4. Type anything in the text box (like "folder created").
5. Click `Commit changes`.
6. You can now click `Add file` -> `Upload files` while inside the `plugins/` folder to upload `.jar` files (like Geyser, AuthMe, ViaVersion, etc). 

---

## 🔑 Secret Keys Configuration 

To make the server work, you need to provide it with "Secrets" (hidden private passwords).
Go to your Repository **Settings -> Secrets and variables -> Actions -> New repository secret**.

You need to add these secret keys:

### 1. PLAYIT_SECRET (Connects players to the server)
1. Go to [Playit.gg](https://playit.gg) & log in.
2. Go to **Dashboard -> Agents -> Add Agent** (or create a new GitHub Server agent).
3. Copy the long random "Secret Key".
4. Add it as a repository secret named `PLAYIT_SECRET`.

### 2. DISCORD_TOKEN (For server chat and console logs)
1. Go to the [Discord Developer Portal](https://discord.com/developers/applications).
2. Create Application -> Go to the "Bot" tab.
3. Click `Reset Token` and copy the token.
4. **Important**: Scroll down on that page and turn ON the **"Message Content Intent"** toggle.
5. Add it as a repository secret named `DISCORD_TOKEN`.
   *(Don't forget to edit the workflow `.yml` file and change the `145437...` numbers to your actual Discord Channel IDs if you use DiscordSRV!)*

### 3. SEED (Optional)
*   **Name:** `SEED`
*   **Value:** Type any seed you want (e.g., `-123456789`). This only works on a brand new world before a backup is created.

### 4. END_PORTAL (Optional)
*   **Name:** `END_PORTAL`
*   **Value:** `true` or `false` (Controls whether the End dimension is generated/accessible).

---

## 💾 Setting Up Google Drive Backups (GDRIVE_CONFIG)

This server requires a connection to your Google Drive so it doesn't delete your world when it turns off! You can generate this secret key using only an Android phone (via the Termux app).

**Step A: Get the App**
1. Download **Termux** from the [F-Droid store](https://f-droid.org/) (Do NOT use Google Play, that version is broken).
2. Open Termux and type: `pkg update && pkg upgrade -y`
3. Type: `pkg install rclone -y`

**Step B: Link the Account**
1. Type: `rclone config`
2. Type `n` (New remote) and name it exactly **`gdrive`**.
3. It will show a massive list of cloud providers. Look for "Google Drive" (usually number `18` or `19`) and type that number.
4. Leave `client_id` **BLANK** (Press Enter).
5. Leave `client_secret` **BLANK** (Press Enter).
6. For scope, type `1` (Full access).
7. Leave `root_folder_id` and `service_account_file` **BLANK**.
8. "Edit advanced config?" Type `n` (No).
9. "Use web browser to authenticate?" Type `y` (Yes).
10. It will give you a link starting with `http://127.0.0.1:53682/auth`. Copy it and open it in Chrome.
11. Log into your Google account and click **Allow**. 
12. Back in Termux, it asks "Configure as Shared Drive?" Type `n` (No). Type `y` (Yes) when it asks if the config is okay. Then type `q` to quit.

**Step C: Copy the Key to GitHub**
1. In Termux, type: `cat ~/.config/rclone/rclone.conf`
2. A block of text starting with `[gdrive]` will appear. **Copy ALL of it.**
3. Paste that massive block of text into GitHub as a new secret named `GDRIVE_CONFIG`.

**Step D: Make the Folder**
Go to your Google Drive and create a brand new folder named exactly **`MinecraftServer`**. The auto-backups will drop inside this folder!

---

## 🎮 How to Play!

1. Go to the **"Actions"** tab on your GitHub repository.
2. Select "Ultimate Minecraft Server" on the left menu.
3. Click the `Run workflow` button!
4. Wait 2-3 minutes.

To get the IP Address, go to your [Playit.gg Dashboard](https://playit.gg) -> Click your Agent -> **Add Tunnels**.

*   **For Java Players:** Add a `Minecraft Java` tunnel. It will give you a linking domain (like `word.joinmc.link`).
*   **For Bedrock Players:** Add a `Minecraft Bedrock` tunnel. It will give you an IP (`word.ply.gg`) and a 5-digit Port. Use these in the "Add Server" menu in Minecraft Bedrock!
