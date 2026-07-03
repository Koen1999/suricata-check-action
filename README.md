# Suricata Check Action

This action runs `suricata-check` to validate rules and highlight issues in Pull Requests. It is available as both a **Composite Action** and a **Reusable Workflow**.

## Installation

### Using as a Composite Action

To use this action as a composite action, add it to your workflow file:

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: Koen1999/suricata-check-action@master
    with:
      python_version: "3.x"
      extra_packages: "requests,pandas"
      extra_args: "--ini suricata-check.ini"
```

### Using as a Reusable Workflow

To use this action as a reusable workflow, call it from your workflow file:

```yaml
jobs:
  lint:
    uses: Koen1999/suricata-check-action@master
    with:
      python_version: "3.x"
      extra_packages: "requests,pandas"
      extra_args: "--ini suricata-check.ini"
```

## Examples

Here are some examples of how to use the `extra_args` input to customize the check:

```yaml
- uses: Koen1999/suricata-check-action@master
  with:
    python_version: "3.x"
    # Pass multiple arguments as a space-separated string
    extra_args: "--include /path/to/rules --issue-severity=WARNING"
```

You can combine various flags such as `--include`, `--exclude`, and `--issue-severity` in the `extra_args` string.
More details on the available arguments can be found in the [CLI Usage documentation](https://suricata-check.teuwen.net/cli.html).

| Name             | Description                                                                      | Default |
| ---------------- | -------------------------------------------------------------------------------- | ------- |
| `python_version` | The version of Python to use (e.g., "3.10" or "3.x")                             | `3.x`   |
| `extra_packages` | Additional Python packages to install (comma-separated, e.g., "requests,pandas") | ``      |
| `extra_args`     | Additional arguments to pass to suricata-check                                   | ``      |

### Output

For example, when integrated with GitHub, issues can be highlighted in a pull requests (PRs) similar to [this example PR](For example, when integrated with GitHub, issues can be highlighted in a pull requests (PRs) similar to this example PR.).

## Details

The action performs the following steps:

1. Sets up a Python environment.
2. Installs the `suricata-check` package with performance enhancements.
3. Optionally installs additional Python packages (i.e., [suricata-check extensions](https://suricata-check.teuwen.net/checker.html#releasing-checkers-as-a-package)) specified in the `extra_packages` input.
4. Runs `suricata-check --github` to perform the check and output results for GitHub integration.

While some tools only validate that a rule is syntactically correct and can be parsed by the Suricata engine, `suricata-check` provides a comprehensive static analysis without relying on the Suricata engine. It evaluates critical factors that standard syntax parsing does not, such as runtime performance, the likelihood of false positives, and whether the rule effectively detects its intended target.

For more information on usage for Continuous Integration and Continuous Deployment (CI/CD), please refer to the [suricata-check CI/CD documentation](https://suricata-check.teuwen.net/ci_cd.html).
