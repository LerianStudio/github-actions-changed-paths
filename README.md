# GitHub Actions - Changed Paths

GitHub action used to get the changed paths between two commits or refs.

**Organization:** LerianStudio

## Inputs

| Name            | Required | Description                                                                 |
|-----------------|----------|-----------------------------------------------------------------------------|
| `filter_paths`  | No       | Optional. A list of path prefixes to filter results. One per line.          |
| `path_level`    | No       | Optional. Limits the output path to the first N segments.                   |
| `get_app_name`  | No       | Optional. If true, outputs a matrix with `name` and `working_dir` fields for each app. Assumes second path segment is the app name. |
| `app_name_prefix` | No | Optional. Adds a prefix to the generated app names when `get_app_name` is enabled. Ignored if `get_app_name` is false. |

## Outputs

| Name    | Description                                                                 |
|---------|-----------------------------------------------------------------------------|
| `matrix` | A JSON array of changed directories (optionally filtered), suitable for use in a matrix strategy. |

## Env vars

This action does not export any environment variables.

## Example usage

```yaml
  name: Run per changed path

  on:
    push:
      branches: [main]

  jobs:
    # Example using this action
    get-changed-files:
      runs-on: ubuntu-latest
      outputs:
        matrix: ${{ steps.changed-paths.outputs.matrix }}
      steps:
        - name: Get changed paths
          id: changed-paths
          uses: LerianStudio/github-actions-changed-paths@main
          with:
            filter_paths: |-
              components/onboarding
              components/transaction
            get_app_name: true
            path_level: 2
            app_name_prefix: midaz

    # Example using the matrix output
    run-per-path:
      needs: get-changed-files
      runs-on: ubuntu-latest
      if: needs.get-changed-files.outputs.matrix != '[]'
      strategy:
        matrix:
          path: ${{ fromJson(needs.get-changed-files.outputs.matrix) }}
      steps:
        - name: Echo changed path
          run: echo "${{ matrix.path }}"

```

## Requirements

This action uses `jq` to handle JSON formatting.
It is **preinstalled** on all GitHub-hosted runners (e.g., `ubuntu-latest`).

If you're using a **self-hosted runner**, make sure `jq` is available in the environment:

```bash
# Example installation (Debian/Ubuntu)
sudo apt-get update && sudo apt-get install -y jq
```

## How to send updates?

To contribute to this action, please follow the steps outlined in our [CONTRIBUTING.md](CONTRIBUTING.md) guide.

There you'll find instructions for forking the repository, creating a feature branch, and opening a pull request to the `develop` branch.

