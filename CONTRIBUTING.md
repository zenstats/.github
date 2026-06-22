# Contributing to ZenStats

Thank you for your interest in contributing! ZenStats is a **privacy-first, self-hosted web analytics** platform. This document covers how to get started, report issues, and submit changes.

## Code of Conduct

All contributors are expected to follow our [Code of Conduct](CODE_OF_CONDUCT.md). Please read it before participating.

## Project structure

ZenStats consists of three independent repositories:

| Repository | Purpose | Tech Stack |
|------------|---------|------------|
| [**zenstats**](https://github.com/zenstats/zenstats) | Go API backend | Go 1.24, Gin, ent ORM (PG), ClickHouse |
| [**zenstats-web**](https://github.com/zenstats/zenstats-web) | React admin panel + Tracker JS SDK | React 19, TypeScript, Vite, Tailwind CSS |
| [**zenstats-deploy**](https://github.com/zenstats/zenstats-deploy) | Docker Compose deployment | Docker, Caddy, PostgreSQL, ClickHouse |

Each repository has its own `README.md` with setup instructions. For local development, clone all three as siblings and use `zenstats-deploy` to orchestrate them.

## Getting started

```bash
# Clone all three repos as siblings
git clone https://github.com/zenstats/zenstats.git
git clone https://github.com/zenstats/zenstats-web.git
git clone https://github.com/zenstats/zenstats-deploy.git

# Start the full local dev environment
cd zenstats-deploy
cp .env.local .env
make local
```

See [zenstats-deploy/README.md](https://github.com/zenstats/zenstats-deploy#readme) for detailed local development instructions.

## Reporting bugs

Open an issue in the relevant repository:

- **Backend / API**: [zenstats issues](https://github.com/zenstats/zenstats/issues/new?template=bug_report.md)
- **Frontend / Tracker SDK**: [zenstats-web issues](https://github.com/zenstats/zenstats-web/issues/new?template=bug_report.md)
- **Deployment / Docker**: [zenstats-deploy issues](https://github.com/zenstats/zenstats-deploy/issues/new?template=bug_report.md)

Include:

- Steps to reproduce
- ZenStats version or commit hash
- Deployment method (Docker / manual)
- Relevant logs or screenshots

## Feature requests

Use the Feature Request template in the repo that best matches your request:

## Pull request workflow

1. **Fork & branch** — Fork the repository you want to contribute to, create a feature branch from `main`
2. **Make changes** — Follow the conventions below
3. **Test locally** — Run `make test` (API) or `pnpm build` (frontend)
4. **Open a PR** — Fill in the PR template
5. **Review** — A maintainer will review within a few days

### API changes ([zenstats](https://github.com/zenstats/zenstats))

- Follow Go standard formatting (`go fmt ./...`)
- Run `make lint` (`go vet ./...`) before committing
- For ent schema changes: edit the schema file → `make ent-generate` → `go run main.go migrate`
- Never manually edit files under `internal/store/postgresql/ent/` (auto-generated)

### Frontend / Tracker changes ([zenstats-web](https://github.com/zenstats/zenstats-web))

- Use `pnpm dev` with `VITE_USE_MOCK=true` for rapid UI iteration
- Verify translations in both `en.json` and `zh-CN.json`
- Run `pnpm build` to confirm no build errors

### Documentation

- Update the relevant `README.md` if you change behavior
- Add JSDoc/GoDoc comments for public APIs

## Style guidelines

- **Go**: Standard library conventions; single-export interfaces preferred
- **TypeScript/React**: Functional components, hooks over classes, Tailwind utility classes
- **Commits**: Conventional Commits format preferred (`feat:`, `fix:`, `docs:`, `chore:`)
- **i18n**: All user-facing strings must have both English and Chinese entries

## License

ZenStats is licensed under the [GNU Affero General Public License v3.0](LICENSE.md). By contributing, you agree that your contributions will be licensed under AGPL-3.0.
