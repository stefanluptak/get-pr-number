# Get Pull Request Number

_GitHub Action to get current Pull Request number_

## Motivation

I need to easily get the number of the PR a workflow is running for.

## Usage

```yaml
name: CI

on:
  pull_request:
    types:
      - opened

jobs:
  ci:
    runs-on: ubuntu-latest

    steps:
      - uses: stefanluptak/get-pr-number@v1
        id: get_pr_number
      - run: echo $PR_NUMBER
        env:
          PR_NUMBER: ${{ steps.get_pr_number.outputs.pr_number }}
```

## Notes

It's needed to have the `actions/checkout@v2` step before this action, otherwise the `hub` command inside the action won't know on what git repository to operate.

If you're using Dependabot, you might want to consider putting `if: startsWith(github.head_ref, 'dependabot') != true` on top of your job definition to prevent this action running on PRs made by Dependabot.