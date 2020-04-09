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
$ mkdir config && mkdir data && mkdir transcode
```
```Shell
$ touch acme.json && chmod 600 acme.json
```

In `docker-compose.yml` and `traefik.toml` replace all `plex.example.com` by your desired domain.


Get a claim token on this link https://plex.tv/claim and replace in `docker-compose.yml` 


`- PLEX_CLAIM=claim-xxx....`

Make sure to replace the env variable value `ADVERTISE_IP=https://plex.example.com`
with your desired domain.

/!\ important if you want Plex Apps access your server remotely.

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

Don't worry about remote access in red, you can acess your plex server anyway with your server url or passing by https://app.plex.tv

### FINISH

## Enjoy
