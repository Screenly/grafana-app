[![Version](https://img.shields.io/github/v/release/Screenly/grafana-app)](https://github.com/Screenly/grafana-app/releases/latest)

# Screenly Grafana App

![Grafana App Preview](/screenshots/1920x1080.webp)

## Getting Started

```bash
bun install
```

## Deployment

Create and deploy the Edge App:

```bash
screenly edge-app create --name my-grafana --in-place
bun run deploy
screenly edge-app instance create
```

### Releasing

Pushes to `main` start a stage deploy, which waits for approval. To release to production, tag a commit on `main` and push the tag (the workflow refuses tags not on `main`); the production deploy also waits for approval:

```bash
git checkout main && git pull
git tag v26.10.0
git push origin v26.10.0
```

Then publish a GitHub Release whose notes list the pull requests merged since the previous release. Add `--draft` to review the notes before publishing:

```bash
gh release create v26.10.0 --verify-tag --generate-notes --title v26.10.0
```

## Configuration

The app accepts the following settings via `screenly.yml`:

| Setting            | Description                                                                          | Type               | Default |
| ------------------ | ------------------------------------------------------------------------------------ | ------------------ | ------- |
| `dashboard_id`     | The unique ID of the Grafana dashboard (can be selected via dropdown when available) | required           | -       |
| `display_errors`   | Display detailed error messages on screen for debugging purposes                     | optional, advanced | `false` |
| `refresh_interval` | The interval in seconds to refresh the dashboard image                               | optional           | `60`    |

The Grafana domain and service access token are automatically fetched from your Grafana integration setup.

### Getting Dashboard Information

1. **Select Your Dashboard**
   - You can select your dashboard from a dropdown list that automatically populates available dashboards from your Grafana instance
   - Alternatively, you can manually enter the dashboard ID

2. **Find Dashboard ID Manually**
   - Open your Grafana dashboard
   - The URL in the browser will look like: `https://your-domain.grafana.net/d/<dashboard_id>/<dashboard_slug>`
   - Extract the `<dashboard_id>` value (you don't need the slug)

## Development

```bash
bun install      # Install dependencies
bun run dev      # Start development server
```

## Testing

```bash
bun test
```

## Screenshots

Generate screenshots at all supported resolutions:

```bash
bun run screenshots
```

Screenshots are saved to the `screenshots/` directory.
