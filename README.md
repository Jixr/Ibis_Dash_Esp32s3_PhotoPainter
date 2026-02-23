# 🪶 Ibis Dash - Strava E-Paper Dashboard

An e-paper dashboard that shows your Strava stats. Written with a ton of frustration, mass amounts of trial and error, and the help of Claude. But hey, it works now!

Changes from Original

- The original code was limited by the ram of the device, if you had too many strava activities, it would display a "0" for all stats, My version uses a different method of pulling the strava API data to get around the hardware limitations.
- I simplified some of the code to reduce the size of the .ino file
- Updated/Fixed some formatting issues in the original code.
- My version is cycling specific, I changed the "pace" display to "Avg. Speed"
- Changed "LATEST RIDE" to display the title of your last strava event, not the date of the event. ( The screen WILL update if you change the title of your event later in strava )
- Adjusted the GPS dispaly route to not be cut off by the screen
- Made some changes so that the Distance Goal, Total Rides, Time, were updated more accurately.
- Fixed an error where if you recorded more than 1 strava activity before the screen refreshed, it wouldn't count it towards your distance goal.
- Default code is set to refresh the screen every 12 hours ( timer starts from when you upload the code )
- Screen will dispaly ALL ride types ( Road bike, mountain bike, Gravel, E-Bike ) and also included Indoor cycling ( zwift, peleton, etc )
- Clarified some of the installation instructions.
- Bypassed the requirement for the ibis.exe file, so in theory, this should work on MacOS as well. ( Though I've not tested it personally, as I don't have a MacOS Device ) 
  
---

## What It Does

Shows your strava activity stats on a nice e-ink screen. Distance, time, activity count, your route, progress toward your yearly goal. Updates automatically. Runs on battery for weeks. Looks cool on your desk.

That's it. That's the project.

---

## What I Used

- **Waveshare ESP32-S3-PhotoPainter** - comes with the 7.5" color e-paper display already attached, LiPo battery, and USB-C cable all included
- **Arduino IDE** - free
- **A Strava account** - you probably have one if you're here

---

## How Hard Is This?

Most of the code is set up, ready to go. 

There are a few lines of copy/paste code you'll need to upload, and the screen can be a bit tricky at times to get recognized by your pc. 

The "hardest" part is getting Strava API credentials, and even that takes like 5 minutes.

---

## Setup (The Short Version)

1. Install Arduino IDE
2. Add ESP32 board support
3. Install some libraries (GxEPD2, ArduinoJson, XPowersLib, QRCode)
4. Set the right board settings (see below - this part matters!)
5. Upload `IBIS_V31.ino` to your board
6. Open `Ibis.exe`, connect, enter WiFi + Strava credentials
7. Done. Go for a run.

---

## Arduino IDE Settings

⚠️ **Get these right or your board will be sad:**

| Setting | Value |
|---------|-------|
| Board | ESP32S3 Dev Module |
| USB CDC On Boot | Disabled |
| Flash Mode | **DIO** (NOT OPI!) |
| Flash Size | 16MB (128Mb) |
| PSRAM | OPI PSRAM |
| Partition Scheme | 16M Flash (3MB APP/9.9MB FATFS) |

The Flash Mode one is important. Ask me how I know.

---

## Getting Strava API Stuff

1. Go to [strava.com/settings/api](https://www.strava.com/settings/api)
2. Create an app (name it whatever, set callback domain to `localhost`)
3. Copy the Client ID and Client Secret into the Ibis Setup app
4. Click "Get Refresh Token" - it opens a browser, you authorize, done

---

## Buttons

| Button | What it does |
|--------|--------------|
| KEY | Nothing ( though will be used in a future update to toggle activity types ) |
| BOOT | Force screen refresh and data fetch |
| PWR | Hold Power on/off |

---

## What's In Here

```
ibis-dash/
├── firmware/
│   ├── IBIS_V31.ino    ← The Arduino code
│   └── ibis_logos.h    ← Pixel art logos (yes I made these)
├── app/
│   ├── Ibis.exe        ← Windows setup app
│   └── Ibis.py         ← Python source if you're curious
├── docs/
│   └── USER_MANUAL.md  ← More detailed instructions if you get stuck
├── README.md           ← You are here
└── LICENSE             ← MIT-ish, see below
```

---

## Why "Ibis"?

Because, believe it or not, I am a bird. 🪶

---

## License

MIT - use it, modify it, make it better. Just don't make it commercial without my consent.

---

## Credits

Built with [GxEPD2](https://github.com/ZinggJM/GxEPD2), [ArduinoJson](https://arduinojson.org/), [XPowersLib](https://github.com/lewisxhe/XPowersLib), the Strava API, mass debugging, mass coffee, and mass vibes.

Shoutout to Nerdland and some fellow nerds. 🤓

---

Happy tracking! 🏃‍♂️🪶
