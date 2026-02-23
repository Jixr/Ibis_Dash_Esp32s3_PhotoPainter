# 🪶 Ibis Dash - Strava E-Paper Dashboard

This is my fork of the original project, updated to fix a few hardware compatibility issues, simplified code, and a few other QOL fixes. 

The original version can be found here
https://github.com/ibisette/Ibis_Dash_Esp32s3_PhotoPainter

This version is set up specifically for cycling.
I'm very happy with how my updated version turend out, and while I've spent the last several days reworking the original, future updates will come at a slower pace as I have many other projects and testing updates takes time.

I am not a professional software developer, just a hobbiest, so I cant guarantee anything, and there may be flaws in my code. I thought OP's idea was a great idea, just wanted to clean it up and take it a step further. 



An e-paper dashboard that shows your Strava stats. 



IBIS_v40.1 Changes
- The original code had a critical flaw where the device would run out of memory, showing errors and inccorect data on the screen. My version found another approach around that hardware limitation.
- Fixed flaw where if you recorded more than 1 activity before the screen refresh, or if the battery died completely, it wouldn't count it towards your goals. 
- Changed the "LATEST RIDE" to display the title of your last recorded strava activity ( Screen will update even if you change your activity title in strava afterwards )
- This version is set up for cycling: "pace" now displays "Avg. Speed"
- This will display ALL cycling activities ( Road cycling, MTB, Gravel, Cyclocross, E-bikes, and indoor rides/zwift ) 
- Lots of code logic & formatting fixes to simplify and make the display more stable and accurate.
- Default screen refresh is every 12 hours.
- Battery Life optimization: The device is set to pull the strava API every 12 hours, but the screen will only refresh if there is a new strava activity ( if you only ride once a week, this could potentially extend the battery life by weeks )
- Added a data point on the bottom right of the screen to show the Date of last screen refresh. ( easy way to tell if the device is working properly ) 

Future Updates
- Create activity specific versions ( running, swimming, etc ) 
- I'm testing a future update where the KEY button on the back of the screen will toggle through your different activity types ( running, swimming, cycling, etc. ) Though this may or may not be possible due to hardware limitations of the device.
- The board does have a connection for a RTC, so in theory it could be set to update at a specific time(s) of the day to help save battery life, and refresh the screen more quickly after an activity. ( example, if you typically ride in the mornings, you could have it refresh at noon, but not needlessly refresh in the middle of the night, or if you only tend to ride on the weekends, it would only power up from deep sleep mode on the weekends ) 
- I want to create a "USB MODE" so that when the screen is powered by usb-c, it will fetch strava request much more frequently. ( ie, every 30 mins on usb power, and then if removed off usb, go back to every 12 hours ) 
- I did attempt to add more data points to the screen ( elevation, power, heart rate, etc ) but it got too crowded, so I've left those out for simpliclity, but it is able to dispaly nearly any stat in strava if you so choose.

Hardware Mods:
  - The board does support an RTC, so adding one would enable even further battery optimization, ( example, have the screen refresh only during the day, and not in the middle of the night )
  - Battery: it uses a standard 5v 2 pin battery, so a larger one would easily give you months of battery life. With an RTC and my previous optimizations, I predict you could get 6+ month battery life pretty easily. 

---

## What It Does

Shows your cycling stats on a nice e-ink screen. Distance, time, activity count, your route, progress toward your yearly goal. Updates automatically. Runs on battery for weeks. Looks cool on your desk.

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
| USB Mode | USB-OTG" (TinyUSB) |

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
| KEY | Nothing. Reserved for a future update |
| BOOT | Force screen refresh and data fetch (the default 12-hour refresh counter will start after a manual refresh )|
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

Original code developed by Ibisette

Built with [GxEPD2](https://github.com/ZinggJM/GxEPD2), [ArduinoJson](https://arduinojson.org/), [XPowersLib](https://github.com/lewisxhe/XPowersLib), the Strava API, mass debugging, mass testing, and mass vibes.


---

## Remember, it doesn't count if its not on Strava
