# Orange Box SP for PlayStation 4 🧡

**Half-Life 2, both Episodes, Portal and Half-Life: Source, running natively on PlayStation 4.**

The Orange Box never had a native PlayStation 4 version. This one is not an emulator and not a stream: it is the Source engine and Valve's own Linux game code, running on the PS4's CPU and GPU, with your DualShock 4 in hand. City 17, White Forest, the Aperture test chambers and Black Mesa, all from one app on your home screen.

> 🧪 **Early release.** This port has not been through full testing. Expect bugs: crashes, graphical glitches, a level that misbehaves. Reports help a lot (see *Contact* below), and the game sends anonymous crash reports by itself.

---

## ⚡ What You Get

* **One app, the whole single-player collection.** Pick the game from a list at start: Half-Life 2, Episode One, Episode Two, Portal, Half-Life: Source. Only the games you copied are shown.
* **The real games.** Valve's menus, chapters, saves and loading, the way they play on PC.
* **60 fps** with 4x MSAA in most of Half-Life 2.
* **A controller layout that feels right.** Radial dead zones, a response curve and turn acceleration for the right stick, and **gyro aiming** with the DualShock 4 (always on, or only while L2 is held).
* **Options on the console.** Stick feel, aim assist strength, gyro, frame rate cap, VSync, anti-aliasing.
* **Your language.** Text and voice follow the console's language when the localized files are in your game folder.

---

## ⚠️ Read Before Installing: No Game Content Included

The PKG contains **only** the engine and game binaries, a few configuration files, and the home-screen icon and background.
* **No game content** (maps, models, textures, sounds) from Valve is included.
* You **must** use your own files from legally purchased copies of the games on Steam.

---

## 🚀 Installation

You need: a PS4 with **GoldHEN**, a Windows PC or a Mac, and a Steam account that owns **Half-Life 2** (and the other games you want to play).

### The easy way: the installer (recommended)

1. From the **Releases** section of this repository download `OrangeBoxSP.pkg` and the installer for your computer:
   `OrangeBox-PS4-Installer-Windows.exe` or `OrangeBox-PS4-Installer-Mac.zip`.
2. Install the PKG on the PS4 with GoldHEN: **Settings → Debug Settings → Game → Package Installer**.
3. On the PS4, turn on the GoldHEN **FTP server** (GoldHEN menu → Server Settings → FTP).
4. Run the installer on your computer and answer its questions. It:
   * finds your PS4 on the network by itself;
   * downloads the right versions of your games with **SteamCMD**, Valve's official command-line Steam client.
     You type your Steam password and Steam Guard code into SteamCMD itself: the installer never sees or keeps them;
   * checks the files and uploads them to the PS4. If something breaks off, run it again: it continues where it
     stopped.
5. Start **Orange Box SP** on the PS4.

The download is about 10 GB, and the upload over Wi-Fi takes a while. The next time the installer remembers your
answers (never your password). At startup, choose **Change Steam Username** to enter a different login, or
**Reset Settings** to clear saved answers. Resetting asks for confirmation and does not delete downloaded game files.
If SteamCMD cannot download a game, the entered username is not saved and will not be reused on the next launch.

> **Windows:** SmartScreen may say *"Windows protected your PC"*, because the installer is not signed. Click
> **More info → Run anyway**.
>
> **Mac (Apple Silicon):** unzip, then right-click the file → **Open** → **Open**. If macOS still blocks it:
> System Settings → Privacy & Security → **Open Anyway**. SteamCMD needs Rosetta; the installer tells you if it is
> missing. On an Intel Mac, or if you prefer, run `installer/install_mac.command` from this repository (needs Python 3).

If the PS4 shows its help screen (*"No games found"* or *"… not found"*), scan its QR code with your phone: it opens this page.

### The manual way

You can do the same by hand.

In the end the console must have this:

```
/data/sourceeng/hl2         ← Half-Life 2 (required for every game)
/data/sourceeng/platform    ← Half-Life 2 (required)
/data/sourceeng/episodic    ← Half-Life 2: Episode One (optional)
/data/sourceeng/ep2         ← Half-Life 2: Episode Two (optional)
/data/sourceeng/portal      ← Portal (optional)
/data/sourceeng/hl1         ← Half-Life: Source (optional)
```

### Step 1. Download the LINUX version of the games (steam_legacy)
The PS4 runs the Linux build of the games, and only the Linux `hl2` folder has the shaders it needs. The Windows files of the very same version draw a broken picture. Steam on Windows downloads the Windows files, so use **SteamCMD**, Valve's official command-line Steam client:

1. Download SteamCMD for Windows: <https://steamcdn-a.akamaihd.net/client/installer/steamcmd.zip>
2. Unpack it to `C:\steamcmd`.
3. Open **Command Prompt** (press Win+R, type `cmd`, press Enter) and run:
   ```
   cd C:\steamcmd
   steamcmd +@sSteamCmdForcePlatformType linux +force_install_dir C:\hl2_linux +login YOUR_STEAM_LOGIN +app_update 220 -beta steam_legacy validate +quit
   ```
   Replace `YOUR_STEAM_LOGIN` with your Steam login. SteamCMD asks for your password and, if you use it, the Steam Guard code.
4. Wait until it says `Success! App '220' fully installed.` In `C:\hl2_linux` you now have `hl2` and `platform`.

`steam_legacy` is the version from **before the 20th Anniversary Update**. The newer version does not work with this port.

For the other games, run the same command with their own folder and app ID, and take the game's folder from there:

