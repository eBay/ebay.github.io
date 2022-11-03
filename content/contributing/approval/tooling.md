---
title: Tooling
weight: 1
---

When open sourcing a repository, we run a few compliance checks.

## Security
We run snyk on all outgoing repositories. Snyk requires the build to happen, such that all the relevant dependencies are downloaded.

Usage:

```
git clone ...
cd path/to/repo
# do the thing to build the project
snyk test --all-projects
```


## License Compliance
We want to ensure that the software we build is in compliance with our [licensing guidance](../licences.md). This is language dependent.

### Java

Run this to get the dependency license list.
```
mvn org.codehaus.mojo:license-maven-plugin:aggregate-third-party-report
```
When this is done, the result will be in `./target/site/aggregate-third-party-report.html`.

### Node.js

After installing dependencies, run this:
```
npx license-checker --exclude "MIT,ISC,BSD-3-Clause,Apache-2.0,BSD-2-Clause,0BSD,CC-BY-4.0" --unknown
```

That exclusion list should match our known [green license list](../licences.md).

### Python

```
pip3 install --user pylic
cd path/to/repo
touch pyproject.toml
pylic check
```
### Go
```
go install github.com/google/go-licenses@latest
go-licenses check . --allowed_licenses=MIT,ISC,BSD-3-Clause,Apache-2.0,BSD-2-Clause,0BSD,CC-BY-4.0
```

## Repolinter

The TODO group has built a very helpful project around linting repos for adherence to policy.

Install:
```
export GEM_HOME=/tmp
export PATH=/tmp/bin:$PATH
gem install licensee
gem install github-linguist -- --with-icu-dir=/opt/local --with-cxxflags=-Wno-reserved-user-defined-literal
```

Usage:
```
npx repolinter lint . -u https://raw.githubusercontent.com/eBay/.github/main/repolinter.yaml
```

The rules for the linter are [here on github](https://github.com/eBay/.github/blob/main/repolinter.yaml).
