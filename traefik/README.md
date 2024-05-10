# Traefik

[Traefik](https://traefik.io/traefik/) setup using docker compose and [Cloudflare](https://www.cloudflare.com/).

## Getting Started

Instructions for getting Traefik up and running.

### Prerequisites

Requirements for setup:
- [Docker Compose](https://docs.docker.com/compose/install/) installed
- [Cloudflare](https://www.cloudflare.com/) account and DNS records setup

### Create files and directories

This is what the directory structure should look like when finished:

```
.
└── traefik
    ├── logs
    ├── secrets
    │   ├── .htpasswd
    │   ├── cloudflare_dns_api_token
    │   └── cloudflare_zone_api_token
    ├── acme.json
    ├── config.yml
    ├── docker-compose.yml
    └── traefik.yml
```

#### Create docker compose and configs

- Copy the `config.yml` file into the Traefik directory
- Copy the `traefik.yml` file into the Traefik directory
- Copy the `docker-compose.yml` file into the Traefik directory

> [!IMPORTANT]
> Edit the lines with `traefik.your-domain.com` to your own domain name in the docker-compose file.

#### Create acme.json

First create the empty acme.json file in the Traefik directory:

```sh
touch acme.json
```

Next change the permissions to 600:

```sh
sudo chmod 600 acme.json
```

#### Create directories

Create the logs and secrets directories in the Traefik directory:

```sh
mkdir logs secrets
```

Change permissions of the secrets directory to 600, owned by the user root and group root:

```sh
sudo chown root:root secrets/
sudo chmod 600 secrets/
```

##### Create the secret files

To create the files in the secrets directory, you will need root:

```sh
sudo su
```

> [!NOTE]
> The only thing to add to these files is the specific API token from Cloudflare.

Change into the secrets directory:

```sh
cd secrets
```

Create and add the Cloudflare DNS token with preferred editor:

```sh
vim cloudflare_dns_api_token
```

Create and add the Cloudflare Zone token with preferred editor:

```sh
vim cloudflare_zone_api_token
```

Exit from the root user when done:

```sh
exit
```

##### Create basic auth password

Use the Apache Utilities Package to create the basic auth password file.

First update the server's package index:

```sh
sudo apt update
```

Install the Apache Utilities package:

```sh
sudo apt install apache2-utils
```

With this installed the `htpasswd` file can be created within the `./secrets` directory.

Specify the username to use at the end of the command:

```sh
sudo htpasswd -c ./secrets/.htpasswd jason
```

You will be asked to supply and confirm a password for the user.

If you check the contents of the file, it will contain the username and the encrypted password:

```
jason:ABCabc123!@#
```

### Docker network

A Docker network will need to be created. To check current networks:

```sh
sudo docker network ls
```

Create the Docker network defined in the docker-compose file:

```sh
sudo docker network create proxy
```

The `proxy` network should now be listed when checking the networks.

### Deploy

From the Traefik directory, deploy the docker container:

```sh
docker compose up -d
```

Traefik should now be running at traefik.your-domain.com