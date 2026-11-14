# KrabbzDev U1 Announcer

A Windows tray app for Snapmaker U1 printers. Alexa tells you when your print is done.

[![Download the installer](https://img.shields.io/badge/Download%20the%20installer-U1--Announcer1--Installer.exe-0048FE?style=for-the-badge&logo=windows&logoColor=white)](https://github.com/krabbzdev/KrabbzDev-SnapMaker-U1-Announcer/releases/latest/download/U1-Announcer1-Installer.exe)

## Why I built it

I wanted Alexa to tell me when a print finished. I didn't want to keep walking to the printer or checking my phone. This app does that. It also gives you a live dashboard of your printers, which grew out of the same idea.

## What it does

- **Alexa announcements:** Your Echo speaks up when a print finishes, fails, or is cancelled.
- **Live dashboard:** It shows progress, model preview, temperatures, filament, and recent prints. You can open it on the PC or on any phone or computer on your network.
- **Print controls:** You can pause, resume, and adjust speed, flow, fans, and the chamber light from the dashboard. Each control has an on/off switch in Settings.
- **Reports and recordings:** You can see how much you printed over 7 days, 30 days, or all time, and play the timelapse videos saved on your printers.
- **Windows notifications:** These show the printer, the print name, and how long it took.

## How the Alexa part works

Alexa can't be told to say a custom sentence on demand, so the app uses a workaround. It uses [Sinric Pro](https://sinric.pro/) to "ring" a virtual Doorbell. An Alexa routine you set up listens for that doorbell and says your phrase. I use two doorbells, one for finished prints and one for failed or cancelled prints.

You need a free Sinric Pro account. It's a separate third-party service, not part of this app. The app runs a small helper that keeps the doorbells connected, and that helper needs Node.js on the PC. The dashboard works fine without any of it.

The full Sinric Pro walkthrough (devices, App Key and Secret, linking the Alexa skill, building the routines) is in the [guide](https://github.com/krabbzdev/KrabbzDev-SnapMaker-U1-Announcer/blob/main/GUIDE.md).

## What you need

- A Windows PC that stays on and signed in, running the app on **one PC only**, or every announcement plays twice
- A fixed IP address (DHCP reservation) for each printer, so the app doesn't lose them after a router restart
- A free Sinric Pro account, [Node.js](https://nodejs.org), and an Echo with the Alexa app (for the announcements)

## Install

Download **U1-Announcer1-Installer.exe** from the [releases page](https://github.com/krabbzdev/KrabbzDev-SnapMaker-U1-Announcer/releases/latest). It needs no admin rights, starts with Windows, updates itself once a day, and keeps your settings between updates. The other `.exe` on the releases page is only for self-updating, so you can ignore it.

Full setup steps: [GUIDE.md](https://github.com/krabbzdev/KrabbzDev-SnapMaker-U1-Announcer/blob/main/GUIDE.md)

## Feedback

Use **Send feedback** in the app, or open an [issue](https://github.com/krabbzdev/KrabbzDev-SnapMaker-U1-Announcer/issues).

This repository only holds the downloads and the guide.
