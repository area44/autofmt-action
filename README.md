# autofmt

This GitHub Action provides a reusable Composite Action for fast JavaScript and TypeScript formatting using `oxfmt` (the Oxc formatter).

## Features

- **Blazing Fast**: Powered by Oxc, the fastest JavaScript toolchain.
- **Auto-commit**: Automatically detects changes and pushes formatted code back to your branch.
- **Default Formatting Rules**: Includes sensible defaults for import sorting.
- **Zero Repo Noise**: Provide rules and ignore patterns directly in your workflow file - no need for extra files in your repository.
- **CI Friendly**: Automatically adds `[skip ci]` to prevent recursive workflow runs.

## Usage

Create a file named `.github/workflows/autofmt.yml` in your repository:

```yaml
name: Format

on:
  push:
    branches: ["main"]
  pull_request:

permissions:
  contents: write

jobs:
  format:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1 # v7

      - name: Run autofmt
        uses: area44/autofmt-action@d2c585d7e412b237cde77b054c680835fc5d3999 # v0.1.0
```

## Default Configuration

If no `rules` or `ignore` are provided, the following defaults are used:

### Default Ignore Patterns

- `*.min.*`, `*.map`
- `**/public`, `**/build`, `**/dist`, `**/out`
- `**/.github`, `**/.next`, `**/.astro`, `**/.netlify`
- `**/*.gen.*`

### Formatting Rules

- **Import Sorting**: Groups imports by type, builtins/externals, internal, parents, and siblings.

## Configuration

| Input    | Description                                                   | Default    |
| -------- | ------------------------------------------------------------- | ---------- |
| `rules`  | JSON string of formatting rules (merged with defaults)        | (optional) |
| `ignore` | Multiline string of patterns to ignore (appended to defaults) | (optional) |

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
