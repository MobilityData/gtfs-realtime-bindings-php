# How-To Update Bindings When gtfs-realtime.proto Changes

First, make sure you have all [Composer](https://getcomposer.org/) dependencies
installed:

```
composer update
```

Regenerate the language binding source from gtfs-realtime.proto.

```
vendor/bin/protoc-gen-php.php --include=../gtfs-realtime-bindings --out=src ../gtfs-realtime-bindings/gtfs-realtime.proto
```

Add the license header back to the generated source file.

s/EMPTY/EMPTY0/ in OccupancyStatus enum, since EMPTY is a reserved word in PHP.

Test the generated code:

```
vendor/bin/phpunit
````
