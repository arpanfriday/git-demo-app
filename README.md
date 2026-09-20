# Git Demo App

A tiny static web app used as a live demo for the **Git & version control** session.
It is deployed to **GitHub Pages** automatically — but **only from the `main` branch**.
Treat `main` as production: nothing reaches the live site unless it is merged into `main`.

## What's inside

```
git-demo-app/
├── index.html            # the page
├── src/
│   ├── styles.css        # styling
│   └── app.js            # small interactive demo
├── .github/workflows/
│   └── deploy.yml         # GitHub Actions -> GitHub Pages (main only)
├── .gitignore
└── README.md
```

## Run it locally

No build tools required — it's plain HTML/CSS/JS.

```bash
# clone your repo
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>

# serve locally (any static server works)
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploying (main = production)

1. Do work on a feature branch.
2. Open a Pull Request into `main`.
3. When the PR is merged, the **Deploy to GitHub Pages** workflow runs.
4. The site is published. Pushes to any other branch do **not** deploy.

The workflow is defined in [`.github/workflows/deploy.yml`](.github/workflows/deploy.yml)
and is restricted with:

```yaml
on:
  push:
    branches: [main]
```

## Demo talking points

- Every merge into `main` = one production release.
- The build stamp on the page (`build.json`) is generated during deploy, so you can
  point at it and say "this is the exact commit that's live right now."
- Show a change on a branch → open a PR → merge → watch Actions redeploy.

## Suggested branch protection

To make `main` behave like production, enable branch protection on `main`
(**Settings → Branches → Add rule**): require a pull request and require the
deploy check to pass before merging.
