# hugo-mod-easy-iconlinks

[![standard-readme compliant](https://img.shields.io/badge/standard--readme-OK-green.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

A small [module](https://gohugo.io/hugo-modules/) for [Hugo](https://gohugo.io/) to simplify adding standard icon links to web pages.

The module generates `site.webmanifest` and `browserconfig.xml` files for your site, and provides a partial layout called `easy-iconlinks` that you can add to your layouts to create appropriate links in the `<head>` of your documents.

It does *not* generate or place icons for you. It just creates links.

## Table of Contents

- [Background](#background)
- [Install](#install)
- [Usage](#usage)
- [API](#api)
- [Maintainers](#maintainers)
- [Contributing](#contributing)
- [License](#license)

## Background

Every website you build with Hugo will probably need `site.webmanifest` and `browserconfig.xml` files, as well as links from your HTML documents to the icons you use. Doing this for each website you build probably involves time-consuming and error-prone copy-pasting. This module uses the power of Hugo modules to simplify things as much as possible.

Note that this is designed for simplicity, not flexibility. The 'easy' in the name is there for a reason. If you are developing PWAs or Windows web applications, the `site.webmanifest` and `browserconfig.xml` files created will probably be too simple for you.

This is also an *opinionated* project. Among its opinions are:

- manifest files should be called `site.webmanifest` and should live in your root directory
- almost all your icons should live in `/icons` (only `favicon.ico` lives in `/`)
- Andrey Sitnik's ideas about [which icons you need](https://evilmartians.com/chronicles/how-to-favicon-in-2021-six-files-that-fit-most-needs) are largely correct.

### Acknowledgements

The implementation is based largely on `@shedd`'s approach, described in [this Hugo forum thread](https://discourse.gohugo.io/t/solved-is-it-possible-to-use-site-variables-in-manifest-json/14018/6). It follows Andrey Sitnik's recommendations about [current best practices for favicons](https://evilmartians.com/chronicles/how-to-favicon-in-2021-six-files-that-fit-most-needs).

## Install

```
```

## Usage

```
```

## API

## Maintainers

[@angusmci](https://github.com/angusmci)

## Contributing

PRs accepted.

Small note: If editing the README, please conform to the [standard-readme](https://github.com/RichardLitt/standard-readme) specification.

## License

MIT © 2022 Angus McIntyre






