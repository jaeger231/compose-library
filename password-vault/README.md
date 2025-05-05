
# Password Vault Service (Vaultwarden)

A lightweight, self-hosted password manager compatible with Bitwarden clients.

## Features

- Bitwarden API-compatible server
- Web vault interface
- Secure password storage
- Cross-platform client support

## Prerequisites

- Docker and Docker Compose installed
- Port 5555 available on your host machine

## Quick Start

1. Clone this repository or create the `docker-compose.yaml` file

2. Start the service:
   ```bash
   docker-compose up -d
   ```

3. Access the web interface at:
   ```
   http://localhost:5555
   ```

## Configuration

### Ports
- Service exposed on host port `5555` (container port `80`)

### Volumes
- `./vw-data:/data` - Stores all vault data persistently

### Automatic Restart
- Configured to restart automatically unless manually stopped

## Data Location
All vault data is stored in the `vw-data` directory in your project folder.

## Administration

- Create your first account by visiting the web interface
- Use any Bitwarden-compatible client with your server URL:
  ```
  http://your-server-address:5555
  ```

## Backup Recommendations
Regularly back up the `vw-data` directory to prevent data loss.

## Security Notes

1. For production use:
   - Enable HTTPS (consider using a reverse proxy)
   - Set up proper firewall rules
   - Use strong master passwords

2. The service runs as a non-root user inside the container by default

## Troubleshooting

- Check logs:
  ```bash
  docker logs password-vault
  ```

- Verify container status:
  ```bash
  docker ps
  ```

1. Stop the container:
   ```bash
   docker-compose down
   ```

2. Pull the latest image:
   ```bash
   docker-compose pull
   ```

3. Restart:
   ```bash
   docker-compose up -d
   ```
```



