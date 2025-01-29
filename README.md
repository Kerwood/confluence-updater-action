# confluence-updater-action
A Github Action for the [Confluence Updater](https://github.com/Kerwood/confluence-updater) tool.

## Example
The example below triggers the pipeline whenever there is a push to the `main` branch that includes changes to the `./README.md` file.

If you have multiple Markdown files and prefer not to list them explicitly in the workflow file, you can omit the `on.push.paths` property.
Confluence Updater will only update the page if the content SHA has changed.
```yaml
name: Update Confluence

on:
  workflow_dispatch:
  push:
    branches:
      - main
    paths:
      - "README.md"

jobs:
  confluence-updater:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Confluence Updater
        uses: kerwood/confluence-updater-action@v1
        with:
          fqdn: your-domain.atlassian.net
          user: ${{ secrets.USER }}
          api_token: ${{ secrets.API_TOKEN }}

          # Optional
          version: 2.0.0 # Will default to latests version
          labels: "github-action $GITHUB_REPOSITORY" # Global labels that is added to all Confluece pages.
```
