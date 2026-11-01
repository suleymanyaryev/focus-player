# Focus Player

Paste a YouTube URL, watch that one video. No feed, no recommendations.

## Run

YouTube refuses to play embeds from `file://` pages, so serve the folder:

```sh
python3 -m http.server 8000
# or: npx serve .
```

Then open http://localhost:8000.

### On your phone

- **Same Wi-Fi, quick test:** open `http://<your-mac-ip>:8000`. The Paste button is hidden there, because browsers only allow clipboard access on HTTPS or localhost.
- **Everyday use:** host the folder on any free static HTTPS host (GitHub Pages, Netlify, Cloudflare Pages), then use "Add to Home Screen". It opens full-screen like an app.

## Notes

- Embeds come from `youtube-nocookie.com`. The page loads no scripts from `youtube.com`, so it works even if your blocker covers `youtube.com`, as long as it lets `youtube-nocookie.com`, `*.ytimg.com` and `*.googlevideo.com` through.
- When a video ends, the player is replaced with a "Video finished" panel so YouTube's end-screen suggestions never appear.
- Title and channel come from noembed.com. If that fails, the player still works.
- Accepted inputs: `watch?v=`, `youtu.be/`, `shorts/`, `embed/`, `live/`, `m.youtube.com`, or a bare 11-character ID. Timestamps (`t=90`, `t=1m30s`) are honored. Playlists are ignored.
- The page URL becomes `?v=<id>&t=<seconds>`, so you can bookmark a course video.
