# GitHub Actions - Changed Paths

GitHub action used to get the changed paths between two commits or refs.

**Organization:** LerianStudio

## Inputs

| Name           | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| `filter-string` | (Optional) Filters changed paths to only include those containing this string (e.g., `infra`, `frontend`). |

## Outputs

| Name    | Description                                                                 |
|---------|-----------------------------------------------------------------------------|
| `matrix` | A JSON array of changed directories (optionally filtered), suitable for use in a matrix strategy. |

## Env vars

This action does not export any environment variables.

## Example usage

```yaml
      # Example using this action
      - name: Get changed paths
        uses: LerianStudio/github-actions-changed-paths@main
        with:
          filter-string: components

      # Example using the matrix output
      - name: Run for each changed path
        uses: actions/checkout@v4

      - run: echo "Changed path: ${{ matrix.path }}"
        strategy:
          matrix:
            path: ${{ fromJson(needs.get-changed-paths.outputs.matrix) }}
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

