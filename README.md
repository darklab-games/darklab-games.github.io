# DarkLab Games — website

The public site for **Void Strike**. It exists mainly to host the two URLs Google
Play requires, plus an `app-ads.txt` that AdMob needs in order to verify your
inventory. It also serves a playable browser build.

---

## ⚠ Name the repository correctly — this matters

**Create the repo as `<your-github-username>.github.io`.**

Not `voidstrike`, not `darklab-site`. Here is why:

`app-ads.txt` is only crawled at the **root of a domain**. With a repo named
`<username>.github.io` your site is served at `https://<username>.github.io/`, so
the file lands at `https://<username>.github.io/app-ads.txt` — which is where
AdMob looks.

Any other repo name puts the site in a subdirectory
(`https://<username>.github.io/voidstrike/`), the file ends up at
`/voidstrike/app-ads.txt`, and **AdMob will never find it.** The privacy policy
would still work, but you would be leaving ad revenue on the table and losing a
fraud protection.

If your GitHub account is an organisation named `darklabgames`, the repo is
`darklabgames.github.io` and the site is `https://darklabgames.github.io/`.

---

## Deploy

```bash
cd github-pages
git init -b main
git add .
git commit -m "DarkLab Games site: Void Strike, privacy, terms, support"
git remote add origin https://github.com/<username>/<username>.github.io.git
git push -u origin main
```

Then in the repo: **Settings → Pages → Source: Deploy from a branch →
`main` / `/ (root)` → Save.**

First publish takes 1–2 minutes. Confirm all four of these load before you
touch Play Console:

- `https://<username>.github.io/`
- `https://<username>.github.io/privacy.html`
- `https://<username>.github.io/support.html`
- `https://<username>.github.io/app-ads.txt`

---

## Where each URL goes

### Google Play Console

| Console field | Value |
|---|---|
| Store listing → **Privacy policy** | `https://<username>.github.io/privacy.html` |
| Store settings → **Email** | `darklabgaming24@gmail.com` |
| Store settings → **Website** | `https://<username>.github.io/` |
| Store settings → **Phone** | optional, leave blank |

> The **Website** field is what AdMob reads to find `app-ads.txt`. Set it to the
> root URL, not a subpage.

### AdMob

**Apps → Void Strike → App settings → app-ads.txt.** Once the Play listing is
live and linked, AdMob crawls the site automatically. Status moves from
*Not found* to *Authorised* within roughly 24 hours. You can force a recheck
from that page.

---

## Files

| Path | Purpose |
|---|---|
| `index.html` | Landing page. Click-to-play hero, screenshots, studio blurb. |
| `privacy.html` | **Required by Play.** Matches what you declare in Data safety. |
| `terms.html` | Not required, but expected of a real studio. |
| `support.html` | Controls, FAQ, how to report a bug. Good as the Play support URL. |
| `app-ads.txt` | AdMob authorised sellers. Root hosting required — see above. |
| `play/index.html` | The full game, playable in a browser. Identical to the Android build; the native hooks are inert without Capacitor. |
| `404.html` | Fallback page. |
| `.nojekyll` | Stops GitHub running Jekyll, which would otherwise ignore some files. |
| `assets/` | Stylesheet, icon, feature graphic, eight compressed screenshots. |

---

## Keeping the browser build current

`play/index.html` is a copy. After changing the game, refresh it:

```bash
cp ../android-app/www/index.html play/index.html
```

Do not edit it in place — the Android build is the source of truth.

If you would rather not host a free browser version alongside the Play release,
delete the `play/` folder and remove the Play links from `index.html`,
`support.html`, `terms.html` and `404.html`.

---

## Editing the text

Everything is plain HTML with one stylesheet, no build step and no dependencies.
Open a file and type.

Two things to change if your details differ:

- **Email** — `darklabgaming24@gmail.com` appears in all four pages.
- **Country** — the terms do not name a jurisdiction. If you want one, add a
  governing-law line to `terms.html`.

Colours and type live at the top of `assets/style.css` as CSS custom properties.
