# Deploying peihanliu.com on GitHub Pages

## 1. Push this folder to a GitHub repo

```bash
cd /Users/peihanliu/Research
git init
git add .
git commit -m "Initial site"
git branch -M main
# Create an empty repo on GitHub first, then:
git remote add origin git@github.com:<your-username>/<repo-name>.git
git push -u origin main
```

Two repo-name options:
- **`<your-username>.github.io`** — served at `https://<your-username>.github.io` and at your custom domain. Simplest.
- **Any other name** (e.g. `personal-site`) — served at `https://<your-username>.github.io/<repo-name>`. Also fine; the custom domain still works.

## 2. Turn on Pages

GitHub repo → **Settings → Pages**:
- Source: **Deploy from a branch**
- Branch: `main` / root (`/`)
- Save.

Within ~1 minute you should get a green checkmark with the live URL.

## 3. Point peihanliu.com at GitHub

The `CNAME` file in this repo already declares `peihanliu.com`.

In your DNS provider (wherever you bought peihanliu.com), add these records:

**Apex (peihanliu.com)** — four A records pointing to GitHub's IPs:
```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
```

**www subdomain** — CNAME to your GitHub Pages host:
```
CNAME   www   <your-username>.github.io.
```
(Note the trailing dot, and use your actual GitHub username.)

DNS can take anywhere from a few minutes to a few hours to propagate.

## 4. Enforce HTTPS

Back in **Settings → Pages**, once DNS is verified, tick **Enforce HTTPS**. GitHub provisions a Let's Encrypt cert automatically.

## Editing the site later

- Bio / experience / publications / blog list: edit `index.html`.
- Styles: `styles.css`.
- New blog post: drop an HTML file in `posts/` and add a `<li>` to the Writing section in `index.html`.

Commit & push — the live site updates within ~30 seconds.
