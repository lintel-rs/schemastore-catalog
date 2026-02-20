# schemastore-catalog

A mirror of the [SchemaStore](https://www.schemastore.org/) catalog, providing a version-controlled copy of the catalog index and all schema files for use by [lintel](https://github.com/lintel-rs/lintel).

## How it works

This repo is automatically updated daily by a [CI workflow](https://github.com/lintel-rs/lintel/blob/master/.github/workflows/schemastore-catalog.yml) in the lintel repo that runs `lintel-schemastore-catalog update`. That command:

1. Fetches the [SchemaStore catalog](https://www.schemastore.org/api/json/catalog.json)
2. Downloads every referenced schema concurrently
3. Rewrites the catalog's `url` fields to point to `raw.githubusercontent.com` URLs in this repo
4. Validates each download is parseable JSON; skips failures gracefully
5. Commits and pushes `catalog.json` + `schemas/*.json` if anything changed

## Structure

```
catalog.json          # rewritten catalog index
schemas/
  tsconfig.json
  package-json.json
  github-workflow.json
  ...
```
