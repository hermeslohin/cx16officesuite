# The sync hub (ownCloud for the X16)

The X16 can't speak HTTPS, so a small **sync hub** runs on a Linux machine on your network. The X16
dials it over the **TexElec X16 Serial & ESP32 Network Card** (Zimodem firmware, Wi-Fi); the hub
talks to your **ownCloud** server.

```
X16 (serial/ESP32 card) --Wi-Fi/TCP 6502--> x16hub container --HTTPS--> ownCloud
```

* Documents (Write, Sheets, Files) live in ownCloud's **`Documents`** folder of the hub's account.
* The calendar syncs with an ownCloud calendar named **`X16`**.
* The hub is published as a container image for amd64 and arm64 (a Raspberry Pi 4/5 is fine):
  **`ghcr.io/hermeslohin/x16-office-hub:latest`**.
* Each X16 has its own secret key; the X16 and the hub prove to each other that they know it
  (HMAC-SHA256) before anything else happens. The link itself is **not encrypted**, so keep port
  6502 reachable only from your own network (step 7).

This is the short version. The complete guide with troubleshooting is
[INSTALL.md in the hub repository](https://github.com/hermeslohin/x16-office-hub/blob/main/INSTALL.md).

## What you need

* A Linux machine on the same LAN as the X16, with Docker Engine and the Compose plugin.
  (Docker Desktop on macOS/Windows works too, but sees every X16 as one address.)
* An **ownCloud** server reachable over **HTTPS** from that machine.
* An X16 with the TexElec serial/ESP32 card, on a Wi-Fi network that can reach the Linux machine.

## 1. Prepare ownCloud

1. Make a dedicated user, for example **`x16hub`** (Users, as an admin).
2. Sign in as that user: **Settings → Security → App passwords**, create one named `x16hub`, and
   **copy it** (it is shown once). The hub only ever uses this app password.
3. Find out which certificate to trust: a public certificate (Let's Encrypt) needs nothing; for
   your own CA or a self-signed certificate, save the CA certificate (PEM) as
   `~/x16hub/secrets/ca.pem` after step 2 below and check its fingerprint against your browser's.

## 2. Folders and the credentials file

```sh
mkdir -p ~/x16hub/secrets ~/x16hub/data ~/x16hub/sd-staging
chmod 700 ~/x16hub/secrets ~/x16hub/data ~/x16hub/sd-staging
nano ~/x16hub/secrets/owncloud.json          # an editor keeps the password out of your shell history
```

```json
{
  "base_url": "https://owncloud.example.lan",
  "username": "x16hub",
  "app_password": "paste-the-app-password-here",
  "ca_file": "/secrets/ca.pem"
}
```

Use `"ca_file": "/etc/ssl/certs/ca-certificates.crt"` for a public certificate. Then
`chmod 600 ~/x16hub/secrets/*`. The hub refuses to start if these files are readable by others.

## 3. Get the image

```sh
docker pull ghcr.io/hermeslohin/x16-office-hub:latest
```

## 4. Compose file

Save this as `~/x16hub/compose.yaml`:

```yaml
services:
  x16hub:
    image: ghcr.io/hermeslohin/x16-office-hub:latest
    container_name: x16hub
    restart: unless-stopped
    ports:
      - "0.0.0.0:6502:6502"
    user: "${X16HUB_UID:-1000}:${X16HUB_GID:-1000}"
    volumes:
      - ./secrets:/secrets
      - ./data:/data
      - ./sd-staging:/sd
    environment:
      X16HUB_LOG: INFO
    read_only: true
    tmpfs:
      - /tmp
    cap_drop: [ALL]
    security_opt:
      - no-new-privileges:true
    mem_limit: 512m
    pids_limit: 64
```

and tell Compose to run as you (the owner of the folders):

```sh
printf 'X16HUB_UID=%s\nX16HUB_GID=%s\n' "$(id -u)" "$(id -g)" > ~/x16hub/.env
```

Run every `docker compose` command from `~/x16hub`.

## 5. Test the ownCloud connection

```sh
docker compose run --rm x16hub oc check
```

Every line should say **PASS** (it writes, reads back and deletes a test file and a test event).

## 6. Connect the X16

**The key file.** Each X16 gets its own key. Use your hub machine's LAN address (or a DNS name your
Wi-Fi resolves) for `--host`:

```sh
docker compose run --rm x16hub link key new my-x16 --sdcard /sd --host 192.168.1.10:6502
cp ~/x16hub/sd-staging/X16LINK.KEY /path/to/the/sd/card/        # next to the apps
shred -u ~/x16hub/sd-staging/X16LINK.KEY
```

`my-x16` is the device name (up to 16 letters, digits, `-`, `_`). Anyone holding the SD card can
act as that X16; if a card is lost: `docker compose run --rm x16hub link key rm my-x16`.

**The ESP32 (once).** In a terminal program on the serial card:

```
ATW"<wifi name>,<wifi password>"     join your Wi-Fi
ATB115200                            115200 baud
AT&K3                                RTS/CTS flow control
AT&W                                 save
```

The apps dial the address in `X16LINK.KEY` themselves.

## 7. Firewall port 6502

Allow TCP 6502 **only from the network your X16's Wi-Fi is on** and drop it from everywhere else.
Docker-published ports bypass ufw/firewalld and ordinary `INPUT` rules: put the rule in Docker's
`DOCKER-USER` chain ([Docker's guide](https://docs.docker.com/engine/network/packet-filtering-firewalls/)),
matching `-m conntrack --ctorigdstport 6502 --ctdir ORIGINAL`, and make it survive reboots. The
hub also has its own allow-list (private LAN ranges by default).

## 8. Start it

```sh
docker compose up -d
docker compose logs -f
```

You should see `x16link listening on ('0.0.0.0', 6502)`. On the X16, use **Open / Save As → 2**
in Write or Sheets, the right pane of Files, or **Sync** in the Calendar; each connection shows in
the log. The hub also sets the X16's clock when it connects.

## Everyday tasks

| Task | Command (in `~/x16hub`) |
|---|---|
| Log | `docker compose logs -f` |
| Stop / start | `docker compose stop` / `docker compose up -d` |
| **Update to the newest hub** | `docker compose pull && docker compose up -d` |
| List X16s / add another | `docker compose run --rm x16hub link key list` / step 6 with a new name |
| Re-test ownCloud | `docker compose run --rm x16hub oc check` |
| Calendar sync status | `docker compose run --rm --entrypoint python x16hub -m x16hub.calsync status` |
| Calendar conflicts | `docker compose run --rm --entrypoint python x16hub -m x16hub.calsync conflicts` |

**Change the app password**: create a new one in ownCloud, put it in `secrets/owncloud.json`, run
`oc check`, `docker compose restart`, then revoke the old one in ownCloud.

**Back up** `~/x16hub/secrets` and `~/x16hub/data` together and keep the backup private (app password
and device keys). Your documents and calendar live in ownCloud.
