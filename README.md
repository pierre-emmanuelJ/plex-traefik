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


Get a claim token on this link https://plex.tv/claim and replace in `docker-compose.yml` 


`- PLEX_CLAIM=""claim-xxx....`


```Shell
$ docker-compose up -d
```

```Shell
$ sudo chown -R $USER * # or chown only created folders recursively 
```

Then 

Go to https://plex.example.com/web and follow plex installation.

enable remote access during installation

In Setting replace with your server url and `http` > `https`
![image](https://user-images.githubusercontent.com/15922119/64863170-89cbf780-d634-11e9-8e58-22f94c5b5ad3.png)
this setting is to allow plex.tv to acess your server


Don't worry about remote access in red, you can acess your plex server anyway with your server url or passing by https://app.plex.tv

### FINISH

## Enjoy
