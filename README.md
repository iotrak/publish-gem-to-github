# Release Ruby Gem to GitHub Packages
This action builds the gems for all `.gemspec` files in the projects root and uploads them to [GitHub Packages](https://github.com/features/packages).

## Usage
Example minimal workflow using this action:
```yaml
name: CI

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v1
    - name: Build and publish gem
      uses: iotrak/publish-gem-to-github@master
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        owner: jstastny
        working-directory: gem
```

## Inputs

| Name                | Description                                                                               |
| ------------------- | ----------------------------------------------------------------------------------------- |
| `token`             | GitHub token that has write access to Packages. You can use `secrets.GITHUB_TOKEN`        |
| `owner`             | Name of the user or organization account that owns the repository containing your project |
| `working-directory` | Name of the working directory that contains the gemspecs                                  |

## Versioning your gem

This action currently does not bump the gem's version when building it. It is up to you to do it (either manually or in a previous workflow step).
If you try to release gem in the same version that already exists, the step will fail.

In case you want to ignore these types of failures, you can add:

```
continue-on-error: true
```

to the build step configuration.
