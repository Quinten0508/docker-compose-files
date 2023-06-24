# Docker-Compose files
Repository containing docker-compose files I use (or have used). Be sure to check the documentation of whatever service you want to run for any configuration changes or other updates. These composefiles will pull the latest image, but their config won't magically adapt to breaking changes that may be introduced in the future. Use these files as a template to create your own setup, do not copy and deploy them mindlessly.

## General setup
* Any volume mounts with e.g. config or data are stored at `/portainer/<service_name>`.
* Any web interfaces exposed are ran through a reverse proxy which supplies SSL certificates. Running these services barebones usually means access via insecure, unencrypted HTTP.

## Composefile formatting
I've tried to keep formatting the same across composefiles for readability and consistency, but swapping around different parts (for example, putting `image` above `container_name`) will not have any adverse effects.
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