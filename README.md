### Prerequesites
Depends on a running instance of nginx-proxy in order to expose `radarr` and `sonarr`.

### Initial setup
Copy `.env.stub` to `.env` and update the values. Set `SONARR_HOSTNAME` and `RADARR_HOSTNAME` to domains that you own and wish to be accessible on the Internet (you will obviously need to own these domains and have them pointing to your server). 'Set `PUID` and `PGID` to the values of a user you wish to own and manage the configuration and data files. Set `MEDIA_ROOT` to the directory where you want your media to be stored, and ensure that it is owned by the aforementioned user. Set the `PORT` variables to the ports to expose for Plex, Prowlarr and qBitTorrent. 

### Ports
You may need to open your device's firewall to the ports specified in `docker-compose.yml`. In order to access Plex on the Internet, the value you specify for `PLEX_PORT` will need to be forwarded through your network's router.

### qBittorrent
qBittorrent communicates through a VPN container via Wireguard. Download a Wireguard configuration from your VPN provider and place it at `qbittorrent-vpn/wireguard/wg0.conf` (use `chown` to ensure it is owned by the aforementioned user). When first starting the `qbittorrent` container, the logs will display a temporary password. Use this to log into the Web UI (<local ip>:<QBITTORRENT_PORT>), then change the credentials through the interface. `sonarr` and `radarr` will communicate with `qbittorrent` using the host name `qbittorrent-vpn`, port `<QBITTORRENT_PORT>` and the aforementioned credentials.

### Running
Run with `docker compose up -d`.
