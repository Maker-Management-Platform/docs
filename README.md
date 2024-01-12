# Maker Management Platform

Maker Management Platform, or mmp, aims to simplify and unify the management of a variety of digital assets related to 3d printing, manufactoring, laser engraving and such.

### Disclaimer
Insecure, use locally only.

Under development so things might break, please contact us via issue or on discord.

#### Create and manage projects
![Projects](/assets/projects.png)
#### Projects are a collection of assets like models, images, slice files and documents
![Projects](/assets/assets.png)
#### You can preview multiple models at the same time and see how they fit together
![Projects](/assets/model_preview.png)
#### Send your slices directly to your printer
![Projects](/assets/printers.png)
![Projects](/assets/slices_send_to_printer.png)
#### Integrate with your slicer
![Projects](/assets/slicer_integration.png)
#### Import projects from public platforms
By using [MMP Companion browser extension](https://github.com/Maker-Management-Platform/mmp-companion) you can import projects from multiple public platforms

This feature is also available in MMP UI but limited to thingiverse (see MMP companion for more details)


## Support and Discussion
If you find any problems or want to request a feature please open an issue in the related project:
- UI related issues: [Here](https://github.com/Maker-Management-Platform/mmp-ui/issues)
- Backend related issues: [Here](https://github.com/Maker-Management-Platform/agent/issues)
- Companion (extension) related issues: [Here](https://github.com/Maker-Management-Platform/mmp-companion/issues)
- Documentation / typos related issues: [Here](https://github.com/Maker-Management-Platform/docs/issues)

If you have any doubts or do you wanna chat about it join us on [Discord](https://discord.gg/SqxKE3Ve4Z)

![Discord Shield](https://discordapp.com/api/guilds/1013417395777450034/widget.png?style=shield)

## Runing mmp locally

docker-compose.yml
``` yaml
---
version: "3.6"
services:
  agent:
    image: ghcr.io/maker-management-platform/agent:latest
    container_name: agent
    volumes:
      - ./library:/library
      - ./config.toml:/app/config.toml
    ports:
      - 8000:8000 # currently required for your slicer integration, looking for a workaround
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
    image: ghcr.io/maker-management-platform/mmp-ui:latest
    container_name: ui
    ports:
      - 8081:8081
    environment:
      - "AGENT_ADDRESS=agent:8000" #local address for the agent
    restart: unless-stopped

```

## Thingiverse token

To get a Thingiverse token go to [Apps](https://www.thingiverse.com/apps/create) > Create an App

Select "Web App" fill in any name & description, accept the policy, and click on "Create & Get App Key" at the top of the page.

Use the "App Token" for the `THINGIVERSE_TOKEN` environment.
