# Branch lifetime action

## Summary

This action calculates a lifetime of the branch of the pull request.
You can specify the unit of the action output from `hour`(default), `minute` or `second`.

## Note

If this action is triggered by events except `pull_request`, all calculation will be skipped and outputs will be empty.

## Setup

```yml
on:
  pull_request:
    # if you want to check lifetime at only closing PR, remove 'opened' and 'synchronize'.
    types: [opened, synchronize, closed]

jobs:
  call-as-actions:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: gki/branch-lifetime@v1
        id: lifetime
        with:
          # You can set 'hour' or 'minute' as well. Default is 'hour'.
          unit: second
      - name: "Use output"
        run: |
          echo "${{ steps.lifetime.outputs.lifetime }}"
          echo "${{ steps.lifetime.outputs.unit }}"
```

## Why checking branch lifetime?

According State of DevOps and the book "Accelerate", the four metrics are super important for today's software project.

- Deployment Frequency
- Cycle Time (Change Lead Time)
- Mean Time to Recovery (MTTR)
- Change Failure Rate

Ideally, we should measure them from day one, but it's unrealistic since they are related to the production release.
However, it should be nice if we can track one of the similar metrics as soon as possible.

To do that, let's see 'Deployment Frequency' and 'Cycle Time'. They are normally tracked by a ticket (maybe), but they include a time between the first commit of a branch and the merge of the branch, and that time, the branch lifetime, will be the greater part of them.

If any other part is bigger than the branch lifetime, yes, it's problematic. But to notice that, checking branch lifetime should help you.

That's why I created this action. I think this tool doesn't directly give an insight of our project health, the lifetime will be unstable in the very first period. I will use this tool by myself and would like to try to get something from this metric as a one of the users. 🤞
