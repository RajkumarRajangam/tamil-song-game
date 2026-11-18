# Tamil Hitster — Android QR player test

Three song cards: `001` (Anjali Anjali), `005` (Why This Kolaveri Di?), `006` (Rowdy Baby). These track IDs are taken from the earlier 9-card test CSV; the user confirmed playback of the songs in the desktop prototype.

## Publish over HTTPS

1. Deploy `index.html` as a static website on a host that provides HTTPS, such as GitHub Pages, Netlify or Cloudflare Pages. **Do not** just open the file locally on Android.
2. Note the exact URL of the deployed page, e.g. `https://YOUR-SITE.example/index.html` or `https://YOUR-SITE.example/` (the slash matters).
3. In Spotify Developer Dashboard → your app → Settings → Redirect URIs, register the exact page URL **without** `?card=...`. Save. You can keep the desktop redirect URI as an additional entry.
4. Open the deployed page on Android Chrome with `?card=001` appended. Enter your Client ID and authorize Spotify. Connect browser player, then tap Play.
5. Repeat with `?card=005` and `?card=006`. A QR code should encode each complete HTTPS URL with its card query parameter. The page itself shows the full card URL in the QR testing section.

## Important limitations

- Android Chrome's DRM and Spotify SDK behavior may differ from desktop. Premium does not guarantee playback on every mobile browser.
- The Spotify app, system notifications, or lock screen may show the track title despite the page hiding it.
- The timer starts after Spotify acknowledges the play request, not necessarily at the exact audio onset. Pausing at 20 seconds is best effort.
- The `card` parameter only selects from the three preconfigured tracks; do not put Spotify access tokens or secrets in QR codes.
- The app stores OAuth tokens in `sessionStorage` for this prototype. For a production public game, add stronger session handling, content security policy and secure deployment controls.
- Playback must be initiated with a user tap; automatic playback on scanning is usually blocked by mobile browser policies.
- Spotify developer-mode user limits and app permissions still apply.
