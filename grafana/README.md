# Grafana with PostgreSQL using Docker Compose

This setup runs [Grafana Enterprise](https://grafana.com/grafana/enterprise/) with PostgreSQL as the external database backend using Docker Compose.

##  Services

### 1. **grafana**
- **Image:** `grafana/grafana-enterprise`
- **Purpose:** Grafana is a data visualization and monitoring platform.
- **Ports:**
  - `3333:3000` — Web UI available on port 3333.
- **Environment Variables:**
  - `GF_DATABASE_TYPE` — Database type, e.g., `postgres`.
  - `GF_DATABASE_HOST` — Host of the PostgreSQL service (e.g., `grafana-db:5432`).
  - `GF_DATABASE_NAME` — Name of the PostgreSQL database.
  - `GF_DATABASE_USER` — PostgreSQL username.
  - `GF_DATABASE_PASSWORD` — PostgreSQL password.
- **Volumes:**
  - `grafana-storage` — Persistent data for Grafana.
- **Depends on:** `grafana-db`
- **Restart Policy:** `unless-stopped`

### 2. **grafana-db**
- **Image:** `postgres:15`
- **Purpose:** PostgreSQL database used as Grafana's backend.
- **Environment Variables:**
  - `POSTGRES_DB` — Name of the database.
  - `POSTGRES_USER` — Username for authentication.
  - `POSTGRES_PASSWORD` — Password for the user.
- **Volumes:**
  - `grafana-db-data` — Persistent PostgreSQL data.
- **Restart Policy:** `always`

##  Volumes

- `grafana-storage` – Stores Grafana data.
- `grafana-db-data` – Stores PostgreSQL data.

##  Usage

1. **Create a `.env` file** in the same directory as your `docker-compose.yml`:
   ```env
   GF_DATABASE_TYPE=postgres
   GF_DATABASE_HOST=grafana-db:5432
   GF_DATABASE_NAME=grafana
   GF_DATABASE_USER=grafanauser
   GF_DATABASE_PASSWORD=strongpassword

   POSTGRES_DB=grafana
   POSTGRES_USER=grafanauser
   POSTGRES_PASSWORD=strongpassword
   ```

2. **Start the services:**
   ```bash
   docker-compose up -d
   ```

3. **Access Grafana:**
   - Open your browser and go to `http://localhost:3333`

4. **Stop the stack:**
   ```bash
   docker-compose down
   ```

