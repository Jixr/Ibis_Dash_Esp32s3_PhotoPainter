# 🪶 Ibis Dash - Strava E-Paper Dashboard

This is my fork of the original project, updated to fix a few hardware compatibility issues, simplified code, and a few other QOL fixes. 

An e-paper dashboard that shows your Strava stats. Written with a ton of frustration, mass amounts of trial and error, and the help of Claude. But hey, it works now!

The original version can be found here
https://github.com/ibisette/Ibis_Dash_Esp32s3_PhotoPainter

---

## What It Does

Shows your running/cycling/swimming/hiking/walking stats on a nice e-ink screen. Distance, time, activity count, your route, progress toward your yearly goal. Updates automatically. Runs on battery for weeks. Looks cool on your desk.

That's it. That's the project.

---

## What I Used

- **Waveshare ESP32-S3-PhotoPainter** - comes with the 7.5" color e-paper display already attached, LiPo battery, and USB-C cable all included
- **Arduino IDE** - free
- **A Strava account** - you probably have one if you're here ( no strava subscription required ) 

---

## How Hard Is This?

There is some extremely minor copy/paste editing you'll need to do in the code and while connected to Arduino IDE. 

---

## Setup (The Short Version)

1. Install Arduino IDE
2. Add ESP32 board support
3. Install some libraries (GxEPD2, ArduinoJson, XPowersLib, QRCode)
4. Set the right board settings (see below - this part matters!)
5. Upload `IBIS_V40.1.ino` to your board
6. Copy/Paste in some code to import your wifi, strava, and goal settings.
7. Done. Go for a ride.

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
| 

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
| KEY | Absolutely nothing. In a future update it will cycle through your different activity types (running, swimming, cycling, etc. ) |
| BOOT | Force screen refresh and data fetch |
| PWR | Power on/off |

---

## What's In Here

```
ibis-dash/
├── firmware/
│   ├── IBIS_V40.1.ino    ← The Arduino code
├── docs/
│   └── USER_MANUAL.md  ← More detailed instructions if you get stuck
├── README.md           ← You are here
└── LICENSE             ← MIT-ish, see below
```

---

## License

MIT - use it, modify it, make it better. Just don't make it commercial without my consent.

---

## Credits

Built with [GxEPD2](https://github.com/ZinggJM/GxEPD2), [ArduinoJson](https://arduinojson.org/), [XPowersLib](https://github.com/lewisxhe/XPowersLib), the Strava API, mass debugging, mass coffee, and mass vibes.

Shoutout to Nerdland and some fellow nerds. 🤓

---

Happy tracking! 🏃‍♂️🪶
