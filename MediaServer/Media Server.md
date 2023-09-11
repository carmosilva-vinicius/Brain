My media server server with Plex, Arr apps in docker [[Linux]] container:

```yml
version: "3.8"
services:
	prowlarr:
	container_name: prowlarr
	image: ghcr.io/hotio/prowlarr
	restart: unless-stopped
	logging:
		driver: json-file
	ports:
		- "9696:9696"
	environment:
		- PUID=1000
		- PGID=1000
		- UMASK=002
		- TZ=America/Sao_Paulo
	volumes:
		- /etc/localtime:/etc/localtime:ro
		- /docker/MediaServer/app/prowlarr:/config
		- /docker/MediaServer/data:/data
	networks:
		- MediaServer
	radarr:
		container_name: radarr
		image: ghcr.io/hotio/radarr
		restart: unless-stopped
		logging:
			driver: json-file
		ports:
			- 7878:7878
		environment:
			- PUID=1000
			- PGID=1000
			- UMASK=002
			- TZ=America/Sao_Paulo
		volumes:
			- /etc/localtime:/etc/localtime:ro
			- /docker/MediaServer/app/radarr:/config
			- /docker/MediaServer/data:/data
		networks:
			- MediaServer
	sonarr:
		container_name: sonarr
		image: ghcr.io/hotio/sonarr
		restart: unless-stopped
		logging:
			driver: json-file
		ports:
			- 8989:8989
		environment:
			- PUID=1000
			- PGID=1000
			- UMASK=002
			- TZ=America/Sao_Paulo
		volumes:
			- /etc/localtime:/etc/localtime:ro
			- /docker/MediaServer/app/sonarr:/config
			- /docker/MediaServer/data:/data
		networks:
			- MediaServer
	qbittorrent:
		container_name: qbittorrent
		image: ghcr.io/hotio/qbittorrent
		ports:
			- "8080:8080"
		environment:
			- PUID=1000
			- PGID=1000
			- UMASK=002
			- TZ=America/Sao_Paulo
		volumes:
			- /docker/MediaServer/app/qbittorrent:/config
			- /docker/MediaServer/data/torrents:/data/torrents
		networks:
			- MediaServer
	bazarr:
		container_name: bazarr
		image: ghcr.io/hotio/bazarr
		ports:
			- "6767:6767"
		environment:
			- PUID=1000
			- PGID=1000
			- UMASK=002
			- TZ=America/Sao_Paulo
		volumes:
			- /docker/MediaServer/app/bazarr:/config
			- /docker/MediaServer/data/torrents/movies:/data/torrents/movies
			- /docker/MediaServer/data/torrents/tv:/data/torrents/tv
		networks:
			- MediaServer
	pms-docker:
		container_name: plex
		ports:
			- '32400:32400/tcp'
			- '8324:8324/tcp'
			- '32469:32469/tcp'
			- '1900:1900/udp'
			- '32410:32410/udp'
			- '32412:32412/udp'
			- '32413:32413/udp'
			- '32414:32414/udp'
		environment:
			- TZ=America/Sao_Paulo
			- PLEX_CLAIM=claim-jSFGMPjYbxkp6SL8yo9s
			- 'ADVERTISE_IP=http://172.19.0.3:32400/'
		hostname: PlexServer
		volumes:
			- '/docker/MediaServer/app/plex/config:/config'
			- '/docker/MediaServer/app/plex/transcode:/transcode'
			- '/docker/MediaServer/data:/data'
		image: plexinc/pms-docker
		networks:
			- MediaServer
networks:
	MediaServer:
		driver: bridge
```

