# Authentik

[Authentik](https://goauthentik.io/) setup using docker compose and [Traefik](https://traefik.io/traefik/) reverse proxy.

## Getting Started

Instructions for getting Authentik up and running.

### Prerequisites

Requirements for setup:
- [Docker Compose](https://docs.docker.com/compose/install/) installed
- Traefik up and running

> [!NOTE]
> [Traefik docker-compose here](/traefik/)

### Create files and directories

This is what the directory structure should look like when finished:

```
.
└── authentik
    ├── secrets
    │   ├── authentik_secret_key
    │   ├── postgres_db
    │   ├── postgres_password
    │   └── postgres_user
    └── docker-compose.yml
```

#### Docker compose

Copy the `docker-compose.yml` file into the Authentik directory.

> [!IMPORTANT]
> In the `docker-compose.yml` file update the lines with `authentik.your-domain.com` to your own domain name.

#### Create directories

Create the secrets directories in the Authentik directory:

```sh
mkdir secrets
```

Change permissions of the secrets directory to 600, owned by the user root and group root:

```sh
sudo chown root:root secrets/
sudo chmod 600 secrets/
```

#### Create the secret files

To create the files in the secrets directory, you will need root:

```sh
sudo su
```

> [!NOTE]
> The only thing to add to these files is the specific value for each.

Change into the secrets directory:

```sh
cd secrets
```

To generate a password for the postgres_password, use a secure password generator like openssl:

```sh
echo "$(openssl rand 36 | base64)" > postgres_password
```

Create and add the postgres_user with preferred editor:

```sh
vim postgres_user
```

Create and add the postgres_db with preferred editor:

```sh
vim postgres_db
```

To generate a key for the authentik_secret_key, use a secure password generator like openssl:

```sh
echo "$(openssl rand 60 | base64)" > authentik_secret_key
```

Exit from the root user when done:

```sh
exit
```

### Deploy

From the Authentik directory, deploy the docker container:

```sh
sudo docker compose up -d
```

Authentik will take some time to come up for the initial deployment.

When it's ready, you should be able to setup the admin account from https://authentik.your-domain.com/if/flow/initial-setup/