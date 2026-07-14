# Orb Wiki

Documentation and the public site for [Orb](https://github.com/getorb) — the proactive
AI presence. **The assistant that talks first — on hardware you own.**

Published with GitHub Pages (Jekyll + the [just-the-docs](https://just-the-docs.com)
theme). Guides live here: getting started, connecting your PC, brains & models,
connectors, free-API providers, local inference, and the FAQ.

- App: [Orb-Mobile-App](https://github.com/getorb/Orb-Mobile-App)
- Server: [Orb-Backend](https://github.com/getorb/Orb-Backend)

## Edit the wiki

Pages are plain Markdown in this repo's root. Each has front matter:

```yaml
---
title: Page Title
nav_order: 4
---
```

Edit a `.md` file (or add a new one), commit, and GitHub Pages rebuilds automatically.

## Run locally (optional)

```bash
gem install bundler jekyll
bundle exec jekyll serve
```

## Contributing

Free-API limits and provider lists change often — corrections and additions are welcome.
Open a PR. Keep pages user-facing and practical.
