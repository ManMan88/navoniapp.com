# navoniapp.com

The static site for Navoni. Its one job for now is the privacy policy at `https://navoniapp.com/privacy`, which Google Play needs before the first upload.

- `privacy.html`: the policy, in Hebrew then English. GitHub Pages serves it at `/privacy`.
- `index.html`: a one-line landing page that links to it.
- `CNAME`: the custom domain.

## Before publishing

Fill the four placeholders in `privacy.html`: the developer name (as it will appear on Google Play) and the contact email, each in both languages.

```bash
grep -n '\[' privacy.html   # must print nothing
```

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
