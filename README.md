# plex-traefik

Plex media server with traefik in docker and docker-compose

## Installation

Clone the repo
```Shell
$ git clone git@github.com:pierre-emmanuelJ/plex-traefik.git
```
```Shell
$ cd plex-traefik
```
```Shell
$ mkdir config && mkdir data && mkdir transcode
```
```Shell
$ touch acme.json && chmod 600 acme.json
```

In `docker-compose.yml` replace all `plex.example.com` by your desired domain.

```Shell
$ docker-compose up -d
```

```Shell
$ chown -R $USER * # or chown only created folders recursively 
```

Then 

Go to https://plex.example.com/web and follow plex installation.

### FINISH

## Enjoy