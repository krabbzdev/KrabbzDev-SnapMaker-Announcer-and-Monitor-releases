# How to use SnapMaker Announcer and Monitor

One Windows app for Snapmaker U1 printers on your home network:

- **Announcer:** Alexa tells you when a print finishes, fails, pauses or is cancelled.
- **Monitor:** a live dashboard showing every printer's progress, model preview, temperatures,
  filament and recent prints, on this PC or any phone or computer on your network.

> **Alexa announcements use [Voice Monkey](https://voicemonkey.io/)**, a third-party service and
> Alexa skill (not part of this app) that lets apps make an Echo speak. You'll need a free Voice
> Monkey account. The dashboard works without it.

---

## ⚠️ Before you start: two things this app needs

### 1. Give each printer a fixed IP address (an "IP reservation")

The app finds your printers by their local IP address (for example `192.168.1.50`). By default,
your router can hand a printer a different address after a restart, and the app loses track of it
until you update the address in Settings.

To prevent that, set up a **DHCP reservation** (also called a *static IP reservation* or *static
lease*) for each printer in your router or firewall. That locks each printer to the same IP permanently.

1. Find each printer's IP address on its touchscreen (its network or Wi-Fi settings).
2. Sign in to your router or firewall's admin page and look for **DHCP reservation**, **Address
   reservation**, **Static lease** or **LAN → DHCP**. The wording varies by brand.
3. Pick the printer from the list of connected devices (or enter its MAC address) and reserve its
   current IP address. Save.
4. Restart the printer and check it comes back with the same address.

Not sure how? Search for your router's model plus "DHCP reservation".

### 2. Set up the Voice Monkey skill for Alexa

Announcements go through **Voice Monkey**, a free Alexa skill that lets apps make an Echo speak.

1. In the **Alexa app**, go to **More → Skills & Games**, search for **Voice Monkey**, enable it and
   link your account.
2. Sign in at [voicemonkey.io](https://voicemonkey.io) and create an **API token**
   (app.voicemonkey.io/tokens). You'll paste it into this app.
3. In Voice Monkey, create a **Speaker** device for each Echo that should talk. Note each one's
   **device ID**.
4. In the **Alexa app**, create one **routine per Echo**: **When this happens → Smart Home →** that
   Voice Monkey speaker, and set **From** to that Echo. Without its own routine, an Echo stays
   silent even though Voice Monkey reports the announcement as sent.

---

## Install

1. Download **SnapMaker-Announcer-and-Monitor.exe** from the
   [latest release](https://github.com/krabbzdev/KrabbzDev-SnapMaker-Announcer-and-Monitor-releases/releases/latest).
   There's no installer: the app runs wherever you put it and updates itself there.
   The recommended folder is `C:\Users\Public\Apps\KrabbzDev-U1-Monitor1`.
2. Run it. If Windows shows "Windows protected your PC", click **More info → Run anyway**.
3. When Windows Firewall asks about network access, click **Allow**, so phones and other PCs can
   open the dashboard.
4. Downloaded it somewhere else? Right-click the tray icon (near the clock) →
   **Move app to Public\Apps\KrabbzDev-U1-Monitor1**.

## Set up the app

The **Settings** window opens the first time you run the app. You can open it again any time from
the tray icon (right-click → **Settings**) or from the dashboard (**Edit Configurations**).

1. **Alexa:** paste your Voice Monkey **API token** and your **Echo device IDs** (separate several
   with commas), then click **Send test announcement**. Every Echo you listed should speak.
2. **Printers:** add each printer's name (what Alexa will call it) and its IP address, then click
   **Check printers**. Each one should show its status.
3. **Announcements:** choose which events to announce and edit the wording. You can use
   `{printer}`, `{name}` (the print), `{time}` (how long it ran) and `{filament}` (about how much it used).
4. Click **Save**.

**Start with Windows** is on by default, so the app runs whenever the PC starts. Keep that PC
awake and signed in, and run the app on **one PC only**, or every announcement plays twice.

## Everyday use

- **Dashboard:** opens by itself when the app starts. Double-click the tray icon or choose
  **Open dashboard** to open it again. To view it on a phone, use the address shown in
  **Settings → App** (the IP address version works best on phones).
- **Tray icon colour:** blue = printing, green = idle, red = error, grey = printer offline.
  Hover over it for each printer's status.
- **Updates** install themselves. After an update, click the notification to see what's new.

## Back up your settings

**Settings → App → Back up settings…** saves your API token, Echo IDs, printers and messages to a
file. Use **Restore settings…** to load it on a new PC or after a reinstall. The backup contains
your API token, so keep it somewhere private.

## Troubleshooting

| Problem | Try this |
|---|---|
| An Echo doesn't speak | Check that Echo has its own Alexa routine (see step 2 above), Do Not Disturb is off and the volume is up. |
| A printer shows **Offline** | Its IP address probably changed. Check it on the printer's screen, update it in **Settings → Printers**, and set up an IP reservation so it doesn't happen again. |
| Dashboard won't load on a phone | Use the IP address from **Settings → App**, and make sure the PC allowed the app through Windows Firewall. |
| Microsoft Defender blocks the download | Defender sometimes flags new, unsigned apps by mistake. Report it at [microsoft.com/wdsi/filesubmission](https://www.microsoft.com/wdsi/filesubmission) as "Incorrectly detected". On a work PC, check with your IT team first. |
| Something else | Right-click the tray icon → **Open log** to see what the app saw, or **Send feedback** to report it. |
