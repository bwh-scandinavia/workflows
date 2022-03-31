# Shared Github actions and workflows

Reusuable workflows, actions, composite actions for use in our Github workflows.

Please note that this repository is _PUBLIC_ and no sensitive information shall be saved here! This is a Github limitation (unless we have a Github Enterprise plan) that only allows reusable workflows and actions from public repositories.

## Reusable workflows:

| workflow                        | language | service  |
| ------------------------------- | -------- | -------- |
| build-deploy-node-function.yaml | nodejs   | function |


## Example usage for function app:

In your project repository, create your workflow thusly:

```
name: Build & Deploy

on:
  push:
    branches:
      - main

  workflow_dispatch:
    branches:
      - main

jobs:
  build-deploy-test:
    uses: bwh-scandinavia/actions/.github/workflows/build-deploy-node-function.yaml@main
    with:
      ENVIRONMENT: Test
      NODE_VERSION: 16.x
      AZURE_FUNCTIONAPP_NAME: func-test-something
    secrets:
      SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}
      AZURE_FUNCTIONAPP_PUBLISH_PROFILE: ${{ secrets.AZURE_FUNCTIONAPP_PUBLISH_PROFILE_TEST }}
      NODE_AUTH_TOKEN: ${{ secrets.BWH_PAT_READ_PACKAGES }}
```

## Example usage for app service:

In your project repository, create your workflow thusly:

```
name: Build & Deploy

on:
  push:
    branches:
      - main

  workflow_dispatch:
    branches:
      - main

jobs:
  build-deploy-test:
    uses: bwh-scandinavia/actions/.github/workflows/build-deploy-node-appservice.yaml@main
    with:
      ENVIRONMENT: Test
      NODE_VERSION: 16.x
      AZURE_APPSERVICE_NAME: app-test-something
    secrets:
      SLACK_WEBHOOK_URL: ${{ secrets.SLACK_WEBHOOK_URL }}
      AZURE_APPSERVICE_PUBLISH_PROFILE: ${{ secrets.AZURE_APPSERVICE_PUBLISH_PROFILE_TEST }}
      NODE_AUTH_TOKEN: ${{ secrets.BWH_PAT_READ_PACKAGES }}
```

