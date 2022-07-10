# Nuitka-Build-Executable-from-Python-Script

This builds a stand-alone executable from a python script using [nuitka](https://github.com/Nuitka/Nuitka), the python compiler.

# Usage

See [action.yml](action.yml)

### Build a python script into an exe

```yaml
jobs:
  build:
    # Windows is currently the only platform this action supports
    runs-on: windows-latest

    steps:
      # Check-out repository
      - uses: actions/checkout@v3

      # Build python script into a stand-alone exe
      - uses: jimkring/nuitka-build-executable-from-python-script@main
        with:
          script-name: test.py
      
      # Uploads artifact
      - name: Upload Artifact
        uses: actions/upload-artifact@v3
        with:
          name: exe
          path: build/test.exe

```

# Limitations

- Currently, this action will use the python version that gets run via the `python` command on the runner. So, you should [setup-python](https://github.com/actions/setup-python) on the runner in a step prior to calling this action.

# Roadmap

- Add input parameters for various nuitka build settings and options
- Support for Mac and Linux
- Allow specifying desired python version
- Optional caching nuitka dependencies (that it self downloads when needed)
- Option to not install package dependencies and rely on dependencies being set in the calling workflow
- Create a repo with various examples and tests for this action

### Python and Package Dependencies

This action installs the following python packages (which are specified in the [requirements.txt](requirements.txt) of this action repo)

```
nuitka==0.9.4
    # via -r requirements.in
ordered-set==4.1.0
    # via -r requirements.in
wheel==0.37.1
    # via -r requirements.in
zstandard==0.18.0
    # via -r requirements.in
```

## Additional Documentation

See [Nuitka](https://github.com/Nuitka/Nuitka) for full documentation on Nuitka. It's really a fantastic tool!


# License

The scripts and documentation in this project are released under the [MIT License](LICENSE).

Nuitka is licensed under the [Apache 2.0 License](https://github.com/Nuitka/Nuitka/blob/develop/LICENSE.txt)

Python is licensed under the [Python Software Foundation (PSF) License](https://github.com/python/cpython/blob/main/LICENSE).

## You are Reponsible for Complying with your Project's Dependencies' Licenses 

This tool compiles and/or copies your project's package dependencies (and their dependencies) into the output executable, which will be considered a combined and/or derivative work of those packages.

> **_Important:_** You are responsibile for compliance with the licenses of your project's package dependencies. Please consult with an attorney about your individual/project's compliance needs and strategy.

## How to Comply With Dependency Package Licenses

There are some great license checker tools that you might consider integrating with your project. Generally speaking, they enable you to specify which licenses (or types) are approved or disaproved and alert you whenever your project has a package dependency that is not approved.

Here are a couple license checker tools:

- [python-license-check](https://github.com/dhatim/python-license-check) - can be run as a GitHub pre-commit hook.
- [dependencies-license-compliance-checker](https://github.com/marketplace/actions/dependencies-license-compliance-checker) - a github action that can be run before your executable build.

