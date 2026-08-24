# Knovera landing

Static marketing site for **Knovera** — AI-native business ERP. Separate from the [orflax-stockflow](https://github.com/naiverahul/orflax-stockflow) Django app.

**Live (planned):** [knovera.voltxresources.com](https://knovera.voltxresources.com)

## What's here

| File | Purpose |
|---|---|
| `public/index.html` | Full landing page (inline CSS + JS) |
| `public/thanks.html` | Shown after contact form submit |

Contact form posts to [FormSubmit](https://formsubmit.co) → **rahul@voltxresources.com** (no backend required).

## Local preview

```bash
cd ~/Desktop/knovera-landing
python3 -m http.server 8080 --directory public
# open http://localhost:8080
```

Submit the form once locally; FormSubmit sends a confirmation email to `rahul@voltxresources.com` — click **Activate Form** in that email before production submissions work.

## Deploy to knovera.voltxresources.com

### Cloudflare (Git → Workers static assets)

Cloudflare may require a **deploy command**. Use these settings:

| Field | Value |
|---|---|
| Build command | `npm install` |
| **Deploy command** | `npx wrangler deploy` |
| Root directory | `/` |

`wrangler.toml` in this repo tells Wrangler to publish all static files (`index.html`, `thanks.html`).

After deploy: **Workers & Pages** → your project → **Settings** → **Domains & Routes** → add `knovera.voltxresources.com`.

### Cloudflare Pages (if deploy command can stay empty)

1. **Workers & Pages** → **Create** → **Pages** tab → connect repo.
2. Framework: **None**, build command empty, output directory **`/`**.

### Direct upload (no Git, no deploy command)

**Workers & Pages** → **Create** → **Upload assets** → drag the repo folder. Fastest if Git setup fights you.

### Option B — GitHub Pages

1. Repo → **Settings** → **Pages** → Source: **Deploy from branch** `main`, folder `/ (root)`.
2. DNS at voltxresources.com: CNAME `knovera` → `naiverahul.github.io` (or use Cloudflare proxy to GitHub Pages).

### Option C — S3 + CloudFront

Upload `index.html` and `thanks.html` to a bucket; point `knovera.voltxresources.com` at the distribution.

## DNS (voltxresources.com)

Add one record:

| Type | Name | Target |
|---|---|---|
| CNAME | `knovera` | Your Pages host (e.g. `knovera-landing.pages.dev`) |

Keep the ERP app on its own host (e.g. factory IP or `app.voltxresources.com`) — do not serve Django from this repo.

## Contact form

Uses FormSubmit (`action="https://formsubmit.co/81f07e5a51a5ffd1ab93878990954884"`) → **rahul@voltxresources.com**. Fields: name, email, company, message.

To switch provider later (Resend, Cloudflare Worker, etc.), change the `<form action>` in `index.html` only.

## Design

Tokens match **Stockflow Claycom** (`DESIGN.md` in the ERP repo). Update both when rebranding.
