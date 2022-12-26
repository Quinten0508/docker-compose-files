# Wordpress Installation

### Defaults
This Wordpress installation has a couple of defaults you can play with:
* The WP files are stored in `/portainer/wordpress`. You may change this by changing every entry of `volumes`.
* We use a network called `wordpress` and assign every container their own static IP. If the default IPs are already in use, change them under every container and under the `network` segment.
* We use a redis container in tandem with WP to allow for caching, this will greatly increase speeds and reduce CPU load.

### Step-by-Step
1. Download the `docker-compose.yml` file from this directory or paste it into e.g. your `Portainer` instance.
2. Go through the file and **change everything that says** `CHANGEME`**!**
3. Change the ports of `wordpress` and `phpmyadmin` if needed.
4. Change the IP range if needed.
5. `docker-compose up -d`

I recommend re-deploying the container every once in a while to pull the latest versions of each image. You can also use something like `watchtower`, but unattended upgrades may break things!