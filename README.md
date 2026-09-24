# Subtitles-for-Plex
Adds subtitles to your movies or series easily.
I didnt find any web apps that did this for plex easily so i made one myself that i could use and now sharing it if anyone else needs something like this.

An easy-to-use, independent tool designed for your Plex media library to effortlessly add and manage subtitles. Whether you have local files ready to import or need to fetch missing subtitles.

### Features
**Any Language Support:** Easily select and download subtitles in any language you need.
**Local Imports:** Seamlessly import your own subtitle files or map existing subtitle directories.
**OpenSubtitles Integration:** Automatically pull high-quality subtitles directly from OpenSubtitles.
**Plex-Compatible:** Organizes and names files perfectly so Plex recognizes them instantly.


**⚠️ Disclaimer**
This is an independent, unofficial community project. It is not affiliated with, endorsed by, or associated with Plex, Inc. "Plex" is a registered trademark of Plex, Inc.



# Subtitles for Plex

> **Disclaimer:** Subtitles for Plex is an unofficial tool and is not affiliated with,
> endorsed by, or sponsored by Plex, Inc. "Plex" is a trademark of Plex, Inc.

A small self-hosted web app that adds subtitles in **your language** to the movies and
series in your Plex library. It finds them on OpenSubtitles, or takes subtitle files you
already have, and saves each one next to its video (`Movie (2010).en.srt`,
`Show.S01E02.de.srt`, …), where Plex picks it up automatically.

This started as a personal project for a home Plex server. It's shared here in case it's
useful to others too.

- **One file, no dependencies.** Needs only Python 3.8 or newer and runs on Linux, macOS,
  Windows, or a NAS with Python.
- **Browser interface.** Use it from any computer or phone on your network.
- **Matched to your exact file.** It looks up each video by its OpenSubtitles fingerprint
  first, so the subtitle timing fits your release. If there's no exact match, it falls
  back to title/year or show/season/episode.
- **Batch mode.** "Get all missing" works through a whole library, or through whatever
  the filter shows.
- **Imports subtitles you already have.** Drop a folder, files, or `.zip`s into the
  browser. Each one is matched to the right video, and you check the matches before
  anything is saved.
- **Readable characters.** Subtitles are converted to UTF-8, so accented letters display
  correctly in Plex.
- **70+ languages**, choosable in Settings.

## Requirements

- **Python 3.8+.** It's already installed on most Linux systems and on macOS. On Windows,
  get it from python.org.
- **A free OpenSubtitles.com account and API key.** In your profile, open **API
  consumers** → create one → copy the key. Free accounts get a limited number of
  downloads per day, and Subtitles for Plex shows how many you have left.
- **Access to your media folders,** with write permission, from the machine running
  Subtitles for Plex. The easiest place to run it is the Plex server itself.

## Quick start

```bash
python3 subtitles_for_plex.py
```

Open `http://localhost:8765`, or `http://<server-ip>:8765` from another device. Then fill
in **Settings**:

1. **Subtitle language**
2. **Media folders,** one per line, e.g. `/mnt/media/Movies`
3. **OpenSubtitles API key, username and password**
4. **Plex address and token** (optional). These enable the **Refresh Plex** button.
   Here's [how to find your token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/).

Settings are stored in `~/.config/subtitles-for-plex/config.json`, readable only by your user.
They are **not** kept in the app folder, so sharing the folder never shares your keys.

### Options

These are set as environment variables:

| Variable                           | Default                                    | Meaning                  |
|------------------------------------|--------------------------------------------|--------------------------|
| `SUBTITLES_FOR_PLEX_PORT`          | `8765`                                     | Port for the web page    |
| `SUBTITLES_FOR_PLEX_HOST`          | `0.0.0.0`                                  | Use `127.0.0.1` to allow this machine only |
| `SUBTITLES_FOR_PLEX_CONFIG`        | `~/.config/subtitles-for-plex/config.json` | Where settings are saved |
| `SUBTITLES_FOR_PLEX_PASSWORD`      | *(none)*                                   | Ask for this password before showing the page (any username) |
| `SUBTITLES_FOR_PLEX_ALLOWED_HOSTS` | *(none)*                                   | Extra host names you open it by, comma-separated, e.g. `plexbox.lan,subs.example.com` |
| `SUBTITLES_FOR_PLEX_ALLOW_PUBLIC`  | *(off)*                                    | Set to `1` to answer devices outside your local network (only behind a proxy with a login) |

