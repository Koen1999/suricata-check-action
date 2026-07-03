# Contributing to suricata-check-action

Thank you for your interest in contributing to `suricata-check-action`! 

## Development Workflow

To ensure your changes don't break the action, we use a combination of local testing with `act` and automated verification via GitHub Actions.

### Local Testing with `act`

You can run the GitHub Action workflows locally using [act](https://github.com/nektos/act). This is the fastest way to iterate on changes.

1.  **Install act**: Follow the instructions on the [act GitHub page](https://github.com/nektos/act) to install it on your machine.
2.  **Configure Environment**: Ensure you have Docker installed and running.
3.  **Run the workflow**: From the root of this repository, run:
    ```bash
    act
    ```
    This will execute all workflows defined in `.github/workflows`, including our verification workflow.

### Automated Verification

Every pull request should trigger the verification workflow. This workflow runs `suricata-check` against a set of test rules and configurations stored in the `tests/` directory.

To run the verification workflow specifically:
```bash
act -j verify-suricata-check
```

### Guidelines

-   **Tests First**: Always ensure that your changes pass the verification workflow before submitting a Pull Request.
-   **Style**: We follow standard Python and YAML conventions. Please run `black` and `ruff` on your changes before pushing.
-   **Issues**: If you find a bug, please open an issue with a clear description and, if possible, a minimal reproducible example.

## Pull Request Process

1.  Fork the repository and create a new branch.
2.  Make your changes and ensure they pass local tests.
3.  Submit a Pull Request with a clear description of the changes.
4.  Be prepared to engage in discussion and address any feedback from the maintainers.