| Game | App ID | Branch | Folder to copy |
|---|---|---|---|
| Half-Life 2: Episode One | `380` | `-beta steam_legacy` | `episodic` |
| Half-Life 2: Episode Two | `420` | `-beta steam_legacy` | `ep2` |
| Portal | `400` | none (it has no steam_legacy) | `portal` |
| Half-Life: Source | `280` | none (it has no steam_legacy) | `hl1` |

Example for Episode Two: `... +force_install_dir C:\ep2_linux ... +app_update 420 -beta steam_legacy validate +quit`.
For Portal: `... +force_install_dir C:\portal_linux ... +app_update 400 validate +quit`. Half-Life 2 and the episodes
must be steam_legacy: their current version is the 20th Anniversary one, which does not work.

### Step 2. Install the PKG on the PS4
1. Download `OrangeBoxSP.pkg` from the **Releases** section of this repository.
2. Put it on a USB stick (FAT32 or exFAT) or send it to the console over FTP.
3. Install it with GoldHEN: **Settings → Debug Settings → Game → Package Installer**.

### Step 3. Copy the game files to the PS4
1. On the PS4, enable the GoldHEN **FTP server** (GoldHEN menu → Server Settings → FTP).
2. Find the console's IP address: **Settings → Network → View Connection Status**.
3. On the PC, open an FTP client such as [FileZilla](https://filezilla-project.org/) and connect:
   * Host: the PS4's IP address
   * Port: `2121`
   * No user name or password.
4. Go to `/data/` and create a folder named **`sourceeng`**.
5. Upload `hl2` and `platform` from `C:\hl2_linux` into `/data/sourceeng/`, and the folders of any other games you downloaded.

   This is several gigabytes. Wait until FileZilla reports that every transfer finished.

**Prefer USB?** FTP is not required: the game only needs the folders in `/data/sourceeng/`, however they get there.
Copy them to a USB stick (FAT32 or exFAT), plug it into the PS4 and use a homebrew file manager (for example
Itemzflow) to copy them from `/mnt/usb0/` into `/data/sourceeng/`, keeping the same folder names. The games cannot
run straight from the USB stick. The installer from *The easy way* always uploads over FTP.

### Step 4. Play
1. Start **Orange Box SP** from the PS4 home screen.
2. Pick a game from the list and press Cross.

### Something went wrong?

| What you see | What to do |
|---|---|
| **"No games found"** or **"Not ready"** screen | Read the list on that screen: it names the missing or wrong file. Fix it, press **Cross**, and the game checks again. |
| *"missing … .vpk"* or *"… is short (still copying?)"* | The copy is incomplete. Upload that file again. |
| *"Windows shaders: use the Linux hl2"* | Your `hl2` is the Windows version. Repeat Step 1 and replace the `hl2` folder. |
| *"shaders from the 20th Anniversary version"* | Your `hl2` is the new version. Repeat Step 1 (with `-beta steam_legacy`). |
| *"20th Anniversary files - use the older version"* | Delete the `hl2_complete` folder and use the files from Step 1. |
| White world, broken textures | Same cause: the Windows `hl2`. Repeat Step 1. |

If you are sure your files are right and the check is wrong, an empty file `/data/sourceeng/content_check_off.txt` turns the file checks off.

---

## 🛠️ Status & Compatibility

* **PlayStation 4 Slim (GoldHEN):** tested.
* **Other consoles (original PS4, PS4 Pro, PS5):** not tested. It may work, but nobody has tried yet. If you run it on one of them, please let me know how it went.
* **Known issues:** **Half-Life: Source has graphical bugs**; they will be fixed in a later update. In the other games some models show shading seams at mid distance, there are light outlines around foliage, and very busy scenes can drop below 60 fps.

---

## 📊 Crash Reports

To find and fix crashes, the game sends **anonymous** crash and hang reports and session counts (launches, play time, crash-free rate) to Sentry. There is no account, console or network information in them: a player is a random ID created on your console.

**To turn it off**, create an empty file `/data/sourceeng/telemetry_off.txt`.

---

## 🗺️ Roadmap

What we want to work on next. These are directions, not promises or dates.

* **Half-Life: Source graphics fixes.**
* **Graphics.** Shading seams on character models at mid distance, light outlines around foliage, flashlight shadows, texture shimmer in the distance.
* **Trophies** for the games' achievements.
* **More hardware.** Testing on the original PS4, PS4 Pro and PS5; 4K output on PS4 Pro and PS5.
* **Keyboard and mouse** support.
* **More Source mods** from the community.

Multiplayer lives in its own app: [Counter-Strike: Source for PS4](https://github.com/sausage88/CSS-PS4).

---

## ✉️ Contact
Questions, bug reports, results on other consoles: **apsausage@gmail.com**

---

## ⚖️ Disclaimer
This is a non-commercial fan project. It is not affiliated with, endorsed by, or connected to Valve Corporation or Sony Interactive Entertainment. Half-Life, Portal, The Orange Box and Steam are trademarks of Valve Corporation. PlayStation is a trademark of Sony Interactive Entertainment.

---

## Support the Project ☕
If you appreciate my work and want to support the development of this port and future homebrew projects for the PlayStation scene, feel free to drop a donation! It is completely optional but highly appreciated.

* USDT (Network: TRC-20): `TTWDNBNeMJmLyzf5CxhUqrgQynZDgAUZCz`
* Bitcoin (Network: BTC): `1NbMq2pqSR8zdFpLB4H4nQXbxPwzZctaVL`
* Ethereum (Network: ERC-20): `0x93cd7ebc2204a59d6ddd14870470b9069d3666ad`
* Litecoin (Network: LTC): `LN4L3zbrkmGyGKJjG97oWwQXq8ojZSWJAC`

Thank you for supporting the PlayStation Homebrew community! 🎮
