Depends on a running instance of nginx-proxy in order to expose `radarr` and `sonarr`.

Copy `.env.stub` to `.env` and update the values. Set `PUID` and `PGID` to the values of a user you wish to own and manage the configuration and data files. 

Create directories for `./sonarr`, `./radarr`, `./prowlarr`, `./qbittorrent`, `./qbittorrent-vpn` and `./plex` and ensure that they are owned by the user above.

qBittorrent communicates through a VPN container via Wireguard. Download a Wireguard configuration from your VPN provider and place it at `qbittorrent-vpn/wireguard/wg0.conf`.

