<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/zenstats/zenstats/main/assets/logo-horizontal-dark.svg">
    <img src="https://raw.githubusercontent.com/zenstats/zenstats/main/assets/logo-horizontal.svg" height="80" alt="ZenStats">
  </picture>
</p>

<p align="center">
  <strong>Self-Hosted · Cookieless · Privacy-First Web Analytics</strong>
</p>

<p align="center">
  <a href="https://github.com/zenstats/zenstats/blob/main/LICENSE.md"><img src="https://img.shields.io/badge/license-AGPL--3.0-blue" alt="License"></a>
  <a href="https://github.com/zenstats/zenstats"><img src="https://img.shields.io/badge/Go-1.25-00ADD8?style=flat&logo=go" alt="Go"></a>
  <a href="https://github.com/zenstats/zenstats-web"><img src="https://img.shields.io/badge/React-19-61DAFB?style=flat&logo=react" alt="React"></a>
  <a href="https://github.com/zenstats/zenstats"><img src="https://img.shields.io/github/stars/zenstats/zenstats?style=flat" alt="Stars"></a>
</p>

---

## What is ZenStats?

ZenStats is an **open-source, self-hosted** alternative to Google Analytics.
Track your website traffic without compromising visitor privacy — **no cookies,
no personal data collection, fully compliant with GDPR / CCPA / PECR**.

### Why ZenStats?

- 🔒 **Privacy by design** — No cookies, no fingerprinting, no cross-site tracking
- 📦 **Self-hosted** — Your data stays on your server, not in a third-party cloud
- ⚡ **Lightweight** — Tracker script is ~3 KB, won't slow down your site
- 🌍 **Geo-aware** — Built-in GeoIP (country/region/city) without exposing IPs
- 📊 **Rich analytics** — Realtime dashboard, funnels, goals, custom events, UTM tracking
- 🎨 **Dark mode** — Full light/dark theme support across the entire dashboard
- 🧩 **SPA support** — Works with React, Vue, and all modern frameworks

---

## Repositories

| Repository | Description | Stack |
|------------|-------------|-------|
| [**zenstats**](https://github.com/zenstats/zenstats) | Go API backend | Go 1.25, Gin, PostgreSQL, ClickHouse |
| [**zenstats-web**](https://github.com/zenstats/zenstats-web) | React admin panel + Tracker JS SDK | React 19, TypeScript, Vite, Tailwind CSS |
| [**zenstats-deploy**](https://github.com/zenstats/zenstats-deploy) | Docker Compose one-click deployment | Docker, Caddy, PostgreSQL 18, ClickHouse |

---

## Quick Start

```bash
# Clone all three repos as siblings
git clone https://github.com/zenstats/zenstats.git
git clone https://github.com/zenstats/zenstats-web.git
git clone https://github.com/zenstats/zenstats-deploy.git

# One command to start everything locally
cd zenstats-deploy
cp .env.local .env
make local

# Open http://localhost
```

That's it — PostgreSQL, ClickHouse, Go API, and Caddy frontend are all running locally.
Generate test data with `make seed-test` and start exploring at `http://localhost`.

---

## Architecture

```
                    ┌──────────────────────────┐
  Internet ────▶ [Caddy :80/:443]              │
                    │  SPA + Tracker JS + Proxy │
                    └─────────┬────────────────┘
                              │ /api/*  reverse proxy
                              ▼
                    ┌──────────────────────────┐
                    │   Go API :8080            │
                    │   Gin + JWT + LRU Cache   │
                    └──────┬──────────┬────────┘
                           │          │
                           ▼          ▼
                  ┌────────────┐ ┌──────────────┐
                  │ PostgreSQL │ │  ClickHouse   │
                  │ (metadata) │ │  (analytics)  │
                  └────────────┘ └──────────────┘
```

---

## Contributing

We welcome contributions! See [CONTRIBUTING.md](https://github.com/zenstats/.github/blob/main/CONTRIBUTING.md) for guidelines on reporting bugs, suggesting features, and submitting pull requests.

## License

ZenStats is licensed under the [GNU Affero General Public License v3.0](https://github.com/zenstats/zenstats/blob/main/LICENSE.md).
