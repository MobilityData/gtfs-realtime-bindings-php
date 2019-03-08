# How-To Update Bindings When gtfs-realtime.proto Changes

## Regenerate the language binding source from gtfs-realtime.proto.

## One-Time Setup

1. Download and setup [php](http://www.php.net/).  As of February 2019 we're using 7.3.3.
1. Download and install [Composer](https://getcomposer.org/)
1. Make sure you have all [Composer](https://getcomposer.org/) dependencies
installed by running:

```
composer update
```

**FIXME:** *As of February 2019, the official `google-protobuf` Google protoc tool [doesn't support proto2 files](https://github.com/protocolbuffers/protobuf/issues/3623).  As a result we are deprecating the PHP bindings until official support for proto2 files is implemented in the Google protocol buffer tools.*

#### Every time `gtfs-realtime.proto` changes

Regenerate the language binding source from gtfs-realtime.proto.

```
vendor/bin/protoc-gen-php.php --include=../gtfs-realtime-bindings --out=src ../gtfs-realtime-bindings/gtfs-realtime.proto
```

(or, on Windows, `vendor/bin/protoc-gen-php.php.bat --include=../gtfs-realtime-bindings --out=src ../gtfs-realtime-bindings/gtfs-realtime.proto`)

Add the license header back to the generated source file.

s/EMPTY/EMPTY0/ in OccupancyStatus enum, since EMPTY is a reserved word in PHP.

Test the generated code:

```
vendor/bin/phpunit
````

## Publishing a new release

#### One-Time Setup

?

#### Every release

Tag the new release:

```
git tag -a 0.0.1 -m "Tag for 0.0.1 release"
git push --tags -u origin master
```
