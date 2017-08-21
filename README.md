# ci-test
Just testing travis-ci ...

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
the (.travis.yml)[.travis.yml] file:
```
deploy:
  provider: releases
  api_key:
    secure: ZSqZx+Ej1m........
  file: main
  on:
    repo: jandelgado/ci-test
```

### Creating a release


