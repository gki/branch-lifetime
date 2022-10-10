# Branch lifetime action

## Summary

This action calculates a lifetime of the branch of the pull request.
You can specify the unit of the action output from `hour`(default), `minute` or `second`.

## Setup

```yml
on:
  pull_request:
    # if you want to check lifetime at only closing PR, remove 'synchronize'.
    types: [synchronize, closed]

jobs:
  call-as-actions:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: gki/branch-lifetime@v0.0.3
        id: lifetime
        with:
          # You can set 'hour' or 'minute' as well. Default is 'hour'.
          unit: second
      - name: "Use output"
        run: |
          echo "${{ steps.lifetime.outputs.lifetime }}"
          echo "${{ steps.lifetime.outputs.unit }}"
```
