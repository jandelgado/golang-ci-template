# golang travis-ci template

![ci status](https://travis-ci.org/jandelgado/golang-ci-template.svg?branch=master) [![Coverage Status](https://coveralls.io/repos/github/jandelgado/golang-ci-template/badge.svg?branch=master)](https://coveralls.io/github/jandelgado/golang-ci-template?branch=master) [![Go Report Card](https://goreportcard.com/badge/github.com/jandelgado/golang-ci-template)](https://goreportcard.com/report/github.com/jandelgado/golang-ci-template) 


<!-- vim-markdown-toc GFM -->

* [Releasing](#releasing)
    * [travis-ci cli](#travis-ci-cli)
    * [Creating a release](#creating-a-release)
* [Test coverage (coveralls)](#test-coverage-coveralls)

<!-- vim-markdown-toc -->

This repository serves as my template for travis-ci-integrated go projects.  It
consists of a `hello, world!` like example in source file `main.go` which gets
compiled into binary `ci-test`. The `pre-commit` script runs some checks on the
code. When a new release is created, the released-artifacts are automatically
uploaded to github and available on the [release
page](https://github.com/jandelgado/ci-test/releases/).  For demonstration
purposes, both a linux- and windows target is created and packetized in a
zip-archive.

## Releasing

### travis-ci cli

The travis cli tool is recommended to create the encrypted api_key used in
`.travis.yml` file. Example installation on Fedora25:

```
$ sudo dnf install ruby ruby-devel redhat-rpm-config
$ gem install travis -v 1.8.8 --no-rdoc --no-ri
```

Set up deployment in .travis.yml and create encrypted api-key with:
`$ travis setup releases --force`

This will ask some questions and create the `deploy` section in i
the [.travis.yml](.travis.yml), modify it to look like:

```
before_deploy:
- zip ci-test-${TRAVIS_TAG}-windows-amd64.zip ci-test-windows-amd64.exe README.md
- zip ci-test-${TRAVIS_TAG}-linux-amd64.zip ci-test-linux-amd64 README.md
- sha256sum *zip > SHASUMS256.txt

deploy:
  provider: releases
  api_key:
    secure: ZSqZx+Ej1mFm5....
  file: 
    - ci-test-${TRAVIS_TAG}-windows-amd64.zip
    - ci-test-${TRAVIS_TAG}-linux-amd64.zip
  skip_cleanup: true
  on:
    tags: true
```

### Creating a release

On your repositories home (github.com) go to `Releases` > `create realease`.
As soon as the release-tag is created, Travis will run the deployment step.


## Test coverage (coveralls)

Create coveralls account and activate coveralls for repositiory. Encrypt 
coveralls token with `travis encrypt COVERALLS_TOKE="<token>"`.

For instructions on using goveralls look [here](https://coveralls.zendesk.com/hc/en-us/articles/201342809-Go).

