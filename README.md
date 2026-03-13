## site-base

`site-base` is the shared Hugo module layer for the `www` and `docs` sites.

### Module identity

- Module path: `github.com/dan-hill/site-base`

### Responsibility

- imports the shared OX presentation module
- mounts OX archetypes, assets, data, layouts, and static files into the live Hugo module tree
- provides the shared integration point used by both sites

### Current dependency chain

- `github.com/dan-hill/ox` → shared theme/presentation
- `github.com/dan-hill/site-base` → shared site integration layer
- `github.com/dan-hill/www` → site consuming `site-base`
- `github.com/dan-hill/docs` → site consuming `site-base`

### Notes on overrides

`site-base` intentionally no longer ships its own page/home/section/base templates, because those would override OX and prevent the shared theme from taking effect.

Downstream repos can still add local overrides, such as `docs/layouts/page.html`.

### GitHub Actions / deploy prerequisite

`site-base` itself is not the Pages deployment target, but it must resolve OX remotely for downstream GitHub Actions builds to work.

After OX is pushed and tagged, OpenClaw should run:

- `hugo mod get github.com/dan-hill/ox@<tag>`

Then commit the updated `go.mod` and generated `go.sum`, tag `site-base`, and push it before pushing updated `www` and `docs`.