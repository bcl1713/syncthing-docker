# Syncthing Docker Setup

This repository contains a Docker Compose configuration for running Syncthing using the LinuxServer.io image, designed for deployment with Portainer using Git repository integration.

## Quick Start

1. Create the required directories on your Docker host:
   ```bash
   sudo mkdir -p /mnt/TANK/docker/syncthing/{config,sync}
   sudo chown -R 1000:1000 /mnt/TANK/docker/syncthing
   ```

2. Deploy in Portainer:
   - Go to Stacks → Add Stack
   - Select "Repository" as the build method
   - Enter this repository URL
   - Set the compose file path to `docker-compose.yml`
   - Deploy the stack

## Configuration

- **Image**: `lscr.io/linuxserver/syncthing:latest`
- **Web UI Port**: 8384
- **File Transfer Ports**: 22000 (TCP/UDP)
- **Discovery Port**: 21027 (UDP)

## Volume Mounts

- `/mnt/TANK/docker/syncthing/config:/config` - Syncthing configuration
- `/mnt/TANK/docker/syncthing/sync:/sync` - Data directory for synchronization

## Environment Variables

- `PUID=1000` - User ID
- `PGID=1000` - Group ID
- `TZ=Etc/UTC` - Timezone

## Portainer Git Integration

This repository is designed to be deployed directly from Git in Portainer:

1. **Stack Creation**: Use "Repository" build method
2. **Auto-updates**: Enable automatic redeploy when repository updates
3. **Branch Selection**: Use `main` branch for stable releases

## Network

The container runs on a custom bridge network `syncthing-network` for isolation.

## Accessing Syncthing

After deployment, access the web interface at `http://your-docker-host:8384`

## Troubleshooting

- Ensure the host directories exist and have correct permissions
- Check firewall settings for ports 8384, 22000, and 21027
- Verify the PUID/PGID match your system user
- For Portainer deployment issues, check the stack logs in Portainer