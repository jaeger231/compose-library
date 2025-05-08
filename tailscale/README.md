
# Tailscale 

This project sets up a Tailscale VPN client.

## Prerequisites

- Docker installed on your host machine
- A Tailscale auth key (can be generated at https://login.tailscale.com/admin/settings/keys)

## Setup

1. Create a `.env` file in the same directory with your Tailscale auth key:
   ```
   TS_AUTHKEY=your-auth-key-here
   ```

2. Start the container:
   ```bash
   docker compose up -d
   ```

## Configuration

The container is configured with:
- NET_ADMIN capabilities (required for VPN functionality)
- Persistent storage for Tailscale state (mounted at `/var/lib/tailscale`)
- Automatic authentication using your provided auth key

## Volumes

- `tailscale-data`: Persistent storage for Tailscale client state

## Management

- Check container logs:
  ```bash
  docker logs tailscale
  ```

- Stop the container:
  ```bash
  docker compose down
  ```

## PS:

- The container will automatically join your Tailscale network using the provided auth key
- You can manage the device from your Tailscale admin console
- The container uses the latest Tailscale client image

## Security

Keep your `.env` file secure as it contains your Tailscale auth key. Do not commit it to version control.
```

