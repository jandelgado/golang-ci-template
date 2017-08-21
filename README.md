# Go CI template
![ci status](https://travis-ci.org/jandelgado/ci-test.svg?branch=master)

This repository serves as my template for travis-integration of go projects.
It consists of a `hello, world!` like example in source file `main.go` which
gets compiled into binary `ci-test`. The `pre-commit` script runs some checks
on the code. When a new release is created, the released-artifacts are 
automatically uploaded to github and available on the [release page](https://github.com/jandelgado/ci-test/releases/).

## Releasing
### recommended client tools
#### travis cli
```
$ sudo dnf install ruby ruby-devel redhat-rpm-config
$ gem install travis -v 1.8.8 --no-rdoc --no-ri
```

Set up deployment in .travis.yml and create encrypted api-key with:
`$ travis setup release --force`

This will ask some questions and create the `deploy` section in i
the [.travis.yml](.travis.yml) file:
```
deploy:
  provider: releases
  api_key:
    secure: ZSqZx+Ej1m........
  file: ci-test
  on:
    repo: jandelgado/ci-test
```

### Creating a release

## TODO
- add glide example
- add unit tests

