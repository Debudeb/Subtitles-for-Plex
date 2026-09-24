This is all vibecoded

# Subtitles-for-Plex
Adds subtitles to your movies or series easily.
I didnt find any web apps that did this for plex easily so i made one myself that i could use and now sharing it if anyone else needs something like this.

An easy-to-use, independent tool designed for your Plex media library to effortlessly add and manage subtitles. Whether you have local files ready to import or need to fetch missing subtitles.

### Features
**Any Language Support:** Easily select and download subtitles in any language you need.
**Local Imports:** Seamlessly import your own subtitle files or map existing subtitle directories.
**OpenSubtitles Integration:** Automatically pull high-quality subtitles directly from OpenSubtitles.
**Plex-Compatible:** Organizes and names files perfectly so Plex recognizes them instantly.

<img width="1607" height="1025" alt="subforplex1" src="https://github.com/user-attachments/assets/d1dd72a0-02f4-4131-ad86-c54a7ac27956" />


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

- **Runs on Windows, Linux and macOS.** It's one Python file with nothing extra to
  install.
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

**Contents:** [Before you start](#before-you-start) ·
[Windows](#install-on-windows) · [Linux](#install-on-linux) · [macOS](#macos) ·
[First-time setup](#first-time-setup-in-the-browser) · [Options](#options) ·
[Using it](#using-it) · [Troubleshooting](#troubleshooting) · [Security](#security)

## Before you start

You need three things:

1. **A free OpenSubtitles.com account and API key.** Sign up at
   [opensubtitles.com](https://www.opensubtitles.com). Then open your profile, go to
   **API consumers**, create a new consumer (any name) and copy its **API key**. Free
   accounts can download a limited number of subtitles per day, and the app shows how
   many you have left.
2. **A computer that can reach your videos and change files there.** The easiest choice
   is the computer that runs your Plex server. Any computer on the same network works
   too, as long as it can open the folders your movies and series are in.
3. **Python 3.8 or newer.** The steps below show how to check and install it.

## Install on Windows

**1. Install Python** (skip this if you already have it)

- Download it from [python.org/downloads](https://www.python.org/downloads/) and run the
  installer.
- On the first screen, **tick "Add python.exe to PATH"**, then click **Install Now**.

**2. Download Subtitles for Plex**

- Download the project as a ZIP file. On GitHub, that's the green **Code** button →
  **Download ZIP**.
- Before unzipping, right-click the ZIP → **Properties** → tick **Unblock** (if you see
  it) → **OK**. This stops Windows from warning about the files later.
- Right-click the ZIP → **Extract All…** and pick a folder, e.g. `Documents\Subtitles for Plex`.

**3. Start it**

- Double-click **`start-windows.bat`** in that folder.
- A black window opens and your browser opens the app. **Keep the black window open**
  (you can minimize it); closing it stops the app.
- The first time, Windows Firewall asks whether Python may use the network. Tick
  **Private networks** only, then click **Allow**. This lets your phone and other
  computers at home open the app.
- If it says Python is not installed, repeat step 1, and make sure the PATH box is ticked.

**4. Set it up.** See [First-time setup in the browser](#first-time-setup-in-the-browser).
On Windows, media folders look like this:

- a folder on this PC: `D:\Movies`
- a folder on a NAS or another computer: `\\NAS-NAME\Movies` (or a mapped drive such as
  `Z:\Movies`)

**5. Optional: start automatically when you log in**

1. Press **Win + R**, type `shell:startup` and press **Enter**. A folder opens.
2. In another window, right-click `start-windows.bat` → **Show more options** →
   **Create shortcut**, then move the shortcut into the folder from step 1.
3. Right-click the shortcut → **Properties**:
   - add ` --no-browser` at the end of **Target** (so your browser doesn't pop up at
     every login)
   - set **Run** to **Minimized**
   - click **OK**

**Stop it** by closing the black window. **Uninstall** by deleting the folder and
`%APPDATA%\subtitles-for-plex`, where your settings are kept.

## Install on Linux

**1. Check Python.** Open a terminal and run:

```bash
python3 --version
```

If it says 3.8 or higher, you're set. If not, install it:

- **Debian / Ubuntu:** `sudo apt install python3`
- **Fedora:** `sudo dnf install python3`
- **Arch:** `sudo pacman -S python`

**2. Download Subtitles for Plex.** Download the ZIP (on GitHub: **Code → Download ZIP**)
and unzip it into a folder, e.g. `~/subtitles-for-plex`. Or use git:

```bash
git clone <repository-url> ~/subtitles-for-plex
```

**3. Start it**

```bash
cd ~/subtitles-for-plex
python3 subtitles_for_plex.py --open
```

`--open` opens your browser. Leave it out on a server without a screen. The terminal
shows the address to use from other devices, like `http://192.168.1.20:8765`. Press# Subtitles for Plex

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

**Ctrl+C** to stop it.

**4. Set it up.** See [First-time setup in the browser](#first-time-setup-in-the-browser).
On Linux, media folders look like `/mnt/media/Movies` or `/srv/plex/TV Shows`.

**5. If your videos are on a NAS (SMB/CIFS share):** mount the share first. The mount
must be writable for the user that runs Subtitles for Plex. Add a line like this to
`/etc/fstab`:

```
//NAS-ADDRESS/SHARE  /mnt/media  cifs  credentials=/etc/smb-credentials,uid=USER-ID,gid=GROUP-ID,iocharset=utf8,nofail,_netdev  0  0
```

Then create `/etc/smb-credentials` with your NAS login, and protect it with
`sudo chmod 600 /etc/smb-credentials`:

```
username=...
password=...
```

Mount it with `sudo mount -a`. You get `USER-ID` and `GROUP-ID` from the `id` command.
Install `cifs-utils` if the mount command is missing.

**6. Optional: start automatically (systemd)**

Move the folder to a permanent place, e.g. `/opt/subtitles-for-plex`. Open
`subtitles-for-plex.service` and change `User=` to your username (see `whoami`) and the
path on the `ExecStart=` line. Then:

```bash
sudo cp subtitles-for-plex.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now subtitles-for-plex
```

- Check that it's running: `systemctl status subtitles-for-plex`
- Watch its messages: `journalctl -u subtitles-for-plex -f`

**7. If you use a firewall (ufw),** let devices on your home network in. Adjust the
address range to match your network:

```bash
sudo ufw allow from 192.168.0.0/16 to any port 8765 proto tcp
```

Settings are kept in `~/.config/subtitles-for-plex/config.json`.

## macOS

Follow the Linux steps 2–4. macOS doesn't come with Python 3 ready to use. Get it from
[python.org](https://www.python.org/downloads/), or run `xcode-select --install`. Media
folders look like `/Volumes/Media/Movies`.

## First-time setup in the browser

The **Settings** panel opens by itself the first time. Fill in:

1. **Subtitle language:** the language you want subtitles in.
2. **Media folders:** the folders your movies and series are in, one per line.
3. **OpenSubtitles API key, username and password.**
4. **Plex address and token** (optional). These enable the **Refresh Plex** button, so
   new subtitles show up in Plex right away. The address is usually
   `http://localhost:32400` when the app runs on the Plex server. Here's
   [how to find your token](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/).

Click **Save & test**. The list of your videos appears below.

Your settings stay on the computer running the app. They are **not** kept in the app
folder, so sharing the folder never shares your keys.

## Options

Most people never need these. They're set as environment variables:

| Variable                           | Default          | What it does |
|------------------------------------|------------------|--------------|
| `SUBTITLES_FOR_PLEX_PASSWORD`      | *(none)*         | Ask for this password before showing the page (any username works) |
| `SUBTITLES_FOR_PLEX_PORT`          | `8765`           | Port for the web page |
| `SUBTITLES_FOR_PLEX_HOST`          | `0.0.0.0`        | Set `127.0.0.1` to allow only this computer |
| `SUBTITLES_FOR_PLEX_ALLOWED_HOSTS` | *(none)*         | Extra names you open it by, comma-separated, e.g. `plexbox.lan` |
| `SUBTITLES_FOR_PLEX_ALLOW_PUBLIC`  | *(off)*          | `1` = also answer devices outside your home network (only behind a proxy with a login) |
| `SUBTITLES_FOR_PLEX_CONFIG`        | *(see above)*    | Where settings are saved |

How to set them:

- **Windows:** open `start-windows.bat` in Notepad. Near the top, remove `rem ` in front
  of the line you want, change the value, and save.
- **Linux/macOS, one time:** `SUBTITLES_FOR_PLEX_PASSWORD=secret python3 subtitles_for_plex.py`
- **Linux, systemd:** add a line in the `[Service]` section of the service file, e.g.
  `Environment=SUBTITLES_FOR_PLEX_PASSWORD=choose-something-long`, then run
  `sudo systemctl daemon-reload && sudo systemctl restart subtitles-for-plex`.

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

## Troubleshooting

- **Other devices can't open the page.**
  - Use the "other devices" address shown in the black window or terminal, not `localhost`.
  - Make sure both devices are on the same network.
  - On Windows, the network must be set to **Private**: Settings → Network & internet →
    your connection → Network profile type. Allow Python through the firewall.
  - On Linux, see the firewall step.
- **"Unknown host name".** You opened it by a name it doesn't know. Use the IP address
  instead, or add the name to `SUBTITLES_FOR_PLEX_ALLOWED_HOSTS`.
- **"Folder not found or not mounted".** Check the path in Settings. For a NAS, make
  sure it's connected or mounted. On Windows, try the `\\NAS-NAME\Share` form.
- **"Could not save next to the video".** The user running the app can't write in that
  folder. On a NAS, check the share's permissions (Linux: the `uid=` in the mount line).
- **"Could not start on port 8765".** It's already running, maybe in another window, or
  something else uses that port. Close the other one or choose another port.
- **A subtitle was saved but Plex doesn't show it.** Press **Refresh Plex**, or in Plex
  use **⋯ → Refresh Metadata** on that title. Also check that **Use local assets** is on
  in the library's advanced settings.

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
