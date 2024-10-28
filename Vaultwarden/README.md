# Vaultwarden

## Why Vaultwarden?

Vaultwarden is an alternative implementation of the Bitwarden server API written in Rust and compatible with Bitwarden clients.
It has the base features of Bitwarden and also some free features that you have to pay for on Bitwarden. For example 2-factor-authentification (TOTP).

## Prerequisites

- [Portainer](https://www.portainer.io/)

## Installation Guide

For the installation i use a docker-compose file. To run it go to Portainer Stacks. You have to modify the comment variables before execution.

```yaml
version: "3.9"
services:
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: Vaultwarden
    restart: unless-stopped
    ports:
      - #35556:3012
      - #35554:80
    volumes:
      - #/volume1/docker/vaultwarden/data:/data:rw
    environment:
      PUID: #1027
      PGID: #65555
      ROCKET_PROFILE: release
      ROCKET_PORT: 80
      ROCKET_ADDRESS: 0.0.0.0
      ROCKET_ENV: staging
      RODCKET_WORKERS: 10
      DEBIAN_FRONTEND: noninteractive
      SIGNUPS_ALLOWED: true
      WEBSOCKET_ENABLED: true
```

After successful execution of the docker-compose file you have to [create a new account](#create-a-new-account).

## Create a new Account

To create a new account you have to call your defined ipv4_address via web-browser (for example: `192.168.1.123:35554`).

> [!CAUTION]
> Don't forget to [Disable SIGNUPS_ALLOWED](#disable-signups_allowed). If you don't do this, anyone who reaches the login-page can create an account.

## Disable SIGNUPS_ALLOWED

Stop the container and change the `SIGNUPS_ALLOWED` to `false` in the container settings.