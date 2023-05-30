# project-builder: F´ Github Action 

This repository contains **both** a _Composite Action_ **and** a _Reusable Workflow_ that will perform generic building and testing on an F´ project, in GitHub Actions.

Choosing between using the reusable workflow or composite action can be a matter of personal preference or use case.

- **Reusable Workflow**: allows for step-by-step exploration of the `project-builder` workflow logs, with different jobs for building the project versus running the UTs. You can not perform additional steps before or after the execution of the Workflow.

- **Composite Action**: allows for additional steps to be performed before/after the execution of the Action. The output of the `project-builder` action will be condensed in a single step output.

## Inputs

_Note: Both the Composite Action and the Reusable Workflow take the same input_

| input           | default       | description               |
|-----------------|---------------|---------------------------|
| build_location  |               | **Required:** The location to build in. For example: `MyDeployment/`|
| run_unit_tests  | `true`        | Whether to run Unit Tests|
| fprime_version  |               | F´ version to use (branch or tag). Defaults to the version pointed to by the project submodule.|
| fprime_location | `./fprime`    | Relative path from project root to F´ submodule|
| runs_on         |               | Platform to run on. Defaults to ubuntu-latest|


## Workflow Example

### Using the Reusable Workflow

```yaml
name: Builder Workflow (Reusable Workflow)

on: [push, pull_request]

jobs:
  build:
    name: ""
    uses: fprime-community/project-builder/.github/workflows/project-builder.yml@main
    with: 
      run_unit_tests: true
      build_location: SampleDeployment
```

### Using the Action

```yaml
name: Builder Workflow (Composite Action)

on: [push, pull_request]

jobs:
  build:
    name: Build and Test
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
      with:
        submodules: recursive
    - uses: fprime-community/project-builder@main
      with:
        run_unit_tests: true
        build_location: SampleDeployment
```


