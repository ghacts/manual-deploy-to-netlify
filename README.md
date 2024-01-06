# Manual deploy to Netlify Action

[![Test](https://github.com/ghacts/manual-deploy-to-netlify/actions/workflows/test.yml/badge.svg)](https://github.com/ghacts/manual-deploy-to-netlify/actions/workflows/test.yml)

<!-- action-docs-description -->

## Description

GitHub Actions for manual deploying static site to Netlify.

<!-- action-docs-description -->

<!-- action-docs-inputs -->

## Inputs

| parameter  | description                                                              | required | default |
| ---------- | ------------------------------------------------------------------------ | -------- | ------- |
| auth-token | Netlify authentication token                                             | `true`   |         |
| site       | Netlify site name                                                        | `true`   |         |
| dir        | Directory to deploy                                                      | `false`  | dist/   |
| filter     | For monorepos, specify the name of the application to run the command in | `false`  |         |
| functions  | Netlify functions directory to deploy                                    | `false`  |         |
| message    | Deploy message                                                           | `false`  |         |
| alias      | Site alias                                                               | `false`  |         |
| prod       | Deploy to production                                                     | `false`  | false   |

<!-- action-docs-inputs -->

<!-- action-docs-outputs -->

## Outputs

| parameter          | description        |
| ------------------ | ------------------ |
| success            | Deployment success |
| netlify-deploy-url | Netlify deploy URL |

<!-- action-docs-outputs -->

## Examples

```
jobs:
  deploy-preview:
    name: Deploy preview site
    runs-on: ubuntu-latest
    environment:
      name: preview
      url: ${{ steps.deploy_preview.outputs.netlify-deploy-url }}
    steps:
      - name: Checkout
        id: checkout
        uses: actions/checkout@v3

      - name: Deploy preview site
        id: deploy_preview
        uses: ./
        with:
          auth-token: ${{ secrets.NETLIFY_AUTH_TOKEN }}
          site: ${{ vars.NETLIFY_SITE_NAME }}
          dir: sites/preview
          alias: preview
```

```
jobs:
  deploy-production:
    name: Deploy production site
    runs-on: ubuntu-latest
    if: always()
    environment:
      name: production
      url: ${{ steps.deploy_production.outputs.netlify-deploy-url }}
    steps:
      - name: Checkout
        id: checkout
        uses: actions/checkout@v3

      - name: Deploy production site
        id: deploy_production
        uses: ./
        with:
          auth-token: ${{ secrets.NETLIFY_AUTH_TOKEN }}
          site: ${{ vars.NETLIFY_SITE_NAME }}
          dir: sites/production
          prod: true
```

## Contact

Le Minh Tri [@ansidev](https://ansidev.xyz/about).

## License

This source code is available under the [MIT LICENSE](/LICENSE).
