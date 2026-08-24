# Knovera landing

Static marketing site for **Knovera** — AI-native business ERP. Separate from the [orflax-stockflow](https://github.com/naiverahul/orflax-stockflow) Django app.

**Live (planned):** [knovera.voltxresources.com](https://knovera.voltxresources.com)

## What's here

| File | Purpose |
|---|---|
| `index.html` | Full landing page (inline CSS + JS) |
| `thanks.html` | Shown after contact form submit |

Contact form posts to [FormSubmit](https://formsubmit.co) → **rahul@voltxresources.com** (no backend required).

## Local preview

```bash
cd ~/Desktop/knovera-landing
python3 -m http.server 8080
# open http://localhost:8080
```

Submit the form once locally; FormSubmit sends a confirmation email to `rahul@voltxresources.com` — click **Activate Form** in that email before production submissions work.

## Deploy to knovera.voltxresources.com

### Option A — Cloudflare Pages (recommended)

1. Push this repo to GitHub (`naiverahul/knovera-landing`).
2. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → connect repo.
3. Build settings: **Framework preset = None**, build command empty, **Output directory = `/`**.
4. Custom domain: add `knovera.voltxresources.com` (CNAME to Pages URL).
5. After first deploy, update `index.html` hidden field `_next` if your final URL differs from `https://knovera.voltxresources.com/thanks.html`.

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

Uses FormSubmit (`action="https://formsubmit.co/rahul@voltxresources.com"`). Fields: name, email, company, message.

To switch provider later (Resend, Cloudflare Worker, etc.), change the `<form action>` in `index.html` only.

## Design

Tokens match **Stockflow Claycom** (`DESIGN.md` in the ERP repo). Update both when rebranding.
