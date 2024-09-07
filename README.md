# Shared github actions

## Build and push docker image

### Usage

```yaml
name: Build and push docker image

on:
  push:
    branches:
      - "**"
    tags:
      - "v*"

jobs:
  build-and-push:
    uses: a-was/actions/.github/workflows/build-and-push.yaml@main
    with:
      IMAGE: myapp
      REGISTRY: ${{ vars.REGISTRY }}
      REGISTRY_LOGIN: ${{ vars.REGISTRY_LOGIN }}
      # optional
      DOCKERFILE: app/Dockerfile
      TAGS: |
        type=semver,pattern={{version}}
        type=ref,event=branch
    secrets:
      REGISTRY_PASSWORD: ${{ secrets.REGISTRY_PASSWORD }}
```

# Docs

- [Reusing workflows](https://docs.github.com/en/actions/sharing-automations/reusing-workflows)
- [TAGS input](https://github.com/docker/metadata-action?tab=readme-ov-file#tags-input)
- [Workflow syntax](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions)
