# Paperless NGX

The installation has been done on a Synology DS720 but sould work on any System using [Portainer](https://www.portainer.io/). You can find more Information about Paperless-ngx on their [Website](https://docs.paperless-ngx.com/) and [GitHub](https://github.com/paperless-ngx/paperless-ngx).

## Why Paperless?

Paperless-ngx is a community-supported open-source document management system with a webinterface and [OCR](https://en.wikipedia.org/wiki/Optical_character_recognition). The biggest advantage for me is that it saves files in the file directory instead of a database.

## Prerequisites

- [Portainer](https://www.portainer.io/)

## Installation Guide

For the installation i use a docker-compose file. To run it go to Portainer Stacks. You have to modify the comment variables before execution.

```yaml
services:
  redis:
    image: redis
    container_name: paperless-redis
    restart: unless-stopped
    networks:
      default:
        ipv4_address: #192.168.1.123
    volumes:
      - /volume1/paperless/redis:/user/local/etc/redis

  webserver:
    image: ghcr.io/paperless-ngx/paperless-ngx:latest
    container_name: paperless-ngx
    restart: unless-stopped
    depends_on:
      - redis
    ports:
      - 8000:8000
    volumes:
      - /volume1/paperless/data:/usr/src/paperless/data
      - /volume1/paperless/media:/usr/src/paperless/media
      - /volume1/paperless/export:/usr/src/paperless/export
      - /volume1/paperless/consume:/usr/src/paperless/consume
    environment:
      PAPERLESS_REDIS: #redis://192.168.1.123:6379
      PUID: #1027
      PGID: #65555
      USERMAP_UID: #1027
      USERMAP_GID: #65555
      PAPERLESS_TIME_ZONE: Europe/Berlin
      PAPERLESS_ADMIN_USER: #User
      PAPERLESS_ADMIN_PASSWORD: #Password
      PAPERLESS_OCR_LANGUAGE: deu+eng
    networks:
      default:
        ipv4_address: #192.168.1.124
        
networks:
  default:
    name: #Macvlan-Name
    external: true
```

