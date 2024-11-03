# Portainer

## Why Portainer?

[Portainer](https://www.portainer.io/) allows you to deploy container very easily but also in gread detail. I recommend using stacks with docker-compose for deployment. Portainer is necessary to build a [Macvlan](../Macvlan/README.md)

## Installation Guide

### Synology-DSM

- Create a `portainer` folder where you like to store the data (recommended within your docker directory)
- Install and open [Container Manager](https://www.synology.com/de-de/dsm/feature/container-manager)
- Select Tab `Container` and select `Create`
- Click on the Image-Dropdown, choose `Add image` and type `portainer-ce` into the search-box. Then select `portainer/portainer-ce` and click on `Download`
- Define a Container Name and choose `Next`
- Fill the port mapping
- Click on `Add Folder` and select your `portainer` folder
- Choose `Next` and `Done`