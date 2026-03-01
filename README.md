# scrobblescope

> Full-depth LastFM archive analyzer. Every scrobble, every stat, zero cutoffs.

---

ScrobbleScope is the current public implementation of what used to be **Wasted On Music**, a personal tool that started as a Python script and quietly got shelved. This version runs entirely in the browser, no server, no installs, just your API key and patience.

It pages through your *entire* scrobble history (200 tracks per request, rate-limited to stay inside Last.fm's API rules) and builds a real-time dashboard covering everything from total listening time to your most played 2am artist.

---

## Features

- Fetches **all scrobbles** with no page cap (tested past 194,000+)
- Auto-saves progress to localStorage every 50 pages so you can close and resume
- **Now Playing** live indicator and Last Played with relative timestamps
- Estimated total listening time (years / days / hours)
- Average scrobbles per day and average daily listening time
- Top tracks, artists, albums with play counts
- Listening distribution by hour, day of week, and year
- Export full history to CSV or JSON

---

## Getting Started

**1. Get a Last.fm API key**

Create a new LastFM API key at [last.fm/api/account/create](https://www.last.fm/api/account/create).   
If you had previously made one - head to [last.fm/api/accounts](https://www.last.fm/api/accounts) and grab a valid key.  
It takes about a minute and the key is free.

**2. Serve the file locally**

Opening `ScrobbleScope` directly from disk (`file://`) will hit CORS restrictions when the browser tries to reach the Last.fm API. Spin up a quick local server instead:

**Python (no install needed)**
```bash
# Python 3
python -m http.server 8080

# Python 2
python -m SimpleHTTPServer 8080
```
Then open [http://localhost:8080/index.html](http://localhost:8080/index.html).

**Node (if you prefer)**
```bash
npx serve .
```
Then open the URL it prints, usually [http://localhost:3000](http://localhost:3000).

**VS Code**
Install the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension, right-click `index.html`, and hit "Open with Live Server".

**3. Enter your credentials**

Paste in your username and API key, then hit Start. For large accounts (100k+ scrobbles) expect 5 to 20 minutes. The progress bar shows pages fetched in real time, and your session is saved automatically so interruptions are fine.

---

## Resuming a Scan

If the tab closes or you pause mid-fetch, check the "Resume from saved session" box on the next run. Your place is saved after every 50 pages.

---

## Estimated Listening Time

Duration data is not included in the recent tracks API response, so listening time is calculated using a 3.5 minute average per track. It is a reasonable estimate for most libraries. If you want exact durations, that would require a separate track info call per unique song, which is doable but slow at scale.

---

## Notes

- All data stays in your browser. Nothing is sent anywhere beyond the Last.fm API.
- The Last.fm API rate limit is 5 requests per second. ScrobbleScope runs at roughly 4.5 to stay safe.
- localStorage has a ~5MB cap. Very large exports should use the CSV/JSON export buttons.

---

## Origin

This project grew out of **Wasted On Music**, a private Python script for pulling and analyzing personal scrobble data. That version has since been deprecated. ScrobbleScope is the cleaner, browser-native successor.

---

## License

MIT

---

## Preview

![Connecting Account](https://i.imgur.com/yBZdGWl.png)    
![Dashboard](https://i.imgur.com/80vSrMW.png)   
![Dash2](https://i.imgur.com/L29hLAn.png)   
![Dash3](https://i.imgur.com/KeZVsN1.png)
