# Docker-Compose Files
Repository containing docker-compose files I use (or have used). Be sure to check the documentation of whatever service you want to run for any configuration changes or other updates. These composefiles will pull the latest image, but their config won't magically adapt to breaking changes that may be introduced in the future. The date of the last commit should be a reasonable indicator of when this last worked (for me). 
Use these files as a template to create your own setup, do not copy and deploy them mindlessly. Most important: **Read the README!**

## Current stacks

| Name                                                | Images |
|-----------------------------------------------------|--------------------------------------|
| [Adguard](./adguard)                                | `adguard/adguardhome`|
| [Archivebox](./archivebox)                          | `archivebox/archivebox` |
| [Arr*-stack](arr-stack)                             | `binhex/arch-qbittorrentvpn`, `ghcr.io/hotio/sabnzbd`, `ghcr.io/hotio/radarr`, `ghcr.io/hotio/sonarr`, `ghcr.io/hotio/lidarr`, `ghcr.io/hotio/readarr`, `ghcr.io/hotio/bazarr`, `ghcr.io/hotio/jellyseerr`, `ghcr.io/hotio/doplarr`, `ghcr.io/hotio/rflood` |
| [Gitea](./gitea)                                    | `gitea/gitea` |
| [Jellyfin](./jellyfin)                              | `jellyfin/jellyfin` |
| [Navidrome](./navidrome)                            | `deluan/navidrome` |
| [Nextcloud-AIO](./nextcloud-aio)                    | `nextcloud/all-in-one` |
| [Nginx Proxy Manager](./npm)                        | `jc21/nginx-proxy-manager` |
| [Nginx Proxy Manager GoAccess](./npm-goaccess)      | `xavierh/goaccess-for-nginxproxymanager` |
| [PiHole](./pihole)                                  | `pihole/pihole` |
| [Plausible](./plausible)                            | `plausible/analytics`, `postgres`, `maxmindinc/geoipupdate`, `yandex/clickhouse-server` |
| [PsiTransfer](./psitransfer)                        | `psitrax/psitransfer` |
| [Vaultwarden](./vaultwarden)                        | `vaultwarden/server` |
| [Watchtower](./watchtower)                          | `containrrr/watchtower` |
| [Wordpress](./wordpress)                            | `wordpress:latest`, `mysql`, `phpmyadmin/phpmyadmin`, `redis:alpine` |
| [xBackBone](./xbackbone)                            | `lscr.io/linuxserver/xbackbone` |


## General
* Any volume mounts with e.g. config or data are stored at `/portainer/<service_name>` unless specified otherwise. 
* Any web interfaces exposed are ran through a reverse proxy which supplies SSL certificates. Running these services barebones usually means access via insecure HTTP and leaves you open to attacks. **Do not port-forward or expose these services to the internet without a reverse proxy.**
* None of these stacks are to be assumed "secure" by default. WebUI's may be exposed without authentication for example. It is your job to secure the stacks to your own content. Especially when it comes to exposing this to the outside world, do your research and secure your containers (and homelab!).
* I'm expecting you to have some basic understanding of Docker and Docker Compose. If you don't understand something, google it and/or create an issue if you feel like the info should be included.

## Composefile Formatting
I've tried to keep formatting the same across composefiles for readability and consistency, but swapping around different parts (for example, putting `image` above `container_name`) does not have any effect on how the container(s) will run.
```yaml
version:
services:

  service 1:
    container_name:
    image:
    depends on:
    user:
    command:
    expose:
    ports:
    environment:
    sysctls:
    cap_add:
    volumes:
    network:
    restart:

  service 2:
    service:
    container name:

volumes:
  volume 1:
  name:

etc.
```

## (Cross-platform) Compatibility
* This repository expects you to run an x86 based computer and does **not** support arm-based machines like a Raspberry Pi by design (but it's always worth a shot!). It is up to the individual maintainers of each project to support other architectures like arm.
* Windows users might run into trouble when trying to map data directories outside of the WSL environment. All your Windows partitions are mounted to the docker WSL environment under `/mnt/`. As an example, `C:\Users\user1\Documents\nextcloud\` would become `/mnt/c/Users/user1/Documents/nextcloud/`. However, it is strongly recommended not to do this, a mapped directories outside of the WSL environment will incur a severe performance penalty which may not be desirable in some situations.

## Contributing
Any contributions are welcome, just open a PR or submit an issue! Try to follow [the formatting outlined above](#composefile-formatting) for consistency.
