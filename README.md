# HarvestTime invite site

Static pages for HarvestTime invite links. Messenger and other apps only turn `http(s)` URLs into links, so the game
shares `https://<pages-host>/join/#c=<HTR1 code>`. `join/index.html` reads the code from the URL fragment and opens the
app (`intent://...` on Android, `harvesttime://join?c=...` elsewhere). It also has a "Copy invite code" fallback.

Privacy: the code stays in the `#fragment`, which browsers never send to the server. The page has no analytics, no
external scripts or fonts, and makes no network requests (a CSP blocks them).

## Deploy to GitHub Pages
1. Create a repo (for example `harvesttime`) and push the contents of this folder to its root (`index.html`, `join/`, `.nojekyll`, this README).
2. On GitHub: Settings > Pages > Build and deployment > Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
3. Wait for the site at `https://<user>.github.io/<repo>/`. Test `https://<user>.github.io/<repo>/join/#c=HTR1.test` (it should say the link looks incomplete).
4. In the Unity project, set `InviteLink.WebBase` (Assets/Scripts/Network/Internet/InviteLink.cs) to `<user>.github.io/<repo>` (no scheme, no trailing slash) and rebuild.

## TODO
- Replace the `#TODO-get-harvesttime` links with the real store/download URL.
- If the Android package id changes, update `ANDROID_PACKAGE` in `join/index.html` (now `com.DefaultCompany.urp_2d`).
