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

## Run python tests

Installs `REQUIREMENTS` with pip, checks code with ruff and runs pytest.
Ruff has to be in `REQUIREMENTS`, or disabled with `LINT: false`.

### Usage

```yaml
name: Run python tests

on:
  push:
    branches:
      - "**"

jobs:
  test:
    uses: a-was/actions/.github/workflows/python-tests.yaml@main
    with:
      # optional, default values
      PYTHON_VERSION: "3.14"
      REQUIREMENTS: requirements-dev.txt
      LINT: true
      PYTEST_ARGS: -v
```

To build the image only when tests pass, add `needs: test` to the `build-and-push` job.

# Docs

- [Reusing workflows](https://docs.github.com/en/actions/sharing-automations/reusing-workflows)
- [TAGS input](https://github.com/docker/metadata-action?tab=readme-ov-file#tags-input)
- [PYTHON_VERSION input](https://github.com/actions/setup-python/blob/main/docs/advanced-usage.md#using-the-python-version-input)
- [Workflow syntax](https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions)
