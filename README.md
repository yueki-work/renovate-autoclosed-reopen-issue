# 12260

Reproduction for [Renovate issue 12260](https://github.com/renovatebot/renovate/issues/12260).

## Current behavior

Renovate removes comments from `jobs.jobname.steps.uses`, even when commit hash pinning is disabled.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v1 # Comment that Renovate bot will remove later on

      - name: Run a one-line script
        run: echo Hello, world!
```

## Expected behavior

### Commit hash pinning disabled

If commit hash pinning is disabled, then Renovate keeps the original comment.


```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v1 # Renovate keeps comment if commit hash pinning disabled

      - name: Run a one-line script
        run: echo Hello, world!
```

### Commit hash pinning enabled

If commit hash pinning is enabled, then Renovate puts the tag right behind the action name, and moves the original comment further down the line.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v1e204e9a9253d643386038d443f96446fa156a97 # renovate: tag=v2.3.5 # Comment that Renovate bot has moved

      - name: Run a one-line script
        run: echo Hello, world!
```