With systemd, add them to the `[Service]` section, e.g.
`Environment=SUBTITLES_FOR_PLEX_PASSWORD=choose-something-long`.

## Run it as a service (Linux, systemd)

Copy the folder to your server, e.g. `/opt/subtitles-for-plex`. Edit `subtitles-for-plex.service` so that
`User` and the path match your setup, then:

```bash
sudo cp subtitles-for-plex.service /etc/systemd/system/
sudo systemctl enable --now subtitles-for-plex
```

## Media on a network share (SMB/CIFS)

If your videos live on a NAS, mount the share on the machine running Subtitles for Plex, and make
the mount writable for the user Subtitles for Plex runs as. Example `/etc/fstab` line:

```
//NAS-ADDRESS/SHARE  /mnt/media  cifs  credentials=/etc/smb-credentials,uid=USER-ID,gid=GROUP-ID,iocharset=utf8,nofail,_netdev  0  0
```

`/etc/smb-credentials` (with permissions `chmod 600`) contains:

```
username=...
password=...
```

## Using it

- **Missing / Has … / All** filters the list. A yellow dot means the video has no
  subtitle in your language yet.
- **Auto** fetches the best match for one video. **Choose…** lists every subtitle found
  so you can pick one yourself. The *Exact match* tag means it was made for your file.
- **Get all missing** processes everything in the current view. It stops when the daily
  download limit is reached.
- **Import subtitles…** reads `.srt`, `.ass`, `.ssa`, `.vtt`, `.smi` or `.zip` files from
  the device you're browsing on. Pick the language first, then check the matches. Unsure
  matches are left unticked, and existing subtitles are only replaced after you confirm.
- **Refresh Plex** asks Plex to rescan so new subtitles appear. If one still doesn't show
  up on a title, use **⋯ → Refresh Metadata** on it in Plex.

## Security

Subtitles for Plex is meant for your home network. It protects itself like this:

- **Local devices only.** It answers devices on your local network, a VPN, or the same
  machine. Requests from the internet are refused, even if the port is forwarded by
  mistake. `SUBTITLES_FOR_PLEX_ALLOW_PUBLIC=1` turns this off; only do that behind a
  reverse proxy that asks for a login.
- **Websites can't control it.** Web pages you visit can't use it through your browser.
  This covers both cross-site requests and "DNS rebinding", which is why it only answers
  to IP addresses, `localhost` and this machine's name. If you open it by another name,
  add that name to `SUBTITLES_FOR_PLEX_ALLOWED_HOSTS`.
- **Optional password.** Set `SUBTITLES_FOR_PLEX_PASSWORD` if other people use your
  network, such as housemates or guest Wi-Fi. It uses the browser's standard login box,
  which isn't encrypted on plain `http://`. Treat it as a lock against casual use, not
  as internet-grade security.
- **Secrets stay on the server.** Your OpenSubtitles key and password and your Plex token
  are never sent to the browser. The Plex token only goes to the Plex address it was
  entered with: if the address is changed, the token must be entered again.
- **Writes only subtitles.** It only writes subtitle files next to videos inside your
  media folders. It never follows symlinks, and it has size limits for uploads and zips.

Your OpenSubtitles password is stored in plain text in the config file (only your user
can read it), because it's needed to sign in. Use a password you don't use anywhere
else.

## Credits and disclaimer

Subtitles for Plex is an unofficial tool and is not affiliated with Plex, Inc. It is not
affiliated with OpenSubtitles either. "Plex" is a trademark of Plex, Inc., used here only
to describe what this tool works with.

Subtitles are provided by [OpenSubtitles.com](https://www.opensubtitles.com); please
respect their terms of use.

## License

MIT (see [LICENSE](LICENSE)).
