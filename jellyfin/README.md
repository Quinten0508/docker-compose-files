Media is stored in `/portainer/jellyfin/media/` by default. Change this path to your media location, or add multiple volumes to seperate media. Example:
```
      - /home/user/music:/media/music
      - /home/user/movies:/media/movies
      - /home/user2/movies:/media/movies_user2

(!) Does not include any form of HW acceleration. Please use the Jellyfin docs to add this yourself, as it'll be different depending on your GPU.