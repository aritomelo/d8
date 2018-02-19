Testing Drupal 8 with composer, docker, task Runner(from Open-europa)
=====================


[Task Runner](https://github.com/ec-europa/oe-task-runner) From ec-europa @European Commission




## Development setup

You can build a test site by running the following steps.

* Install all the composer dependencies:

```
$ composer install
```

* Customize build settings by copying `runner.yml.dist` to `runner.yml` and
changing relevant values.

* Setup test site by running:

```
$ ./vendor/bin/run drupal:site-setup
```

This will symlink the theme in the proper directory within the test site and
perform token substitution in test configuration files such as `behat.yml.dist`.

* Install test site by running:

```
$ ./vendor/bin/run drupal:site-install
```

Your test site will be available at `./build`.

### Using Docker Compose

Alternatively you can build a test site using Docker and Docker-compose with the
provided configuration.

Requirements:

- [Docker](https://www.docker.com/get-docker)
- [Docker-compose](https://docs.docker.com/compose/)

Run:

1- Start the container:
```
$ docker-compose up -d
```

2- Get into container image:
```
$ docker-compose exec web /bin/bash
```
3- Install dependencies via composer:
```
$ composer install
```

4- Setup, it will fire the task runner and create a drupal strucuture:
```
$ ./vendor/bin/run drupal:site-setup
```

5- Install Drupal Site (using task runner)
```
$ ./vendor/bin/run drupal:site-setup
```

Or, you could skip 2, and do 3,4 and 5 as shown below:
```
$ docker-compose exec -u web web composer install
$ docker-compose exec -u web web ./vendor/bin/run drupal:site-setup
$ docker-compose exec -u web web ./vendor/bin/run drupal:site-install
```

Your test site will be available at
[http://localhost:8080/build](http://localhost:8080/build).
