# Deploy to Steamship

This GitHub Action template will deploy your repository's Steamship App or Plugin.

The deployment script contains the following sanity checks:

* That your `steamship.json` project file exists
* That your project has a `type` of either `app` or `plugin`

Along with the following QA checks:

* That your project passes the `pytest` command
* That this Action is being run form a tag called `v###.###.###`
* That project has a version of `###.###.###` (matching the tag, but without the v)

We recommend the following workflow:

* Write tests for yourplugin / app with pytest (preconfigured with all Steamship plugins and apps)
* Release new versions using GitHub's release feature:
  * Tagging the release with standard semver format (e.g. `v1.0.2`)
  * Making sure the `version` field in `steamship.json` matches (e.g. `1.0.2`)
## Inputs

### `steamship_key`

**Required** Your Steamship API Key. Store it as a Repository Secret and pass it in.

## Example usage

```yaml
name: Deploy to Steamship

on:
  push:
    tags:
      - 'v[0-9]+.[0-9]+.[0-9]+*'

jobs:
  deploy:
    name: Deploy to Steamship
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      - name: Deploy to Steamship
        uses: steamship-core/deploy-to-steamship@main
        with:
          steamship_key: ${{ secrets.STEAMSHIP_KEY }}
```
