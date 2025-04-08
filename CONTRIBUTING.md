# Contributing to github-actions-changed-paths

Thank you for your interest in contributing to **github-actions-changed-paths**.
This guide outlines how to propose changes and participate in development.

## How to Contribute

1. Fork this repository to your own GitHub account.
2. Create a branch from `develop` for your changes:

   ```bash
   git checkout -b feature/my-change
   ```

3. Make your changes, commit, and push them to your fork.
4. Open a pull request to the `develop` branch of this repository.
5. Provide a clear description of your changes in the pull request and reference any related issues.

## Requirements

- Follow the existing code style and structure.
- Test your changes in a GitHub Actions environment before submitting.
- Ensure `jq` is available if your changes rely on JSON processing in shell scripts.
- Keep pull requests focused on a single topic or feature.

## Discussions and Issues

- Use the [Issues](../../issues) tab to report bugs or request features.
- Use the [Discussions](../../discussions) tab for general questions or ideas.

## Branching Strategy

- `main`: Production-ready code.
- `develop`: Active development branch. Pull requests should target this branch.
- `feature/*`: Feature branches should be based on `develop`.

Thank you for contributing to this project.
