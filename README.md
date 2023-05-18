# project-builder: F´ Github Action 

This repository contains both a Composite Action and a Reusable Workflow that will perform generic building and testing of an F´ project.

## Inputs

Required where no default available.

| input    | default             | description               |
|----------|---------------------|---------------------------|
|          |                     |                           |



## Environment



## Workflow Example

TBC

```
name: Build Package
on:
  release:
    types: [published]
jobs:
  Build-PyPI-Package:
    runs-on: ubuntu-latest
    steps:
    - name: Test PyPI
      uses: fprime-community/publish-pypi@main
      env:
        TWINE_PASSWORD: ${{ secrets.TESTPYPI_CREDENTIAL }}
      with:
        package: "fprime-fpp"
        steps: "sdist"
    - name: PyPI
      uses: fprime-community/publish-pypi@main
      env:
        TWINE_PASSWORD: ${{ secrets.PYPI_CREDENTIAL }}
      with:
        repo: "pypi"
        package: "fprime-fpp"
        steps: "sdist"
```

