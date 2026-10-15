# Claude FM Player: a full-window YouTube video as a Mac Dock app

## For an AI assistant reading this file
- Summarise what was done and why, using the sections below.
- Then guide the user step by step through "Setup on a new Mac".
- You can't click menus for the user. Give one step at a time.

## Objective
- Show one YouTube video ("Claude FM: music for thinking and building") filling a window.
- No YouTube header, search bar, labels or suggestions. Only the video.
- Run it as its own Safari web app (Dock icon) placed on one part of the screen.

## Live result
- Page: https://rashikkenn.github.io/claude-fm/
- Repo: https://github.com/Rashikkenn/claude-fm
- Video ID: `tRsQsTMvPNg`

## Why the simple approaches failed
- A Safari web app of youtube.com loads the full site. Resizing the window never removes the header.
- Pressing `f` in YouTube fills the whole display, not a chosen area.
- The embed URL (`https://www.youtube.com/embed/ID`) shows only the player. Opened directly in Safari it fails with Error 153 ("Video player configuration error"). Cause: YouTube receives no referrer (the address of the page showing the video).
- Fix used: a small page of our own, hosted at a real https address, that shows the embed full-window. That page supplies the referrer.

## Files in this repo
- `index.html`: the player page (code below).
- `icon.png`: the Dock icon (1024 x 1024). Drawn with code. The mascot shape was traced from a screenshot, so it may not match the official mascot exactly.
- `README.md`: this file.

## index.html (full code)
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Claude FM</title>
<link rel="apple-touch-icon" href="icon.png">
<style>
html, body { margin: 0; height: 100%; background: #000; }
iframe { width: 100%; height: 100%; border: 0; }
</style>
</head>
<body>
<iframe
  src="https://www.youtube.com/embed/tRsQsTMvPNg?autoplay=1&controls=0&rel=0"
  allow="autoplay; encrypted-media"
  referrerpolicy="strict-origin-when-cross-origin"></iframe>
</body>
</html>
```
- The `apple-touch-icon` line tells Safari which image to use as the app icon. Not yet confirmed to work (see Status).
- `controls=0` hides the control bar. `autoplay=1` starts playback. `rel=0` hides suggested videos.

## Setup on a new Mac (the page is already hosted)
Requirement: macOS Sonoma 14 or later. Older versions have no **File > Add to Dock**.
1. Open regular Safari (not an existing web app).
2. Go to https://rashikkenn.github.io/claude-fm/
3. Confirm the video fills the window. Click it once if it doesn't start.
4. Choose **File > Add to Dock**.
5. In the dialog, check the address is `rashikkenn.github.io/claude-fm` and not `youtube.com`.
6. Name it `Claude FM Player` and click **Add**.
7. Open the new app from the Dock. Confirm it shows only the video.
8. Drag the window to the wanted area. Resize until the video touches all four edges (video shape is 16:9). Black bars at the sides: window too wide. Bars at top and bottom: too tall.
9. Pause and play: click the video once, then press **Space**.

## Set a custom Dock icon (manual method)
1. Open `icon.png` in Preview. Press Cmd+A, then Cmd+C.
2. In Finder, open your home folder's **Applications** folder and select the web app.
3. Press Cmd+I. Click the small icon at the top-left of the info window.
4. Press Cmd+V. Quit and reopen the app if the Dock still shows the old icon.
- Deleting and re-adding the app resets the icon.

## Rebuild from scratch (new GitHub account or repo)
1. Create `index.html` in TextEdit. Use **Format > Make Plain Text** first. Paste the code above.
2. On GitHub: **+ > New repository**. Name `claude-fm`. Set **Public**. Click **Create repository**.
3. Click **uploading an existing file**. Drag in `index.html` and `icon.png`. Click **Commit changes**.
4. Go to **Settings > Pages**. Source: **Deploy from a branch**. Branch: `main`, folder `/ (root)`. Click **Save**.
5. Wait 1 to 2 minutes. Refresh **Settings > Pages** until it says "Your site is live at...".
6. Follow "Setup on a new Mac".

## Change the video
1. In YouTube, right-click the playing video and choose **Copy embed code**.
2. Paste it into Notes. Copy only the text inside `src="..."`.
3. Add `?autoplay=1&controls=0&rel=0` at the end. If the URL already has a `?`, use `&` instead.
4. Edit `index.html` on GitHub (pencil icon) and replace the `src` value. Click **Commit changes**.
- Some videos block embedding and show an error. No workaround is known.

## Known limits
- No visible pause button (`controls=0`). Use click then Space.
- Autoplay may be blocked by Safari until you click once.
- The web app's title bar may still show. Not known whether it can be hidden.
- The repo is public. Never store passwords, keys or private details in it.
- A local copy of `index.html` does nothing. Only the file on GitHub is served.
- Each GitHub upload triggers a rebuild of about 1 minute. Hard-refresh with Cmd+Shift+R.

## Status
- Confirmed: direct embed URL gives Error 153.
- Confirmed: GitHub Pages shows "Your site is live" at the address above.
- Not yet confirmed: the video plays on the hosted page.
- Not yet confirmed: Add to Dock opens the hosted page and shows only the video.
- Not yet confirmed: `apple-touch-icon` sets the Dock icon automatically.
- Update these lines after testing.
