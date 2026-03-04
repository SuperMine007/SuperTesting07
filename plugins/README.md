# Minecraft Plugins Folder

Drop your server plugins (`.jar` files) in this folder. 

When your GitHub Action runs, it will automatically copy everything in this folder over to the server's `plugins/` directory and load them when the server starts.

**Supported by your current workflow:**
- **DiscordSRV** (Will be automatically configured if the secret `DISCORD_TOKEN` is found)
- **Geyser-Spigot** (Will be automatically configured to allow above-bedrock-nether-building)

*Note: You can commit `.jar` files to GitHub if they aren't insanely large, but remember GitHub has a 100MB file limit per file.*
