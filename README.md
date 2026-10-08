# tesla-fleet-key

Public hosting for the **public** half of the Tesla Fleet API application key used by
`home-automation/scripts/supercharger-collect.py`. Served by GitHub Pages at
**https://tesla.advoverwatch.com** (CNAME in GoDaddy DNS → `head2wind.github.io`).

| Path | Purpose |
|---|---|
| `/.well-known/appspecific/com.tesla.3p.public-key.pem` | Tesla requires the app's public key at exactly this path on the app's domain |
| `/callback.html` | OAuth redirect target: shows the sign-in callback URL so it can be pasted back into the CLI. Sends nothing anywhere — no referrer, no external resources (CSP `default-src 'none'`) |
| `.nojekyll` | Without it GitHub Pages (Jekyll) silently drops dot-directories like `.well-known/` |
| `CNAME` | Custom domain for Pages |

**This repo is public on purpose.** A public key is meant to be published. The private key
never leaves ADVM2: it lives in `home-automation/scripts/tesla-fleet-private-key.secret`,
gitignored by `*.secret`. **Never commit any `*.secret`, `*-private*`, or `PRIVATE KEY`
material here** — `git grep -n "PRIVATE"` must return nothing.

Rotating the key: generate a new pair in home-automation, replace the `.pem` here, push,
then re-run the Fleet API partner registration (see `home-automation/teslamate/README.md`).

No services, no ports, no scheduled tasks. Created 2026-10-07.
