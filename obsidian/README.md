# Obsidian using Docker Compose

This Docker Compose setup runs [Obsidian](https://obsidian.md/) in a container using LinuxServer's image, enabling note-taking in a self-hosted environment.

##  Service

### 1. **obsidian**
- **Image:** `lscr.io/linuxserver/obsidian`
- **Purpose:** Self-hosted version of Obsidian for markdown-based note-taking and knowledge management.
- **Ports:**
  - `3421:3000` — Access Obsidian in your browser at `http://localhost:3421`
- **Volumes:**
  - `./obsidian-data:/config` — Stores configuration and vault data
- **Shared Memory:** `1gb` to support the application efficiently
- **Environment Variables:**
  - `PUID` — User ID for file ownership
  - `PGID` — Group ID for file ownership
  - `TZ` — Time zone (e.g., `Europe/London`)
- **Restart Policy:** `unless-stopped`

##  Usage

1. **Create the required data directory:**
   ```bash
   mkdir -p ./obsidian-data
   ```

2. **Start Obsidian:**
   ```bash
   docker compose up -d
   ```

3. **Access the app:**
   - Open your browser and visit `http://localhost:3421`

4. **Stop the container:**
   ```bash
   docker compose down
   ```

##  PS:

- Obsidian requires a browser to use; this container exposes the web UI.
- Ensure you set `PUID`, `PGID`, and `TZ` in a `.env` file or export them before launching.
- This setup is suitable for personal use and note syncing.
