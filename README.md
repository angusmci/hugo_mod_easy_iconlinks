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

Every website you build with Hugo will probably need `site.webmanifest` and `browserconfig.xml` files, as well as links from your HTML documents to the icons you use. Doing this for each website you build probably involves time-consuming and error-prone copy-pasting. This module simplifies things as much as possible.

Note that this is designed for simplicity, not flexibility. The 'easy' in the name is there for a reason. If you are developing PWAs or Windows web applications, the `site.webmanifest` and `browserconfig.xml` files created will probably be too simple for you.

This is also an *opinionated* project. Among its opinions are:

- manifest files should be called `site.webmanifest` and should live in your root directory
- almost all your icons should live in `/icons` (only `favicon.ico` lives in `/`)
- Andrey Sitnik's ideas about [which icons you need](https://evilmartians.com/chronicles/how-to-favicon-in-2021-six-files-that-fit-most-needs) are largely correct.

### Acknowledgements

The implementation is based largely on `@shedd`'s approach, described in [this Hugo forum thread](https://discourse.gohugo.io/t/solved-is-it-possible-to-use-site-variables-in-manifest-json/14018/6). It follows Andrey Sitnik's recommendations about [current best practices for favicons](https://evilmartians.com/chronicles/how-to-favicon-in-2021-six-files-that-fit-most-needs).

## Install

To use the module, add an import to your `config.toml` as follows:

```
[module]
  [[module.imports]]
    path = 'github.com/angusmci/hugo_mod_easy_iconlinks'
```

If you need to update the module, do:

```
hugo mod get -u
```

## Usage

To generate the `site.manifest` and `browserconfig.xml` files, add the following to your `config.toml` file.

```
[outputFormats]
    [outputFormats.manifest]
        name = "manifest"
        baseName = "site"
        mediaType = "application/manifest+json"
        notAlternative = "true"
    [outputFormats.browserconfig]
        name = "browserconfig"
        baseName = "browserconfig"
        mediaType = "application/xml"
        notAlternative = "true"

[outputs]
    home = [ "HTML", "RSS", "MANIFEST", "BROWSERCONFIG"]
```

If you want to generate one of the files but not the other, just remove the appropriate keyword from `[outputs]`.

The files are generated with sensible defaults, but you can fine-tune the output by adding some parameters to your `.Site.Params`. Parameters you might want to change are:

| Parameter         | Default  | Effect                                                                                  |
|-------------------|----------|-----------------------------------------------------------------------------------------|
| theme_color       | #FFFFFF  | Sets the `TileColor` in `browserconfig.xml` and the `theme_color` in `site.webmanifest` |
| background_color  | #FFFFFF  | Sets the `background_color` in `site.webmanifest`                                       |
| description       |          | If present, adds a `description` in `site.webmanifest`                                  |
| short_name        |          | If present, adds a `short_name` in `site.webmanifest`                                   |

For example, your `config.toml` file could contain:

```
title = "Amalgamated Bread Company"

[params]
short_name = "ABC"
description = "For all your bakery needs"
theme_color = "#FF0000"
background_color = "#FFEEEE"
```

To add the relevant links to the `<head>` of your HTML documents, use the `easy-iconlinks` partial in whatever layouts generate the `<head>` of your document, e.g.

```
{{ partial "easy-iconlinks" . }}
```

This will add the following tags to your `<head>`:

```
<link rel="manifest" href="/site.webmanifest" />
<meta name="msapplication-config" content="/browserconfig.xml" />
<link rel="apple-touch-icon" href="/icons/apple-touch-icon.png" />
<link rel="icon" href="/favicon.ico" sizes="any" />
<link rel="icon" href="/icons/icon.svg" type="image/svg+xml" />
```

Between the various files and the `<head>` of your HTML documents, you will end up with links to the following icons:

| Location                    | Type | Size    | Linked from         |
|-----------------------------|------|---------|---------------------|
| /favicon.ico                | ICO  | 32x32   | `<head>`            |
| /icons/icon.svg             | SVG  | -       | `<head>`            |
| /icons/apple-touch-icon.png | PNG  | 180x180 | `<head>`            |
| /icons/icon-192.png         | PNG  | 192x192 | `site.webmanifest`  |
| /icons/icon-512.png         | PNG  | 512x512 | `site.webmanifest`  |
| /icons/smalltile.png        | PNG  | 70x70   | `browserconfig.xml` |
| /icons/mediumtile.png       | PNG  | 150x150 | `browserconfig.xml` |
| /icons/largetile.png        | PNG  | 310x310 | `browserconfig.xml` |
| /icons/widetile.png         | PNG  | 310x150 | `browserconfig.xml` |

To avoid cluttering your weblogs with 404s, you should ensure that appropriate icons exist at each of these locations.

## Maintainers

[@angusmci](https://github.com/angusmci)

## Contributing

PRs accepted (but remember that the goal is to keep everything as simple as possible; if you want to add a million configuration parameters, fork the repo and call it `flexible-iconlinks` or something like that).

## License

MIT © 2022 Angus McIntyre






