# Focus Player

Paste a YouTube link, watch that one video. No feed, no recommendations, no autoplay into the next thing.

## Why this exists

I block YouTube with a distraction blocker. The home feed, the sidebar and the "up next" queue are built to keep you watching, and for me they work too well.

But I'm learning, and a lot of good material only lives on YouTube: courses, conference talks, lectures, long technical videos people send me. Unblocking YouTube to watch one of them means walking straight back into the feed.

Focus Player is the middle ground. It plays a video **only if I already have its link**. There is nothing to browse:

- no home page, search, comments or related videos
- no autoplay into another video; when a video ends, the player is replaced with a "Video finished" panel
- pausing covers the player, so YouTube's "More videos" strip never shows
- it loads nothing from `youtube.com` itself, so the blocker can stay on

If you want the same thing, use the hosted page or fork the repo.

## Use it

1. Open the page.
2. Paste a YouTube link (or press <kbd>/</kbd> to jump to the input) and press Enter.
3. Pick a player width: S, M, L or Full. Your choice is remembered.

The page URL becomes `?v=<id>&t=<seconds>`, so you can bookmark a course video and come back to it.

On a phone, open the page and use "Add to Home Screen". It then opens full-screen like an app.

### Your blocker must allow

The player is served from YouTube's privacy-enhanced domain, so keep `youtube.com` blocked and allow:

- `youtube-nocookie.com` (the player)
- `*.googlevideo.com` (the video stream)
- `*.ytimg.com` (thumbnails and player assets)
- `noembed.com` (title and channel; optional, the player works without it)

## Run locally

YouTube refuses to play embeds from `file://` pages, so serve the folder:

```sh
python3 -m http.server 8000
# or: npx serve .
```

Then open http://localhost:8000.

To try it on a phone on the same Wi-Fi, open `http://<your-computer-ip>:8000`. The Paste button is hidden there, because browsers only allow clipboard access over HTTPS or on localhost.

## Deploy (GitHub Pages)

`.github/workflows/pages.yml` publishes the site on every push to `main`.

One-time setup:

1. Push this repo to GitHub.
2. In the repo, go to **Settings → Pages** and set **Source** to **GitHub Actions**.
3. Push again, or run the workflow from the **Actions** tab.

The site is then live at `https://<your-username>.github.io/<repo-name>/`.

## Details

- Accepted inputs: `watch?v=`, `youtu.be/`, `shorts/`, `embed/`, `live/`, `m.youtube.com`, `music.youtube.com`, or a bare 11-character video ID. Timestamps (`t=90`, `t=1m30s`) are honored. Playlists are ignored.
- If you pause in YouTube's own fullscreen, fullscreen moves to the page's player so the pause cover still shows. On iPhone, fullscreen uses Apple's native video player, where the page can't draw anything.
- YouTube has no setting to turn off the "More videos" strip, which is why the page covers the player while paused.
- Everything is one static `index.html` with no build step and no dependencies.

## License

[MIT](LICENSE)
