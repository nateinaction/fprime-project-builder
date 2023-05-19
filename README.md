# project-builder: F´ Github Action 

This repository contains both a Composite Action and a Reusable Workflow that will perform generic building and testing on an F´ project, in GitHub Actions.

## Inputs

Required where no default available. 
_Note: Both the Action and the Reusable Workflow take the same input_

| input           | default       | description               |
|-----------------|---------------|---------------------------|
| build_location  |               | The location to build in. E.g. MyDeployment/|
| run_unit_tests  | `true`        | Whether to run Unit Tests|
| fprime_version  | _(See desc.)_ | F´ version to use (branch or tag). Defaults to the version pointed to by the project submodule.|
| fprime_location | `./fprime`    | Relative path from project root to F´ submodule|


## Workflow Example

### Using the Action

```
name: Builder Workflow (Action)

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

### Using the Reusable Workflow

```
name: Builder Workflow (Reusable)

on: [push, pull_request]

jobs:
  build:
    name: ""
    uses: fprime-community/project-builder/.github/workflows/project-builder.yml@main
    with: 
      run_unit_tests: true
      build_location: SampleDeployment
```


