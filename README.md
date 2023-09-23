# Docker-Compose Files
Repository containing docker-compose files I use (or have used). Be sure to check the documentation of whatever service you want to run for any configuration changes or other updates. These composefiles will pull the latest image, but their config won't magically adapt to breaking changes that may be introduced in the future. Use these files as a template to create your own setup, do not copy and deploy them mindlessly.

## General Setup
* Any volume mounts with e.g. config or data are stored at `/portainer/<service_name>`.
* Any web interfaces exposed are ran through a reverse proxy which supplies SSL certificates. Running these services barebones usually means access via insecure HTTP and leaves you open to attacks. **Do not port-forward or expose these services to the internet without a reverse proxy.**

## Composefile Formatting
I've tried to keep formatting the same across composefiles for readability and consistency, but swapping around different parts (for example, putting `image` above `container_name`) does not have any effect on how the container(s) will run.
```
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
* This repository expects you to run an x86 based computer and does **not** support arm-based machines like the raspberry pi by default. It is up to the individual maintainers of each project to support other architectures like arm.
* Windows users might run into trouble when trying to map data directories outside of the WSL environment. All your Windows partitions are mounted to the docker WSL environment under `/mnt/`. As an example, `C:\Users\user1\Documents\nextcloud\` would become `/mnt/c/Users/user1/Documents/nextcloud/`.

## Contributing
Any contributions are welcome, just open a PR or submit an issue!
