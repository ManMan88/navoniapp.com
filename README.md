# navoniapp.com

The static site for Navoni. Its one job for now is the privacy policy at `https://navoniapp.com/privacy`, which Google Play needs before the first upload.

- `index.html`: the "coming soon" landing page, in Hebrew then English. The scene is inline SVG, and there are no outside fonts, scripts or trackers.
- `privacy.html`: the policy, in Hebrew then English. GitHub Pages serves it at `/privacy`.
- `og.png`: the 1200 × 630 preview that WhatsApp and other apps show for a shared link, rendered from the landing page's scene.
- `favicon.svg`: Johnny's face.
- `fonts/`: Noto Sans Hebrew as woff2 (the app's font), under the SIL Open Font License in `fonts/NotoSansHebrew-OFL.txt`.
- `CNAME`: the custom domain.

## Publishing (GitHub Pages)

1. Create a **public** repository from this folder and push it:
   `gh repo create ManMan88/navoniapp.com --public --source . --push`
2. Repository Settings → Pages: source "Deploy from a branch", branch `master`, folder `/`. Custom domain `navoniapp.com`.
3. At GoDaddy (DNS for navoniapp.com): delete the two parked `A` records for `@` (3.33.130.190, 15.197.148.33) and any forwarding, then add:
   - `A @` → 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153
   - `AAAA @` → 2606:50c0:8000::153, 2606:50c0:8001::153, 2606:50c0:8002::153, 2606:50c0:8003::153
   - `CNAME www` → `manman88.github.io`
4. Optional but recommended: verify the domain under GitHub account Settings → Pages (a `TXT` record), so no other account can claim it.
5. When the certificate is issued (minutes to an hour), tick **Enforce HTTPS**.
6. Check: `curl -sI https://navoniapp.com/privacy` answers `200`.

## Keeping it true

The policy describes what the app does. Update it here **before** a build that changes that ships: backend sync, a network permission, a new profile field, or a change to Android backup.
