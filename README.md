# plex-traefik

Plex media server with traefik in docker and docker-compose

## Installation

Clone the repo
```Shell
$ git clone https://github.com/pierre-emmanuelJ/plex-traefik.git
```

```Shell
$ cd plex-traefik
```

```Shell
$ mkdir config \
        && mkdir data \
        && mkdir transcode \
        && mkdir -p Traefik/etc/traefik \
        && mkdir -p Traefik/log
```

In `docker-compose.yml` replace all `plex.example.com` by your desired domain.


Get a claim token on this link https://plex.tv/claim and replace in `docker-compose.yml` 

`- PLEX_CLAIM=claim-xxx....`

/!\ important if you want Plex Apps access your server remotely:

Make sure to replace the env variable value `ADVERTISE_IP=https://<plex.example.com>:443` with your desired domain.

Run it now

```Shell
$ docker-compose up -d
```

```Shell
$ sudo chown -R $USER * # or chown only created folders recursively 
```

Then

Go to https://plex.example.com/web and follow plex installation.

enable remote access during installation

Don't worry about remote access in red, you can access your plex server anyway with your server url or passing by https://app.plex.tv


## Enjoy
