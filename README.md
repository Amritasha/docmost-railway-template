# Docmost on Railway

[![CI](https://github.com/Amritasha/docmost-railway-template/actions/workflows/ci.yml/badge.svg)](https://github.com/Amritasha/docmost-railway-template/actions/workflows/ci.yml)
[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/template/docmost)

[Docmost](https://docmost.com) is an open-source collaborative wiki and documentation platform — a self-hosted alternative to Notion and Confluence. Real-time editing, nested pages, workspaces, and granular permissions.

## What's included

- **Docmost** — the app (port 3000)
- **PostgreSQL** — primary database
- **Redis** — real-time collaboration + job queue

## One-click deploy

Click the **Deploy on Railway** button above. Railway will provision all three services automatically.

## Environment variables

Set these after deployment in your Railway project dashboard:

| Variable | Required | Description |
|----------|----------|-------------|
| `APP_URL` | Yes | Your Railway public domain, e.g. `https://docmost.up.railway.app` |
| `APP_SECRET` | Yes | Random secret — generate with `openssl rand -hex 32` |
| `DATABASE_URL` | Auto | Filled automatically from the Postgres service |
| `REDIS_URL` | Auto | Filled automatically from the Redis service |
| `NODE_ENV` | Recommended | Set to `production` |
| `DISABLE_TELEMETRY` | Optional | Set to `true` to opt out of telemetry |

See [`.env.example`](.env.example) for the full list including email, S3, and AI options.

## First launch

1. Open your `APP_URL` — you'll be prompted to create the admin account
2. Create your first workspace
3. Invite your team via email (requires SMTP configuration)

## File storage

Uploaded files are stored in a Railway volume at `/app/data/storage` by default.

To use S3-compatible storage instead, set:

```
STORAGE_DRIVER=s3
AWS_S3_ACCESS_KEY_ID=...
AWS_S3_SECRET_ACCESS_KEY=...
AWS_S3_REGION=us-east-1
AWS_S3_BUCKET=your-bucket
```

## Email (invites & password reset)

```
MAIL_DRIVER=smtp
MAIL_FROM_ADDRESS=noreply@yourdomain.com
SMTP_HOST=smtp.resend.com
SMTP_PORT=587
SMTP_USERNAME=resend
SMTP_PASSWORD=your-api-key
```

Works with Resend, SendGrid, Postmark, or any SMTP provider.

## Upgrading

The image version is pinned in [`Dockerfile`](Dockerfile). A weekly GitHub Actions workflow opens a PR automatically when a new Docmost release is available. Merge the PR and redeploy.

To upgrade manually:

```dockerfile
FROM docmost/docmost:0.81.0
```

## License

Docmost is [AGPL-3.0](https://github.com/docmost/docmost/blob/main/LICENSE). This template is MIT.
