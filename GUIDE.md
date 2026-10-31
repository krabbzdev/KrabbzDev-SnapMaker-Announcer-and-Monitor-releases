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
- **Reports:** the **Reports** button shows how much you printed in the past 7 days, the past 30 days, or **all time** (everything the printers still have on record): prints, printing time and estimated filament, per printer and as a chart. Switch period with the buttons at the top of the report.
- **Speed control:** while a print is running or paused, the **−** and **+** next to *Speed / Flow*
  on its card change the print speed in 10% steps, from 50% to 150%. It's available to any device
  that can open the dashboard, so only share the address with people you trust. To turn it off, set
  `"AllowSpeedControl": false` in `settings.json`.
- **Recordings:** the **Recordings** button lists the timelapse videos saved on your printers, grouped by printer, and plays them in the page. They stream straight from the printer, so nothing is copied to the PC, and you can skip around or download them. The printers don't offer a live camera feed.
- **Chamber light:** the **lightbulb** on each printer's card (amber when the light is on, an outline when it's off) switches the chamber LED. Like speed control, anyone who can open the dashboard can use it. Turning the light off during a print leaves timelapse frames dark. To remove the button, set `"AllowLightControl": false` in `settings.json`.
- **Print controls:** on a printer's card, **Pause** and **Resume** appear while a print is running or paused. **Cancel** sits next to them, asks you to confirm first, and is **off by default** because a cancelled print can't be resumed. **Flow** (80% to 120%, steps of 5%) and the **Part** and **Chamber** fans (steps of 10%) have their own **−** and **+**. Each control has an on/off switch in **Settings → Dashboard controls**, together with the speed and light controls. A control that's switched off disappears from the dashboard and the app refuses it. Like speed, anyone who can open the dashboard can use these, so only share the address with people you trust. Heater temperatures, moving or homing the printer, emergency stop and restarts are left out on purpose.
- **Custom Monkeys:** your own dashboard buttons. Each one fires a [Voice Monkey](https://voicemonkey.io/) Routine Trigger, so an Alexa routine can switch a light or smart plug. In Voice Monkey, add a **Routine Trigger** and copy its ID, then build an Alexa routine that starts from it. In the app, open **Settings → Monkeys**, type a button name and paste the ID. Two slots (Action 1 and Action 2) are ready to fill in, and both buttons sit in the dashboard's top bar. A button without an ID is dimmed and tells you to add one when pressed. Each press counts against your Voice Monkey monthly quota, and anyone who can open the dashboard can press them. One checkbox hides them all.
- **Filament and firmware:** each toolhead tile shows the loaded filament type (hover for vendor and sub-type), and the firmware version is at the bottom of each printer's card. The printers don't report how much filament is left on a spool.
- **Estimated cost:** the green box under each print works out what its filament costs from the weight in the sliced file, against a 1000 g roll. Set your cost per roll in **Settings → Controls → Estimated cost** (it starts at $20), and the box's name shows it.
- **Double-clicking the tray icon:** in **Settings → App** you can choose whether it opens the dashboard window (the default) or a tab in your web browser.
- **Alexa on/off:** **Settings → Alexa → Announce on Alexa** switches spoken announcements off and
  on without losing your settings.
- **Updates** install themselves. If you turned automatic updates off, or an update fails, the app
  tells you when it's out of date: a notification, **Update now** in the tray menu and a note in
  the dashboard's lower right. The **Check for updates** button in the dashboard looks for a newer
  version from any device; installing is only offered on the PC running the app. After an update,
  click the notification to see what's new.
- **Edit Configurations** (dashboard top bar) opens the Settings window on the PC running the app.

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
| Something else | Right-click the tray icon → **Settings** → **App** → **Open log** to see what the app saw, or **Send feedback** to report it. |
