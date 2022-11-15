---
title: Tooling
weight: 1
---

When open sourcing a repository, we run a few compliance checks.

## Security
We run snyk on all outgoing repositories. Snyk requires the build to happen, such that all the relevant dependencies are downloaded.

When installing snyk, it may ask you to log in. Do so with the company sso option.

Usage:

```
git clone ...
cd path/to/repo
# do the thing to build the project
npx snyk test --all-projects
```

The output of that command will say if there are issues. If so, post it to the relevant ticket and have that person address them before open sourcing it.


## License Compliance
We want to ensure that the software we build is in compliance with our [licensing guidance](../licences.md). This is language dependent. The result of this should be a list of problematic licenses. If all are of the licenses that are output are on our approved list, this step passes.

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

You'll need to install [docker](https://docker.com/)

Usage:
```
cd /path/to/repo
docker run -it  -v $PWD:/source ghcr.io/todogroup/repolinter:v0.11.2  /source -u https://raw.githubusercontent.com/eBay/.github/main/repolinter.yaml
```

The rules for the linter are [here on github](https://github.com/eBay/.github/blob/main/repolinter.yaml).

It's expected that "integrates-with-ci" may not be done, given it hasn't existed in a github-actions environment until it's been open sourced. All other items in the list should be addressed before open sourcing it.
