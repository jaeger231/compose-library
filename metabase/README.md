
# Metabase and PostgreSQL Docker Compose Setup

This repository contains a Docker Compose configuration for running **Metabase** and **PostgreSQL** in separate containers. Metabase will connect to a PostgreSQL database for data storage, and you can access the Metabase dashboard through a web interface.

## Services Overview

### 1. **Metabase**

* **Image**: `metabase/metabase`
* **Port**: Exposed on `3030` (accessible at `http://localhost:3030`)
* **Database Connection**: Uses PostgreSQL as the backend database.
* **Volume**: Persists Metabase data in `./metabase-data`.

### 2. **PostgreSQL Database**

* **Image**: `postgres:15`
* **Container Name**: `metabase-postgres`
* **Database**: Creates the database `metabase` with user `user` and password `user`.
* **Volume**: Persists PostgreSQL data in `./postgres-data`.

## Prerequisites

Before you start, ensure you have the following installed:

* Docker
* Docker Compose

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-repository-name.git
cd your-repository-name
```

### 2. Create an `.env` File

Create a `.env` file in the root directory and define your environment variables:

```env
# Database connection settings
MB_DB_TYPE=postgres
MB_DB_DBNAME=metabase
MB_DB_PORT=5432
MB_DB_USER=user
MB_DB_PASS=user
MB_DB_HOST=db

# PostgreSQL settings
POSTGRES_DB=metabase
POSTGRES_USER=user
POSTGRES_PASSWORD=user
```

### 3. Start the Services

Run the following command to start both Metabase and PostgreSQL containers in detached mode:

```bash
docker compose up -d
```

This will start the services in the background.

### 4. Access Metabase

After the containers have started, open your browser and go to `http://localhost:3030` to access the Metabase interface. You will be prompted to complete the setup, such as connecting to the PostgreSQL database.

### 5. Stopping the Services

To stop the containers, run:

```bash
docker compose down
```

This will stop the containers and remove them, but your data will be persisted in the local volumes (`./metabase-data` and `./postgres-data`).

### 6. Volumes and Data Persistence

* **PostgreSQL Data**: The data for the PostgreSQL database is stored in the `./postgres-data` directory on your local machine.
* **Metabase Data**: The data for Metabase, including user information and dashboards, is stored in the `./metabase-data` directory.

These volumes are mapped directly to the host machine for data persistence between container restarts.

## Troubleshooting

* **Cannot Connect to Database**: Ensure that the `db` service has fully started before `metabase` tries to connect. Docker Compose handles the startup order, but if you experience issues, you can try restarting the containers with `docker-compose restart`.
* **Container Logs**: If you encounter any issues, check the logs for each container:

  * Metabase: `docker compose logs metabase`
  * PostgreSQL: `docker compose logs db`

