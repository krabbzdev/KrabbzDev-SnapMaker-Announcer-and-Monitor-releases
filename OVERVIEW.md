# What it does and how it works

KrabbzDev's U1 Monitor and Alert Tool is a Windows tray app for Snapmaker U1 printers on your home network. It watches the printers, shows them on a live dashboard, and alerts you when a print finishes, fails, or is cancelled. Alerts come as Windows notifications and, if you set it up, as spoken announcements on an Echo.

## How it works

1. **Polling:** the app asks each printer for its status by local IP address, every 30 seconds by default (10 to 600 seconds is allowed).
2. **Dashboard:** it serves a web dashboard from the PC. Open it from the tray icon, or from any phone or computer on your network using the PC's IP address.
3. **Alerts:** when a print changes state, the app sends a Windows notification. If Alexa is enabled, it also passes the event to a small background helper that runs on Node.js.
4. **Alexa path:** Alexa can't be told to say a custom sentence on demand. The helper uses [Sinric Pro](https://sinric.pro/) to "ring" a virtual doorbell, and an Alexa routine you built says your phrase on your Echo.
   - There are two doorbells: **Print Finished** and **Print Failed**. Failed and cancelled prints both ring the second one.
   - Pauses never alert.

## Features

### Monitoring
- Progress, model preview, temperatures, loaded filament per toolhead (type, plus vendor on hover), firmware version and recent prints, for every printer.
- Estimated filament cost per print, based on the weight in the sliced file and your cost per roll (default $20 per 1000 g).
- **Reports:** prints, printing time and estimated filament over 7 days, 30 days or all time, per printer and as a chart.
- **Recordings:** a list of the timelapse videos saved on your printers, played by streaming from the printer, so nothing is copied to the PC.
- **Tray icon colors:** blue is printing, green is idle, red is error, grey is offline. Hovering shows each printer's status.

### Controls
- Pause and resume.
- Cancel, which asks you to confirm and is off by default because a cancelled print can't be resumed.
- Speed from 50% to 150% in 10% steps, flow from 80% to 120% in 5% steps, part and chamber fans in 10% steps, and the chamber light.
- Each control has its own on/off switch under **Settings → Controls**. A switched-off control disappears from the dashboard and the app refuses it.
- Heater temperatures, moving or homing, emergency stop and restarts are left out on purpose.

### Alerts
- Choose which outcomes alert you: finished, failed or cancelled. Unticking one stops both the Alexa doorbell and the Windows notification for it.
- Windows notification wording is editable, with placeholders for printer, print name, time and filament used.
- A test button rings the Finished doorbell to check the Alexa setup.

### App and settings
- Four settings tabs: Alexa, Printers, Controls and App.
- The installer needs no admin rights and includes Node.js. If Node.js is ever missing, the app downloads the official copy and checks its checksum.
- The app updates itself once a day and keeps your settings. You can also check by hand from the tray menu or the dashboard.
- Settings live in your Windows account's app-data folder, so updates, reinstalls and uninstalls don't erase them. You can back them up and restore them.
- It migrates settings from the older loose `.exe` versions. There is also a log viewer and a feedback form.

## Limits to know

- The dashboard controls have no password. Anyone who can open the dashboard can use them.
- The Sinric App Key and Secret are stored in plain text, and settings backups contain them.
- Run the app on one PC only, or every announcement plays twice.
- Alexa says a fixed phrase, so it can't name the printer. The Windows notification can.
- The printers don't report remaining filament and have no live camera feed.
- Each printer needs a fixed IP address (a DHCP reservation), or the app loses it after a router restart.

For setup steps, see the [guide](GUIDE.md).
