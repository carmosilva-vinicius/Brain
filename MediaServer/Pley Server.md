My plex server with container:

```yml
# sonarr
Sonarr:
    image: cr.hotio.dev/hotio/sonarr
    volumes:
        - /path/to/config/sonarr:/config
        - /host/data:/data
    environment:
        - PUID=111
        - PGID=321
        - UMASK=002

# deluge
Deluge:
    image: binhex/arch-delugevpn
    volumes:
        - /path/to/config/deluge:/config
        - /host/data/torrents:/data/torrents
    environment:
        - PUID=222
        - PGID=321
        - UMASK=002

# SABnzbd
SABnzbd:
    image: cr.hotio.dev/hotio/sabnzbd
    volumes:
        - /path/to/config/sabnzbd:/config
        - /host/data/usenet:/data/usenet
    environment:
        - PUID=333
        - PGID=321
        - UMASK=002

# plex
Plex:
    image: cr.hotio.dev/hotio/plex
    volumes:
        - /path/to/config/plex:/config
        - /host/data/media:/data/media

    environment:
        - PUID=444
        - PGID=321
        - UMASK=002
```

