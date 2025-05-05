# Code-Server with PostgreSQL using Docker Compose

Here, we set up code-server [code-server](https://github.com/coder/code-server) environment along with a PostgreSQL database using Docker Compose. It allows you to write and run code in a cloud-based Visual Studio Code environment accessible via the web.

Services

### 1. **code-server**
- **Image:** `lscr.io/linuxserver/code-server:latest`
- **Purpose:** A web-based IDE (VS Code).
- **Environment Variables:**
  - `PUID` – User ID to run the container with proper permissions.
  - `PGID` – Group ID to run the container.
  - `TZ` – Timezone (e.g., `Europe/London`).
- **Ports:** 
  - `8443:8443` — Exposes the IDE on port 8443.
- **Volumes:**
  - `codeserver-config` — Persistent configuration storage.
- **Restart Policy:** `unless-stopped`

### 2. **codeserver_db**
- **Image:** `postgres:15`
- **Purpose:** Provides PostgreSQL as a backend database.
- **Environment Variables:**
  - `POSTGRES_DB` – Database name.
  - `POSTGRES_USER` – PostgreSQL username.
  - `POSTGRES_PASSWORD` – PostgreSQL password.
- **Volumes:**
  - `dbdata-codeserver` — Persistent data storage for the PostgreSQL database.
- **Restart Policy:** `on-failure`

## Volumes

- `codeserver-config` – Stores code-server configuration and settings.
- `dbdata-codeserver` – Stores PostgreSQL data files.

## Usage

1. **Set environment variables:** Create a `.env` file in the same directory as your `docker-compose.yml` with the following content:
   ```env
    PUID=1000
    PGID=1000
    TZ=Africa/Nairobi

    POSTGRES_DB=codeserver_db
    POSTGRES_USER=test
    POSTGRES_PASSWORD=test
```

2. **Start the stack:**
   ```bash
   docker compose up -d
   ```

3. **Access code-server:**
   - Open your browser and go to `https://localhost:8443`

4. **Stop the stack:**
   ```bash
   docker compose down
   ```
