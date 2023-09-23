This is about as "plug and play" as an arr* stack will get. It **requires** configuration, explained below.

## Requirements
* A functioning VPN which allows you to export OpenVPN or Wireguard config files.
* A server slightly more capable than a RPi.
* Storage for all of your Linux ISOs (4K bluray *will* take up 20+ GB).

Furthermore, some optional components have their own requirements:
* Jellyseer: A Jellyfin server (*duh*). (You can find one in this repo!)
* SABnzbd: A usenet subscription.
* Doplarr: A Discord bot (or the ability to set one up).

Finally: Grab a snack and a drink. Be prepared to spend the next hour or so getting everything set up correctly. There's no undo button when you accidentally wipe your config files or delete the wrong folder.


## So, where do I begin?
This stack consists of 10 containers. You probably won't need them all. Pick and choose, then delete the rest. I'll lay the stack out here.

### Content fetchers
These will actually download the content or assist in it.
* Arch-qBittorrentVPN (requires Prowlarr!) 
	* A torrent client with VPN and privoxy built-in. This makes sure you're never torrenting without VPN and saves you a lot of networking.
* Prowlarr
	* Will search the internet for torrents using indexers you specify.
* SABnzbd
	* A Usenet downloader and an alternative to torrenting. Does not require a VPN or prowlarr.
* rFlood (broken!)
	* Alternative to Arch-qBittorrentVPN with the same functionality. Does not work in its current state (PRs welcome!).

### Collection managers
These will manage your content, sending requests to the fetchers.
* Radarr: Movies
* Sonarr: TV series
* Lidarr: Music
* Readarr: Books
* Whisparr: (not included) adult content

### Request managers
These allow you to request content.
* Doplarr: Discord bot (Radarr + Sonarr).
* Jellyseerr: Web portal specifically for Jellyfin (Radarr + Sonarr).

Simply put, you'll need at least one content fetcher and one collection manager. If you're going with torrenting, you'll need both `Arch-qBittorrentVPN` and `Prowlarr`.
If you've made your choices, delete the rest of the containers from the composefile, then come back.



## Entries to change


### Universal  (all containers)
* All filepaths
	The default is `$FILEPATH`. Change to the host path where you want to store the goods.
* Timezone
	The default timezone is set to the environment variable `$TIMEZONE`. This var isn't set to anything, but you can create a `.env` file and add it or simply replace it with your timezone (ex: Europe/Amsterdam).

### Arch-qBittorrentVPN
* VPN_PROV: `<pia|airvpn|protonvpn|custom>`. See the [GH](https://github.com/binhex/arch-qbittorrentvpn) for config.
* VPN_CLIENT: `<openvpn|wireguard>`
* LAN_NETWORK: `<lan ipv4 network>/<cidr notation>`
* NAME_SERVERS: `<name server ip(s)>`

### Doplarr
* SONARR__API: Sonarr API token (found in the WebUI)
* RADARR__API: Radarr API token (found in the WebUI)
* DISCORD__TOKEN: Your Discord bot's token. Best stored in a seperate `.env` file for security.


## Miscellaneous

### Helpful links
* [Servarr wiki](https://wiki.servarr.com/)
	* Official wiki for Lidarr, Prowlarr, Radarr, Readarr, Sonarr, and Whisparr.
* [TRaSH Guides](https://trash-guides.info/)
	* Guides on setting up everything post-install.
* [Hotio](https://hotio.dev/)
	* Maintains and serves most of the Docker images. You can find another dozen arr-related containers on here with (almost) plug-and-play composefiles. Integrate them and create a PR if you feel like helping out!

### Debugging
* A specific container is misbehaving and the logs don't show enough detail: 
	* Put `LOG_LEVEL=DEBUG` in the environment section of the troublesome container. This will make it spit out a lot more info in its logs.
* The stack won't launch because ports are already in use:
	* Issue `sudo netstat -tnlp` from the host machine to see which ports may already be in use. If you change one of the container's ports, be sure to check the rest of the composefile!


### Contrubuting
You are welcome to open issues or create a PR. Please be aware that I do not condone the act of piracy and will not be discussing topics related to this (e.g. "what indexer/usenet provider/vpn should I get?"). If you need support with your personal setup, be sure to look through the [helpful links](#helpful-links) above. TRaSH guides has a discord server, but, again, search before you post!

## Final notes
* This stack (alongside most other stacks here) is **not** secure. Most WebUIs do not have password protection and will be open to anyone in your network. Security should be considered on a per-situation basis and is not something I will configure for you.
* This stack does use TRaSH's hardlinks, so r/w performance should be optimal. It does not feature any of TRaSH's quality profiles. There are several options to import these.