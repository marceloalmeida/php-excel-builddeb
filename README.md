# Buildtask for PHP Excel extension

[![Build Status](https://travis-ci.org/marcelosousaalmeida/php-excel-builddeb.svg?branch=master)](https://travis-ci.org/marcelosousaalmeida/php-excel-builddeb)

Task to build Debian package of PHP Excel extension.


## Dependencies

* [libxl 3.8.2](http://www.libxl.com/download/libxl-lin-3.8.2.tar.gz)


## Usage

```sh
# cd (PHP version)
$ docker-compose build
$ docker-compose run --rm builder
$ ls -1 pkg/
```
