# Contributing

Have you read the [Appsilon Contributing
Guidelines](https://github.com/Appsilon/.github/blob/main/CONTRIBUTING.md)?

## pre-commit

This project uses [pre-commit](https://pre-commit.com) hooks. The hooks
are a series of automated checks run locally. These automate mundane
tasks such as running spellchecking, linter, and other potential issues
before you even push your changes!

### Getting Started

To get started you need to install the pre-commit tool. Additionally,
[lintr](https://lintr.r-lib.org), [pkgdown](https://pkgdown.r-lib.org/),
and [testthat](https://testthat.r-lib.org) packages have to be installed
either globally or within [renv](https://rstudio.github.io/renv/) (if
your project uses it). To install pre-commit, pick a method that suits
you the best:

- using pip (package installer for Python): `pip install pre-commit` or
  `pip3 install pre-commit`
- using homebrew: `brew install pre-commit`
- using [precommit](https://lorenzwalthert.github.io/precommit/)
  package: follow [the installation section in its
  vignette](https://lorenzwalthert.github.io/precommit/articles/precommit.html#installation)

Once you have installed pre-commit, run `pre-commit install` to set up
the hooks.

### Modifying Package Dependencies

If package dependencies are being changed, then the list of
`additional_dependencies` for `roxygenize` hook has to be updated. The
list can be generated using a helper function from
[precommit](https://lorenzwalthert.github.io/precommit/) package:
`precommit::snippet_generate("additional-deps-roxygenize")`.

### Known Issues

- If you use MacOS and have installed R via homebrew, then chances are
  that pre-commit will fail to setup an environment. A workaround is
  installing R by other means, e.g. by using
  [rig](https://github.com/r-lib/rig).
- [lintr](https://lintr.r-lib.org) might report false positive warnings
  about `object_usage_linter`. This can be fixed by install the package
  with your contributions prior to running the linter.
