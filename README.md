# Check Git(hub) environment configuration

Github Action to output the workflow and git environment in variables

# Outputs

| Variable         | Description                                                                                      | Value                          | Type    |
| ---------------- | ------------------------------------------------------------------------------------------------ | ------------------------------ | ------- |
| trigger_type     | The type of the trigger                                                                          | automatic \| manual            | string  |
| tagged           | Whether the trigger was a tag                                                                    | true \| false                  | boolean |
| pre-release      | Whether the tag is a semver pre-release tag                                                      | true \| false                  | boolean |
| last-tag         | The last tag (before the current one that triggered the workflow, if tagged=true)                | semver tag i.e., 1.2.3-1       | string  |
| last-release-tag | The last semver release tag (before the current one that triggered the workflow, if tagged=true) | semver release tag i.e., 1.2.3 | string  |

# How to use

```yaml
name: Example workflow

on:
  push:
    branches:
      - main  # Set a branch name to trigger deployment
  workflow_dispatch:

jobs:
  print-environment:
    runs-on: ubuntu-22.04
    steps:
      - uses: spschlegel/action-env-config
        id: env-config

      - name: Print config
        run: |
	      "echo Trigger: ${{ steps.env-config.trigger_type }}"
	      "echo Tagged?: ${{ steps.env-config.tagged }}"
	      "echo Pre-release?: ${{ steps.env-config.pre-release }}"
	      "echo Last tag: ${{ steps.env-config.last-tag }}"
	      "echo Last release tag: ${{ steps.env-config.last-release-tag }}"
```
