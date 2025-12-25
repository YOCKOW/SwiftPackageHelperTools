#  What is this repository?

This repository contains some niche tools for Swift packages.

## How to install?

1. Clone this repository: `git clone https://github.com/YOCKOW/SwiftPackageHelperTools.git`
2. Add `/path/to/repository/SwiftPackageHelperTools/bin` to `PATH` environment variable.

### Alternative

- Copy `./bin/spm-helper` into one of your `PATH` directories.


## Tools

You can invoke subcommands through `spm-helper`:

```console
spm-helper <subcommand> [options]
```


### `collect-licenses`

This subcommand collects licenses of packages which the root package depends on.

Sample command:

```console
spm-helper collect-licenses --package-path . --directory /my/path/to/licenses
```


### `dep-json`

This subcommand prints the resolved dependency graph with JSON format.  
This is equivalent to `swift package show-dependencies --format json`.


### `dep-pretty-dot`

This subcommand prints the resolved dependency graph with DOT format.  
The generated DOT outputs are prettier than `swift package show-dependencies --format dot`.

#### Samples:

- Raw: [sample.dot](./sample.dot)
- SVG: [sample.dot.svg](./sample.dot.svg) ![sample.dot.svg](./sample.dot.svg)


### `dep-mermaid`

This subcommand prints the resolved dependency graph with Mermaid format.  

#### Samples

- Raw: [sample.mmd](./sample.mmd)

<!-- SWIFT PACKAGE DEPENDENCIES MERMAID START -->
```mermaid
---
title: HelperTestPackage Dependencies
---
flowchart TD
  helpertestpackage["HelperTestPackage"]
  swiftbootstring(["Bootstring<br>@1.2.0"])
  swiftcgiresponder(["CGIResponder<br>@0.12.0"])
  swiftnetworkgear(["NetworkGear<br>@0.19.5"])
  swiftpublicsuffix(["PublicSuffix<br>@2.4.0"])
  swiftranges(["Ranges<br>@3.2.2"])
  swiftstringcomposition(["StringComposition<br>@2.2.0"])
  swifttemporaryfile(["TemporaryFile<br>@4.2.1"])
  swifttimespecification(["TimeSpecification<br>@3.4.0"])
  swiftunicodesupplement(["UnicodeSupplement<br>@1.7.0"])
  swiftxhtml(["XHTML<br>@2.8.0"])
  yswiftextensions(["yExtensions<br>@1.12.1"])

  click swiftbootstring href "https://github.com/YOCKOW/SwiftBootstring.git"
  click swiftcgiresponder href "https://github.com/YOCKOW/SwiftCGIResponder.git"
  click swiftnetworkgear href "https://github.com/YOCKOW/SwiftNetworkGear.git"
  click swiftpublicsuffix href "https://github.com/YOCKOW/SwiftPublicSuffix.git"
  click swiftranges href "https://github.com/YOCKOW/SwiftRanges.git"
  click swiftstringcomposition href "https://github.com/YOCKOW/SwiftStringComposition.git"
  click swifttemporaryfile href "https://github.com/YOCKOW/SwiftTemporaryFile.git"
  click swifttimespecification href "https://github.com/YOCKOW/SwiftTimeSpecification.git"
  click swiftunicodesupplement href "https://github.com/YOCKOW/SwiftUnicodeSupplement.git"
  click swiftxhtml href "https://github.com/YOCKOW/SwiftXHTML.git"
  click yswiftextensions href "https://github.com/YOCKOW/ySwiftExtensions.git"

  helpertestpackage --> swiftcgiresponder
  swiftcgiresponder --> swiftnetworkgear
  swiftcgiresponder --> swifttemporaryfile
  swiftcgiresponder ----> swifttimespecification
  swiftcgiresponder --> swiftxhtml
  swiftcgiresponder --> yswiftextensions
  swiftnetworkgear ----> swiftbootstring
  swiftnetworkgear ----> swiftpublicsuffix
  swiftnetworkgear ----> swiftranges
  swiftnetworkgear --> swifttemporaryfile
  swiftnetworkgear --> swiftunicodesupplement
  swiftnetworkgear --> yswiftextensions
  swiftstringcomposition --> yswiftextensions
  swifttemporaryfile ----> swiftranges
  swifttemporaryfile --> yswiftextensions
  swiftunicodesupplement ----> swiftranges
  swiftxhtml --> swiftnetworkgear
  swiftxhtml ----> swiftranges
  swiftxhtml --> swiftstringcomposition
  swiftxhtml --> swiftunicodesupplement
  swiftxhtml --> yswiftextensions
  yswiftextensions ----> swiftranges
  yswiftextensions --> swiftunicodesupplement


```
<!-- SWIFT PACKAGE DEPENDENCIES MERMAID END -->


- SVG: [sample.mmd.svg](./sample.mmd.svg) ![sample.mmd.svg](./sample.mmd.svg)

## GitHub Actions' workflow

This repository contains [reusable workflow](./.github/workflows/reusable_update-dependencies-files.yml).
You can use the workflow in your repository like this:

```yaml
name: Update dependencies files.
on:
  push:
    branches:
      - '**'
    paths:
      - '**/Package.swift'
permissions:
  contents: write
  pull-requests: write
jobs:
  update-dependencies-files:
    uses: YOCKOW/SwiftPackageHelperTools/.github/workflows/reusable_update-dependencies-files.yml@main
    with:
      swift-version: "6.2.3"
      dot-derived-svg-file: "./dependencies.dot.svg"
    secrets:
      gh-token: ${{ secrets.GITHUB_TOKEN }}
```

Other available parameters(inputs) can be seen in the YAML file: [reusable_update-dependencies-files.yml](.github/workflows/reusable_update-dependencies-files.yml).

# License

MIT License.  
See "LICENSE.txt" for more information.
