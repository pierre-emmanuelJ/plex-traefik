# plex-traefik

Run [Plex Media Server](https://www.plex.tv/) in Docker behind [Traefik v3](https://traefik.io/traefik/),
with HTTPS certificates from Let's Encrypt handled automatically.

- Plex is served at `https://plex.example.com`, and the Plex apps connect through it.
- HTTP is redirected to HTTPS.
- Every setting lives in a single `.env` file.

## Requirements

- Docker with the Compose plugin (`docker compose version`).
- A domain name (for example `plex.example.com`) with a DNS record pointing to your server.
- Ports **80** and **443** reachable from the internet, so Let's Encrypt can issue the certificate.
  Nothing else on the machine may already use them.

## Installation

1. Clone the repository:

   ```sh
   git clone https://github.com/pierre-emmanuelJ/plex-traefik.git
   cd plex-traefik
   ```

2. Create your settings file and edit it:

   ```sh
   cp .env.example .env
   ```

   | Variable           | What to put there                                                          |
   | ------------------ | -------------------------------------------------------------------------- |
   | `DOMAIN`           | Your Plex hostname, e.g. `plex.example.com`.                               |
   | `ACME_EMAIL`       | Your email, for the Let's Encrypt account.                                 |
   | `PLEX_CLAIM`       | A token from <https://plex.tv/claim>. It expires after 4 minutes, so get it right before step 4. |
   | `PLEX_SERVER_NAME` | The server name shown in the Plex apps.                                    |
   | `PUID` / `PGID`    | Your user and group IDs, from `id -u` and `id -g`.                         |
   | `TZ`               | Your time zone, e.g. `Europe/Paris`.                                       |
   | `MEDIA_PATH`       | The folder holding your movies, shows and music. It appears as `/data` in Plex. |

3. Create the data folders, so they belong to you rather than to root:

   ```sh
   mkdir -p config transcode data
   ```

4. Start the stack:

   ```sh
   docker compose up -d
   ```

5. Open `https://plex.example.com/web`, sign in, and add your libraries from `/data`.

The server is linked to your Plex account on its first start, thanks to the claim token.
You can remove `PLEX_CLAIM` from `.env` afterwards.

## Remote access

The Plex apps reach your server through `https://plex.example.com:443`
(the `ADVERTISE_IP` setting). In **Settings > Remote Access**, Plex may show remote access
in red because port 32400 is not open. You can ignore it: apps and
<https://app.plex.tv> still connect through Traefik.

## Updating

```sh
git pull
docker compose pull
docker compose up -d
```

Plex updates itself when its container restarts. Traefik follows the latest `v3.7.x` release.

## Local network devices

Port 32400 is published so that devices on your network can connect directly.
DLNA players, casting from local devices and network discovery need more ports.
They are listed and commented out in `docker-compose.yml`: uncomment the ones you need.

## Troubleshooting

- **Certificate errors.** Check `docker compose logs traefik`. Common causes: the DNS record does not
  point to this machine yet, or port 443 is blocked. While testing, set
  `ACME_CA_SERVER` to the staging URL in `.env` to avoid Let's Encrypt rate limits.
  Delete `letsencrypt/acme.json` when you switch back.
- **Permission errors in Plex.** Make sure `PUID`/`PGID` match the owner of `config`, `transcode` and
  your media folder.
- **Claim token expired.** Get a new one, put it in `.env`, then run `docker compose up -d --force-recreate plex`.

## Upgrading from the Traefik v2 version

Older versions of this repository used Traefik v2, a `Traefik/` folder and values hard-coded in
`docker-compose.yml`. To upgrade:

1. Create `.env` from `.env.example`, using the values you had in `docker-compose.yml`.
2. Run `git pull`. Your `config`, `data` and `transcode` folders are kept.
3. Run `docker compose up -d --remove-orphans`. Traefik requests a new certificate, so you can
   delete the old `Traefik/` folder.

## License

[MIT](LICENSE)
