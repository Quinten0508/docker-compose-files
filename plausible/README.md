# Plausible Installation

### Defaults
This Plausible installation has a couple of defaults you can play with:
* The WP files are stored in `/portainer/plausible`. You may change this by changing every entry of `volumes`.
* We use a Postgres database as backend for Plausible - this can be changed out for a couple of other DBs. Should be pretty straightforward, but check the Plausible documentation.

### Step-by-Step
1. Download the `docker-compose.yml` file from this directory or paste it into e.g. your `Portainer` instance.
2. Go through the file and **change everything that says** `CHANGEME`**!**
3. Change the port of `plausible` if needed.
4. `docker-compose up -d`

I recommend re-deploying the container every once in a while to pull the latest versions of each image. You can also use something like `watchtower`, but unattended upgrades may break things!