# Homarr

## Why [Homarr](https://homarr.dev)?

Homarr is an open source monitoring application with a lot of integrations with apps like [Pihole](/Pihole/README.md), Home-Assistant and more.

## Prerequisites

- [Portainer](/Portainer/README.md)
- [Macvlan](/Macvlan/README.md) (optional)

## Installation Guide

For the installation i use a docker-compose file. To run it go to Portainer Stacks. You have to modify the comment variables before execution.

> [!NOTE]  
> If you're not using [Macvlan](/Macvlan/README.md) remove networks (2x) and and everything below it.

```yaml
services:
  homarr:
    container_name: Homarr
    image: ghcr.io/ajnart/homarr:latest
    restart: unless-stopped
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock # Optional, only if you want docker integration
      - /volume1/docker/homarr/configs:/app/data/configs
      - /volume1/docker/homarr/icons:/app/public/icons
      - /volume1/docker/homarr/data:/data
    # ports:
    #   - '7575:7575'
    networks:
      default:
        ipv4_address: 192.168.xxx.xxx

networks:
  default:
    name: #macvlan
    external: true
```

After successful execution of the docker-compose file you have to call your defined ipv4_address and port via web-browser (for example: `192.168.1.123:7575`).