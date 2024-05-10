# Baikal

[Baikal](https://sabre.io/baikal/) setup using docker compose and [Traefik](https://traefik.io/traefik/) reverse proxy.

## Getting Started

Instructions for getting Baikal up and running.

### Prerequisites

Requirements for setup:
- [Docker Compose](https://docs.docker.com/compose/install/) installed
- Traefik up and running
  - Traefik docker compose repo here

### Installing

#### Docker compose

- Copy the docker-compose.yml file into the directory used for Baikal
- Edit the lines with `baikal.your-domain.com` to your own domain name

#### Directory setup

Create the directories for the config and database in the directory used for Baikal:

```sh
mkdir config Specific
```

This is what the directory structure should look like when finished:

```
.
└── baikal
    ├── config
    ├── Specific
    └── docker-compose.yml
```

#### Deploy

From the Baikal directory, deploy the docker container:

```sh
docker compose up -d
```

Baikal should now be running at baikal.your-domain.com