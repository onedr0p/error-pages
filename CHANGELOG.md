# Changelog

All notable changes to this package will be documented in this file.

The format is based on [Keep a Changelog][keepachangelog] and this project adheres to [Semantic Versioning][semver].

## UNRELEASED

### Changed

- It is now possible to use [golang-tags of templates](https://pkg.go.dev/text/template) in error page templates and formatted (`json`, `xml`) responses
- Health-check route become `/healthz` (instead `/health/live`, previous route marked ad deprecated)

### Added

- The templates contain details block now (can be enabled using `--show-details` flag for the `serve` command or environment variable `SHOW_DETAILS=true`)
- Formatted response templates (`json`, `xml`) - the server responds with a formatted response depending on the `Content-Type` (and `X-Format`) request header value
- HTTP header `X-Robots-Tag: noindex` for the error pages
- Possibility to pass the needed error page code using `X-Code` HTTP header
- Possibility to integrate with [ingress-nginx](https://kubernetes.github.io/ingress-nginx/)

### Fixed

- Potential race condition (in the `pick.StringsSlice` struct)

## v2.3.0

### Added

- Flag `--default-http-code` for the `serve` subcommand (`404` is used by default instead of `200`, environment name `DEFAULT_HTTP_CODE`) [#41]

### Changed

- Go updated from `1.17.1` up to `1.17.5`

[#41]:https://github.com/tarampampam/error-pages/issues/41

## v2.2.0

### Added

- Template `cats` [#31]

[#31]:https://github.com/tarampampam/error-pages/pull/31

## v2.1.0

### Added

- `referer` field in access log records
- Flag `--default-error-page` for the `serve` subcommand (`404` is used by default, environment name `DEFAULT_ERROR_PAGE`)

### Changed

- The source code has been refactored
- The index page (`/`) now returns the error page with a code, declared using `--default-error-page` flag (HTTP code 200, when a page code exists)

## v2.0.0

### Changed

- Application rewritten in Go

## v1.8.0

### Added

- Nginx health-check endpoint (`/health/live`) and dockerfile `HEALTHCHECK` to utilise (thx [@modem7](https://github.com/modem7)) [#22], [#23]

[#22]:https://github.com/tarampampam/error-pages/pull/22
[#23]:https://github.com/tarampampam/error-pages/pull/23

## v1.7.2

### Changed

- Nginx updated up to `1.21` (from `1.19`)

## v1.7.1

### Fixed

- Random template selecting (thx [@xpliz](https://github.com/xpliz)) [#12]

[#12]:https://github.com/tarampampam/error-pages/pull/12

## v1.7.0

### Added

- Template `hacker-terminal` [#13]
- HTML comments with error code and description into each template (header and footer, it seems more readable for curl usage)

[#10]:https://github.com/tarampampam/error-pages/pull/13

## v1.6.0

### Added

- Template `noise` [#10]

### Fixed

- File permissions in docker image

[#10]:https://github.com/tarampampam/error-pages/issues/10

## v1.5.0

### Changed

- Repository files structure
- Nginx updated from `1.18` up to `1.19` in docker image
- Docker image now uses default `nginx` entrypoint scripts and command

### Added

- Support for `linux/arm64/v8`, `linux/arm/v6` and `linux/arm/v7` platforms for docker image
- Random template selecting (use `random` as a template name) for docker image

## v1.4.0

### Added

- Template `shuffle` [#4]

[#4]:https://github.com/tarampampam/error-pages/issues/4

## v1.3.1

### Fixed

- `can't create directory '/opt/html/nginx-error-pages'` error [#3]

[#3]:https://github.com/tarampampam/error-pages/issues/3

## v1.3.0

### Added

- `418` status code error page
- Set `server_tokens off;` in `nginx` server configuration

## v1.2.0

### Fixed

- By default `nginx` in docker container returns 404 http code instead 200 when `/` requested

### Changed

- Default value for `TEMPLATE_NAME` is `ghost` now

### Removed

- Environment variable `DEFAULT_ERROR_CODE` support in docker image

### Added

- Templates `l7-light` and `l7-dark`

## v1.1.0

### Added

- Environment variable `DEFAULT_ERROR_CODE` support in docker image

## v1.0.1

### Changed

- Repository (not docker image) renamed from `error-pages-docker` to `error-pages`
- `configuration.json` renamed to `config.json`
- Makefile contains new targets (`install`, `gen`, `preview`)
- Generator logging messages

### Added

- `docker-compose` for development

### Fixed

- Readme file content [#1]

[#1]:https://github.com/tarampampam/error-pages/issues/1

## v1.0.0

### Changed

- First project release

[keepachangelog]:https://keepachangelog.com/en/1.0.0/
[semver]:https://semver.org/spec/v2.0.0.html
