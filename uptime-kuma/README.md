# Uptime Kuma with PostgreSQL using Docker Compose

This setup provides [Uptime Kuma](https://github.com/louislam/uptime-kuma), a self-hosted monitoring tool, integrated with PostgreSQL for persistent database storage using Docker Compose.

##  Services

### 1. **uptime-kuma**
- **Image:** `louislam/uptime-kuma:1`
- **Purpose:** Uptime Kuma provides monitoring for websites, APIs, services, and more.
- **Ports:** 
  - `3001:3001` — Web UI accessible on port 3001.
- **Environment Variables:**
  - `DATABASE_URL` — Connection string for the PostgreSQL database.
- **Volumes:**
  - `uptime-kuma-data` — Persistent data for Uptime Kuma.
- **Depends on:** `uptime-db`
- **Restart Policy:** `always`

### 2. **uptime-db**
- **Image:** `postgres:15`
- **Purpose:** PostgreSQL database used as Uptime Kuma's backend.
- **Environment Variables:**
  - `POSTGRES_DB` — Name of the database.
  - `POSTGRES_USER` — Username for authentication.
  - `POSTGRES_PASSWORD` — Password for the user.
- **Volumes:**
  - `uptime-db-data` — Persistent data for PostgreSQL.
- **Restart Policy:** `always`

##  Volumes

- `uptime-kuma-data` – Stores configuration and monitoring data.
- `uptime-db-data` – Stores PostgreSQL database files.

##  Usage

1. **Create a `.env` file** in the same directory as your `docker-compose.yml`:
   ```env
   POSTGRES_DB=uptimekuma
   POSTGRES_USER=uptimeuser
   POSTGRES_PASSWORD=strongpassword
   DATABASE_URL=postgres://uptimeuser:strongpassword@uptime-db:5432/uptimekuma
   ```

2. **Start the services:**
   ```bash
   docker-compose up -d
   ```

3. **Access Uptime Kuma:**
   - Open your browser and go to `http://localhost:3001`

4. **Stop the stack:**
   ```bash
   docker-compose down
   ```

