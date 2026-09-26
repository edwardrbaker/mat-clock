# Mat Clock

A wrestling practice round timer that pairs partners every round and, when there's an odd number of wrestlers, rotates who rests so everyone gets a break at regular intervals. It installs to a phone's home screen and works offline.

## Deploy with GitHub Pages

1. Create a new GitHub repository (public, or private on a plan that includes Pages).
2. Upload everything in this folder, including the hidden `.github` folder, to the `main` branch:
   ```bash
   git init && git add . && git commit -m "Mat Clock"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
3. In the repo, go to **Settings → Pages** and set **Source** to **GitHub Actions**.
4. Open the **Actions** tab. If the first run failed because Pages wasn't turned on yet, click **Re-run jobs**.
5. Your app is live at `https://<you>.github.io/<repo>/`.

Every push to `main` redeploys. The workflow stamps the commit into the service worker, so installed copies pick up the new version the next time they open with a connection.

## Install on a phone

- **iPhone / iPad (Safari):** open the link → Share → **Add to Home Screen**.
- **Android (Chrome):** open the link → tap **Install app** in Practice setup, or ⋮ → **Install app**.

Open it once while online. After that it runs offline.

## Files

| File | What it does |
| --- | --- |
| `index.html` | The whole app: timer, pairing, rest rotation, voice alerts |
| `manifest.webmanifest` | App name, icons and full-screen display for installing |
| `sw.js` | Service worker that caches the app so it works offline |
| `icons/` | Home-screen and browser icons |
| `.github/workflows/deploy.yml` | Builds and deploys to GitHub Pages on every push to `main` |

## Notes

- The roster and settings are saved on each device. Two phones don't share a roster.
- Service workers need HTTPS (or `localhost`). To test locally: `python3 -m http.server 8080` in this folder, then open `http://localhost:8080`.
- iPhones won't play sound when the ring/silent switch is set to silent. Vibration works on Android only.
