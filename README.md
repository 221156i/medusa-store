# Medusa Store

Medusa v2 ecommerce platform with storefront and admin panel.

## Structure

- `backend/` - Medusa server
- `storefront/` - Next.js storefront
- `docker-compose.yml` - Local dev environment

## Local Dev

```bash
docker-compose up -d
```

Working in a subproject directly:

```bash
cd backend && bun install && bun run dev
cd storefront && bun install && bun run dev
```

## CI/CD

GitHub Actions builds and pushes Docker images to GHCR on `main`, then triggers Dokploy deployment.

Workflow: `.github/workflows/deploy.yml`

### Required GitHub secrets
- `DOKPLOY_WEBHOOK_URL` — deploy hook URL from the Dokploy project settings

Images are pushed to `ghcr.io/<owner>/<repo>/{backend,storefront}` and tagged with the branch name, short SHA, and `latest` on `main`. PRs build only (no push).

Make the package visibility public in **GitHub → Packages** if Dokploy needs to pull unauthenticated, or add a `docker/login-action` step on the Dokploy host with a token.
