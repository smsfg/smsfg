# SMSFG Website — Weekly Update Guide

**Southern Maine Senior Fun Group · smsfg.org**

---

## Overview

The website has two components that need to be updated each week:

1. **Google Sheets** (`SMSFG Website Data`) — holds the live data the site reads automatically
2. **index.html** — holds the config block with notes, week number, scorecard sheet IDs, and next round info

---

## Step 1 — Update Google Sheets (5 minutes)

1. Open `SMSFG Website Data.xlsx` on your PC
2. **Replace the Archive sheet** — copy the full Archive from your main Excel file (paste as values) and overwrite the existing one
3. **Add the new scorecard sheet** — copy the completed `Week - N` sheet from your main Excel file (paste as values), name it `Week - 1`, `Week - 2`, etc.
4. Upload `SMSFG Website Data.xlsx` to Google Drive, replacing the existing file
   - Google Drive will automatically convert it to Google Sheets format

---

## Step 2 — Get the new scorecard sheet GID (1 minute)

1. Open the converted Google Sheet on Google Drive
2. Click the new `Week - N` tab at the bottom
3. Look at the URL in your browser — copy the number after `gid=`
   - Example: `...#gid=1600606220`

---

## Step 3 — Update index.html (5 minutes)

Open `index.html` in a text editor and search for **`EDIT THIS SECTION`** to jump to the right place.

### Update the season info:
```javascript
currentWeek: 2,           // ← increment by 1
totalWeeks: 13,           // ← total weeks in season (doesn't change)
currentCourse: 'Spring Meadow Golf Club',  // ← this week's course
```

### Update the Notes:
```javascript
notesWeek: 2,             // ← match currentWeek
notes: `Your message to the group here.`,
```

### Add the new scorecard GID:
```javascript
const scorecardGids = {
  1: '1600606220',
  2: 'GID_FOR_WEEK_2',    // ← paste the GID from Step 2
};
```

### Update Next Round info:
```javascript
nextWeek: {
  available: true,         // ← set to false if foursomes not yet known
  weekNum: 3,
  date: '5/26/2026',
  course: 'Riverside Golf Club',
  tees: 'White',
  ctpHoles: [6, 13],
  foursomes: [
    { teeTime: '1:00 PM', hole: 1, players: ['Player A', 'Player B', 'Player C', 'Player D'] },
    { teeTime: '1:10 PM', hole: 1, players: ['Player E', 'Player F', 'Player G', 'Player H'] },
  ]
}
```

> **Note:** If a player name contains an apostrophe (e.g. O'Donnell), escape it with a backslash: `'Brendan O\'Donnell'`

> **Note:** If foursomes aren't known yet, set `available: false` and the site will show a "coming soon" message.

---

## Step 4 — Deploy to GitHub (2 minutes)

1. Go to [github.com](https://github.com) and open the `smsfg` repository
2. Click **Add file** → **Upload files**
3. Upload the updated `index.html`, replacing the existing one
4. Click **Commit changes**
5. Wait 1-2 minutes — check the **Actions** tab for the green checkmark
6. Hard refresh `smsfg.org` (`Ctrl+Shift+R` on Windows, `Cmd+Shift+R` on Mac) to verify

---

## Quick Reference — What Updates Automatically

| Item | How it updates |
|------|---------------|
| Season Standings | Automatically from Archive sheet |
| Weekly Results | Automatically from Archive sheet |
| Money Summary | Automatically from Archive sheet |
| Stat pills (weeks played, leader, etc.) | Automatically from Archive sheet |
| Scorecards | Automatically once GID is added to index.html |
| Course name on scorecards | Automatically from Archive sheet |
| Notes | Manually in index.html |
| Season band (week #, course) | Manually in index.html |
| Next Round foursomes | Manually in index.html |

---

## Troubleshooting

**Site shows old data after uploading**
Hard refresh your browser: `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)

**Site is blank / nothing loads**
There is likely a syntax error in index.html. Open the browser console (F12 → Console tab) and look for red errors. Most common cause: a missing `}` or a name with an apostrophe not escaped with `\'`

**Standings show NS for everyone**
The Archive sheet may not have uploaded correctly to Google Drive. Check that the file converted to Google Sheets format and the data is visible.

**Next Round page shows "coming soon"**
Check that `available: true` is set in the nextWeek config block.

---

*Site built and maintained by Mike. For issues contact Mike.*
