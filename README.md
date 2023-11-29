# Maker Management Platform

Maker Management Platform, or mmp, aims to simplify and unify the management of a variety of digital assets related to 3d printing and manufactoring, laser engraving and such.

### Disclaimer
Under development

## Discussion
![Discord Shield](https://discordapp.com/api/guilds/1013417395777450034/widget.png?style=shield)

Join discord if you need any support https://discord.gg/SqxKE3Ve4Z


## Runing mmp local

docker-compose.yml
``` yaml
---
version: "3.6"
services:
  agent:
    image: ghcr.io/maker-management-platform/agent:rebuild
    container_name: agent
    volumes:
      - ./library:/library
      - ./config.toml:/app/config.toml
    ports:
      - 8000:8000
    environment:
      - "THINGIVERSE_TOKEN=" # needed for the thingiverse download feature
      #- "PORT=8000"
      #- "LIBRARY_PATH=/library"
      #- "MAX_RENDER_WORKERS=5"
      #- "MODEL_RENDER_COLOR=#167DF0"
      #- "MODEL_BACKGROUND_COLOR=#FFFFFF"
      #- "LOG_PATH=./log" # If you wish to log to a file
    
    restart: unless-stopped

  ui:
    image: ghcr.io/maker-management-platform/mmp-ui:nightly
    container_name: agent
    ports:
      - 8080:8080
    environment:
      - "LOCAL_BACKEND=192.168.xxx.xxx:8000" #local address for the agent
    
    restart: unless-stopped

```