# Zip NPM Files GitHub Action

[![🚀 Build and release](https://github.com/Roslovets-Inc/ZipAction/actions/workflows/build_and_release.yml/badge.svg?branch=main)](https://github.com/Roslovets-Inc/ZipAction/actions/workflows/build_and_release.yml)

Zip specific files of npm project for deployment and distribution.

## Usage

Call this action with input list of files to get them zipped into archive with name `<npm_package_name><npm_package_version>.zip`. This archive you can attach to release or upload to your server for deployment.

Also with this action there is no need to use another actions to get and use npm package name and version.

More information about zipping: [bestzip](https://github.com/nfriedly/node-bestzip).

### Inputs

#### Parameters

| Name    | Description                                                                           | Required | Default |
| ------- | ------------------------------------------------------------------------------------- | -------- | ------- |
| `files` | Files to zip. Comma-separated list. Also support wildcard (\*) that ignores .dotfiles | ✔️       |         |
| `cwd`   | Current Working Directory that files and zip archive paths are relative to            | ➖       | `""`    |

### Outputs

| Name      | Description                  |
| --------- | ---------------------------- |
| `archive` | Relative path to zip archive |
| `name`    | Name of npm package          |
| `version` | Version of npm package       |

### Examples

Zip compiled JS files (in `dist` folder) for deployment with pm2.

```yml
- name: 📦 Zip dist files
  id: zip
  uses: Roslovets-Inc/zip-npm-files@v1
  with:
    files: dist, pm2.ecosystem.yml
```

Variable `${{ steps.zip.outputs.archive }}` contains path to zip archive.

Also this action use itself in its own [build and release workflow](.github/workflows/build_and_release.yml).

## Development

To create new release of this action use `npm version ...` (i.e. `npm version patch`). GitHub workflow automatically will:

1. Build JS code
2. Update release branch
3. Create release tag
4. Create GitHub Release draft

After it you just need to setup GitHub Release and publish it to Marketplace.
