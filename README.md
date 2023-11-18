# setup-nupm-action
A GitHub action to setup Nupm to run tests for Nushell packages.

## Examples
- a simple workflow to setup Nushell `0.87.0` and Nupm `f7c0843` and finally run the tests of a
Nushell package
```yml
on:
  pull_request:
  push:
    branches:
      - main

env:
  NU_LOG_LEVEL: DEBUG

defaults:
  run:
    shell: nu {0}

jobs:
  nupm-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Setup Nushell and Nupm
        uses: amtoine/setup-nupm-action@0.1.1
        with:
          nu_version: "0.87.0"
          nupm_revision: "f7c0843f4d667194beae468614a46cc8d72cc5db"

      - name: Run the tests
        run: |
          use ${{ steps.nu-setup.outputs.nupm_path }}
          nupm test --show-stdout
```
