# Media Stack — Quartermaster GitOps Repo

Full **Arr suite + Jellyfin** stack for automated TV show and movie downloads
with a beautiful streaming frontend. Managed by
[Quartermaster](https://github.com/example/quartermaster).

## Services

| Service | Port | Purpose |
|---------|------|---------|
| **qBittorrent** | `8080` | Torrent download client |
| **Prowlarr** | `9696` | Indexer/tracker manager for Sonarr & Radarr |
| **Sonarr** | `8989` | TV series automation |
| **Radarr** | `7878` | Movie automation |
| **Jellyfin** | `8096` | Media server (watch your content) |

## Host Directory Layout

```
/mnt/
├── downloads/          # Torrent downloads (shared by qBittorrent, Sonarr, Radarr)
└── media/
    ├── tv/             # Organized TV shows (Sonarr → Jellyfin)
    └── movies/         # Organized movies (Radarr → Jellyfin)

/opt/
├── qbittorrent/config/
├── prowlarr/config/
├── sonarr/config/
├── radarr/config/
└── jellyfin/config/
```

## Quick Start

1. **Create directories and set ownership:**

   ```bash
   sudo mkdir -p /mnt/{downloads,media/{tv,movies}}
   sudo mkdir -p /opt/{qbittorrent,prowlarr,sonarr,radarr,jellyfin}/config
   sudo chown -R 1000:1000 /mnt/downloads /mnt/media /opt/{qbittorrent,prowlarr,sonarr,radarr,jellyfin}
   ```

2. **Point Quartermaster at this repo** and let it reconcile.

## Post-Deployment Setup

After Quartermaster brings everything up:

1. **qBittorrent** → http://your-host:8080 (default: `admin` / `adminadmin`)
2. **Prowlarr** → http://your-host:9696 — Add your indexers, then connect to Sonarr & Radarr under Settings → Apps
3. **Sonarr** → http://your-host:8989 — Add series, configure download client (qBittorrent)
4. **Radarr** → http://your-host:7878 — Add movies, configure download client (qBittorrent)
5. **Jellyfin** → http://your-host:8096 — Add libraries pointing to `/data/tvshows` and `/data/movies`

> **Tip:** Make sure TZ matches your timezone in the manifest.
