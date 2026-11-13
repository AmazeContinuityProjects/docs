# AmazeCC Docs

The documentation site for **AmazeCC** — the VIT student portal, rebuilt. A Mintlify site that aggregates the docs tree from the [AmazeCC repository](https://github.com/AmazeContinuityProjects/AmazeCC) and serves it as a single, navigable handbook for developers.

**Live site:** https://amazecc.com/docs (or your Mintlify-assigned URL until the custom domain is wired)

## How this repo works

This repo is the **site shell**. The actual content lives in the [AmazeCC](https://github.com/AmazeContinuityProjects/AmazeCC) repo under `docs/`. A scheduled/manual GitHub Action (`Aggregate docs`, `.github/workflows/aggregate-docs.yml`) pulls that folder in here, rewrites the navigation, and opens a PR or pushes to this repo:

```
AmazeCC/                              this repo (AmazeContinuityProjects/docs)
  docs/  ──shallow-clone──▶           amazecc/                    ← synced content
  docs/docs.json ──merge──▶           docs.json (generated)        ← synced nav
  (everything else here)              docs.base.json, .github/,     ← you edit these
                                       index.mdx, quickstart.mdx,
                                       logo/, favicon.svg
```

**Do not edit `amazecc/` or `docs.json` here — the next sync overwrites them.** To change a page, edit the child repo (AmazeCC, `docs/…`). To change site configuration (theme, tabs, landing pages), edit `docs.base.json` and the rebranded files.

## Local development

```bash
npm i -g mint
mint dev          # http://localhost:3000
```

Previewing the aggregated site without a sync run:

```bash
git clone https://github.com/AmazeContinuityProjects/docs.git
cd docs
# (after the first sync has populated amazecc/, or with a shallow copy of it)
mint dev
```

## Publishing

Mintlify deploys this repo automatically on push to `main` (after you install the Mintlify GitHub App on the organization). The sync workflow opens a PR whenever the child's docs change; merge it and the site updates.

- [AmazeCC](https://github.com/AmazeContinuityProjects/AmazeCC) — the app + its docs source tree
- [AmazeCC-API](https://github.com/AmazeContinuityProjects/AmazeCC-API) — the backend scraper
- [Mintlify](https://mintlify.com) — docs framework
- [Mintlify multirepo action](https://github.com/mintlify/multirepo-action) — the aggregator used here

## License

MIT.
