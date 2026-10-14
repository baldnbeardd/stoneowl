# stoneowl.co

Static rebuild of the Stone Owl site (previously hosted on Convertri), set up to deploy with **GitHub Pages**. No build step — plain HTML/CSS.

```
.
├── index.html          # the page
├── 404.html            # bounces back home after 4s
├── assets/
│   ├── css/style.css
│   └── img/            # wordmark, owl, skyline (.webp + fallback), icons, og.png
├── favicon.ico
├── CNAME               # custom domain: stoneowl.co
├── .nojekyll           # serve files as-is
├── robots.txt
└── sitemap.xml
```

## Preview locally

```bash
cd ~/Websites/stoneowl
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy

1. **Create the repo and push**

   ```bash
   cd ~/Websites/stoneowl
   git init -b main
   git add .
   git commit -m "Rebuild stoneowl.co as a static site"
   gh repo create stoneowl --public --source=. --push
   # or: create it on github.com, then
   # git remote add origin git@github.com:<you>/stoneowl.git && git push -u origin main
   ```

2. **Turn on Pages** — repo → *Settings → Pages* → Source: **Deploy from a branch**, Branch: **main / (root)**. The `CNAME` file sets the custom domain to `stoneowl.co` automatically.

3. **Point DNS at GitHub** (at the registrar for stoneowl.co, replacing the Convertri records):

   | Type  | Host | Value               |
   |-------|------|---------------------|
   | A     | @    | 185.199.108.153     |
   | A     | @    | 185.199.109.153     |
   | A     | @    | 185.199.110.153     |
   | A     | @    | 185.199.111.153     |
   | CNAME | www  | `<you>.github.io`   |

   Optional IPv6 (AAAA on @): `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`

4. Once the domain check goes green in *Settings → Pages*, tick **Enforce HTTPS**.

Every push to `main` redeploys automatically.

## Editing

- **Links** — the social icons are the `<li>` items in the `<nav>` in `index.html`.
- **Analytics** — the GA4 tag (`G-MPS3E0CKQ6`) from the old site is in the `<head>`; delete that block to drop tracking.
- **Year** — the footer year updates itself.
