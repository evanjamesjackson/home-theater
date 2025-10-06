### Prerequesites
Requires Docker. Depends on a running instance of [nginx-proxy](https://github.com/nginx-proxy/nginx-proxy) in order to expose `radarr` and `sonarr` to the Internet (remove any configuration related to this if you don't wish to expose these services outside of your network).

### Initial setup
Copy `.env.stub` to `.env` and update the values. Set `SONARR_HOSTNAME` and `RADARR_HOSTNAME` to domains that you own and wish to be accessible on the Internet (you will obviously need to own these domains and have them pointing to your server). 'Set `PUID` and `PGID` to the values of a user you wish to own and manage the configuration and data files. Set `MEDIA_ROOT` to the directory where you want your media to be stored, and ensure that it is owned by the aforementioned user. Set the `PORT` variables to the ports to expose for Plex, Sonarr, Radarr, Prowlarr and qBitTorrent. The `PLEX_CLAIM` value will need to be set after you first run the Plex container - once running, go to `<server ip>:<PLEX_PORT>` and click the "Claim Server" button.

### Ports
You may need to open your device's firewall to the ports specified in `docker-compose.yml`. In order to access Plex on the Internet, the value you specify for `PLEX_PORT` will need to be forwarded through your network's router.

### qBittorrent
qBittorrent communicates through a VPN container via Wireguard. Download a Wireguard configuration from your VPN provider and place it at `./wg0.conf` (use `chown` to ensure it is owned by the aforementioned user). When first starting the `qbittorrent` container, the logs will display a temporary password. Use this to log into the Web UI (<local ip>:<QBITTORRENT_PORT>), then change the credentials through the interface. `sonarr` and `radarr` will communicate with `qbittorrent` using the host name `qbittorrent-vpn`, port `<QBITTORRENT_PORT>` and their respective API keys (found in their respective Settings interfaces).

### Running
Run with `docker compose up -d`.
