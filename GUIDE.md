# How to use SnapMaker Announcer and Monitor

One Windows app for Snapmaker U1 printers on your home network:

- **Announcer:** Alexa tells you when a print finishes, or fails or is cancelled.
- **Monitor:** a live dashboard showing every printer's progress, model preview, temperatures,
  filament and recent prints, on this PC or any phone or computer on your network.

> **Alexa announcements use [Sinric Pro](https://sinric.pro/)**, a third-party service and Alexa
> skill (not part of this app), plus a small helper that comes with the app. You'll need a free
> Sinric Pro account and [Node.js](https://nodejs.org). The dashboard works without any of it.
> Alexa says a short fixed phrase (you choose it), so it can't name the printer. The Windows
> notification still shows the printer, the print and how long it took.

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

### 2. Set up Sinric Pro for Alexa

Alexa can't be told to say a custom sentence, so the app uses a trick: it "rings" a virtual doorbell,
and an Alexa routine you set up says a short phrase when that doorbell rings. You need **two
doorbells**, one for finished prints and one for failed or cancelled prints. Sinric Pro's free plan
allows three devices.

**You'll need:** a free account at [sinric.pro](https://sinric.pro), the Alexa app and an Echo, and
[Node.js](https://nodejs.org) (the LTS version) on the PC that runs this app.

**a) Make the two doorbells**

1. Log in to Sinric Pro and open **Devices → Add Device**.
2. Name the first one **Print Finished** and set the type to **Doorbell**. Save.
3. Add a second one named **Print Failed**, also type **Doorbell**.
4. Copy each device's 24-character **ID** from the Devices page.
5. Open **Credentials** and copy your **App Key** and **App Secret**. Treat these like passwords: never
   paste them into a chat, an email or a screenshot.

**b) Link Sinric Pro to Alexa**

1. In the **Alexa app**, go to **More → Skills & Games**, search for **Sinric Pro** and tap **Enable to use**.
2. Sign in with your Sinric Pro login.
3. Say "Alexa, discover devices" and wait about 45 seconds. Both doorbells should now be under
   **Devices → All Devices**. If you created them after linking, say it again.

**c) Start the alert helper**

A Sinric Pro doorbell only counts as online while something on your side stays connected to it. The
app comes with a small helper that does that.

1. Open the `sinric-helper` folder that comes with the app, and run `npm install` in it, once.
2. Copy `config.example.json` to `config.json` and fill in your App Key, App Secret and the two device
   IDs. This file holds secrets, so keep it private. It is never uploaded.
3. Double-click `start-helper.cmd` and leave the window open. In Sinric Pro, both doorbells should
   turn from a red dot to green. If they stay red, check the App Key and App Secret.
4. To start the helper with Windows, press **Win + R**, type `shell:startup`, and put a shortcut to
   `start-helper.cmd` in the folder that opens.

**d) Build the two Alexa routines** (with the helper running, so the doorbells show as online)

1. In the **Alexa app**, go to **More → Routines → +**.
2. Under **When**, choose **Smart Home**, pick the doorbell (for example **Print Finished**) and
   choose the doorbell press as the trigger.
3. Under **Action**, choose **Alexa Says → Announcement**, type your phrase and choose your Echo.
   For example: "A print has finished." and "A print failed or was cancelled."
4. Save. Repeat for the other doorbell.

If Alexa also plays its own doorbell announcement, turn off that doorbell's notifications in the
Alexa app so you only hear your phrase once.

The helper has to be running for alerts to work. Finished prints ring **Print Finished**; failed and
cancelled prints ring **Print Failed**; pauses don't send an alert.

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

1. **Alexa:** make sure the alert helper is running, leave the **Alert helper address** as
   `http://127.0.0.1:8801` (change it only if you changed the port in `config.json`), then click
   **Send test announcement**. Your Echo should say the "finished" phrase.
2. **Printers:** add each printer's name (what Alexa will call it) and its IP address, then click
   **Check printers**. Each one should show its status.
3. **Announcements:** choose which events alert you. Alexa says the fixed phrase from its routine. The
   wording here is the Windows notification, and you can use `{printer}`, `{name}` (the print),
   `{time}` (how long it ran) and `{filament}` (about how much it used).
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
- **Filament and firmware:** each toolhead tile shows the loaded filament type (hover for vendor and sub-type), and the firmware version is at the bottom of each printer's card. The printers don't report how much filament is left on a spool.
- **Estimated cost:** the green box under each print works out what its filament costs from the weight in the sliced file, against a 1000 g roll. Set your cost per roll in **Settings → Controls → Estimated cost** (it starts at $20), and the box's name shows it.
- **Double-clicking the tray icon:** in **Settings → App** you can choose whether it opens the dashboard window (the default) or a tab in your web browser.
- **Alexa on/off:** **Settings → Alexa → Announce on Alexa** switches spoken alerts off and
  on without losing your settings.
- **Updates** install themselves. If you turned automatic updates off, or an update fails, the app
  tells you when it's out of date: a notification, **Update now** in the tray menu and a note in
  the dashboard's lower right. The **Check for updates** button in the dashboard looks for a newer
  version from any device; installing is only offered on the PC running the app. After an update,
  click the notification to see what's new.
- **Edit Configurations** (dashboard top bar) opens the Settings window on the PC running the app.

## Back up your settings

**Settings → App → Back up settings…** saves your helper address, printers and messages to a
file. Use **Restore settings…** to load it on a new PC or after a reinstall. Your Sinric Pro keys
live in the helper's `config.json`, not in this backup, so copy that file separately and keep it private.

## Troubleshooting

| Problem | Try this |
|---|---|
| An Echo doesn't speak | Check that the alert helper window is open and both doorbells are green in Sinric Pro, that each doorbell has its Alexa routine (see step 2 above) with the right Echo chosen, and that Do Not Disturb is off and the volume is up. |
| The app says it couldn't reach the alert helper | Start `start-helper.cmd`. If you changed the port in `config.json`, enter the same address in **Settings → Alexa**. |
| The doorbells stay red in Sinric Pro | The helper isn't running or can't sign in. Check the App Key, App Secret and device IDs in `config.json`. |
| A printer shows **Offline** | Its IP address probably changed. Check it on the printer's screen, update it in **Settings → Printers**, and set up an IP reservation so it doesn't happen again. |
| Dashboard won't load on a phone | Use the IP address from **Settings → App**, and make sure the PC allowed the app through Windows Firewall. |
| Microsoft Defender blocks the download | Defender sometimes flags new, unsigned apps by mistake. Report it at [microsoft.com/wdsi/filesubmission](https://www.microsoft.com/wdsi/filesubmission) as "Incorrectly detected". On a work PC, check with your IT team first. |
| Something else | Right-click the tray icon → **Settings** → **App** → **Open log** to see what the app saw, or **Send feedback** to report it. |
