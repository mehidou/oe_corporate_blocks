# OpenEuropa Corporate Blocks

[![Build Status](https://drone.fpfis.eu/api/badges/openeuropa/oe_corporate_blocks/status.svg?branch=master)](https://drone.fpfis.eu/openeuropa/oe_corporate_blocks)

**Table of contents:**

- [Description](#description)
- [Installation](#installation)
- [Development setup](#development-setup)
- [Contributing](#contributing)
- [Versioning](#versioning)

## Description

OpenEuropa Corporate Blocks is a Drupal module built to contain European Commission corporate blocks.

This currently contains:

- [The European Commission footer](./src/Plugin/Block/EcFooterBlock.php): ships with a set of links and references that
  must be present on all European Commission sites. 
- [The European Union footer](./src/Plugin/Block/EuFooterBlock.php): ships with a set of links and references that must
  be present on all European Union sites. 
 
Both footer blocks will received the proper styling when used in conjunction with the
[OpenEuropa Theme](https://github.com/openeuropa/oe_theme/) component, version 2.x.

### Site specific footer links

The OpenEuropa Corporate Blocks also allows site builders to display a set of site specific links in the footer.
Such links can be of two types:

- Generic links, such as a contact or legal disclaimer link. Generic links can be managed at the following page:
  `/admin/config/footer_link_general`
- Social media footer links, such as a link to a Facebook page or a Twitter account. Social media footer links can be
  managed at the following page: `/admin/config/footer_link_social`

Site specific links can be managed by roles having the `Administer site specific footer links` permission.

## Installation

The recommended way of installing the OpenEuropa Corporate Blocks module is via [Composer](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-osx).

```bash
composer require openeuropa/oe_corporate_blocks
```

### Enable the module

In order to enable the module in your project run:

```bash
./vendor/bin/drush en oe_corporate_blocks
```

## Development setup

You can build the test site by running the following steps.

* Install all the composer dependencies:

```bash
composer install
```

* Customize build settings by copying `runner.yml.dist` to `runner.yml` and
changing relevant values, like your database credentials.

* Install test site by running:

```bash
./vendor/bin/run drupal:site-install
```

Your test site will be available at `./build`.

### Using Docker Compose

Alternatively, you can build a development site using [Docker](https://www.docker.com/get-docker) and 
[Docker Compose](https://docs.docker.com/compose/) with the provided configuration.

Docker provides the necessary services and tools such as a web server and a database server to get the site running, 
regardless of your local host configuration.

#### Requirements:

- [Docker](https://www.docker.com/get-docker)
- [Docker Compose](https://docs.docker.com/compose/)

#### Configuration

By default, Docker Compose reads two files, a `docker-compose.yml` and an optional `docker-compose.override.yml` file.
By convention, the `docker-compose.yml` contains your base configuration and it's provided by default.
The override file, as its name implies, can contain configuration overrides for existing services or entirely new 
services.
If a service is defined in both files, Docker Compose merges the configurations.

Find more information on Docker Compose extension mechanism on [the official Docker Compose documentation](https://docs.docker.com/compose/extends/).

#### Usage

To start, run:

```bash
docker-compose up
```

It's advised to not daemonize `docker-compose` so you can turn it off (`CTRL+C`) quickly when you're done working.
However, if you'd like to daemonize it, you have to add the flag `-d`:

```bash
docker-compose up -d
```

Then:

```bash
docker-compose exec web composer install
docker-compose exec web ./vendor/bin/run drupal:site-install
```

Using default configuration, the development site files should be available in the `build` directory and the development site
should be available at: [http://127.0.0.1:8080/build](http://127.0.0.1:8080/build).

#### Running the tests

To run the grumphp checks:

```bash
docker-compose exec web ./vendor/bin/grumphp run
```

To run the phpunit tests:

```bash
docker-compose exec web ./vendor/bin/phpunit
```

To run the behat tests:

```bash
docker-compose exec web ./vendor/bin/behat
```

#### Upgrade from 1.x to 2.x

`Site Switcher` block has been removed.

## Contributing

Please read [the full documentation](https://github.com/openeuropa/openeuropa) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the available versions, see the [tags on this repository](https://github.com/openeuropa/oe_corporate_blocks/tags).
