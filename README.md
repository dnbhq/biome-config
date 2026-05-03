# @dnbhq/biome-config

Shared Biome configuration for DNBHQ projects.

* [Installation](#installation)
* [Usage](#usage)
* [Available config](#available-config)
* [Design notes](#design-notes)
* [Release](#release)
* [Notes](#notes)

## Installation

```bash
npm install --save-dev @dnbhq/biome-config @biomejs/biome
```

## Usage

Create or update `biome.json` in the consuming project:

```json
{
  "$schema": "./node_modules/@biomejs/biome/configuration_schema.json",
  "extends": ["./node_modules/@dnbhq/biome-config/config.json"]
}
```

## Available config

### Strict DNBHQ baseline

The package exports one shared Biome configuration:

```json
{
  "extends": ["./node_modules/@dnbhq/biome-config/config.json"]
}
```

It enables formatting, import organisation, VCS integration, and a strict rule set for performance, complexity, correctness, and suspicious-code checks.

## Design notes

The configuration data was migrated from `packages/biome-config` in `davidsneighbour/configurations`.

The shared config intentionally keeps project-local decisions in the consuming project. Consumers can override values after the shared config in their local `biome.json`.

Biome applies configs from the `extends` list first, then applies local options from the consuming `biome.json`, so local project settings remain the most specific settings.

## Release

Dry run:

```bash
npm run release:dry
```

Release:

```bash
npm run release
```

Releases are handled by `release-it` and `@release-it/conventional-changelog`.

Commit messages should follow Conventional Commits.

Publishing is handled by the `Publish package` GitHub Actions workflow when a `v*` tag is pushed.

## Notes

* The consuming project should install `@biomejs/biome` directly so editor integrations, CLI usage, and lockfiles remain project-local.
* The package includes only `config.json`, `README.md`, `CHANGELOG.md`, and `LICENSE` in the npm package.
* Use `npm run test` before releasing. The test command currently runs `biome check` against this repository.
