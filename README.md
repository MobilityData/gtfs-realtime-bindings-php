# PHP GTFS-realtime Language Bindings

[![PHP version](https://badge.fury.io/ph/google%2Fgtfs-realtime-bindings.svg)](http://badge.fury.io/ph/google%2Fgtfs-realtime-bindings)

Provides PHP classes generated from the
[GTFS-realtime](https://developers.google.com/transit/gtfs-realtime/) Protocol
Buffer specification.  These classes will allow you to parse a binary Protocol
Buffer GTFS-realtime data feed into PHP objects.

For bindings in other languages, see the
[gtfs-realtime-bindings](https://github.com/google/gtfs-realtime-bindings)
project.

## Add the Dependency

To use the `gtfs-realtime-bindings-php` classes in your own project, you need
to first install the [Packagist Composer
package](https://packagist.org/packages/google/gtfs-realtime-bindings).  To do
so, add a dependency in your `composer.json` file:

```
"require": {
  "google/gtfs-realtime-bindings": "x.y.z"
}
```

Where `x.y.z` is the latest release version:

[![PHP version](https://badge.fury.io/ph/google%2Fgtfs-realtime-bindings.svg)](http://badge.fury.io/ph/google%2Fgtfs-realtime-bindings)

Then update your Composer dependencies:

```
composer update
```

## Example Code

The following code snippet demonstrates downloading a GTFS-realtime data feed
from a particular URL, parsing it as a FeedMessage (the root type of the
GTFS-realtime schema), and iterating over the results.

```php
require_once 'vendor/autoload.php';

use transit_realtime\FeedMessage;

$data = file_get_contents("URL OF YOUR GTFS-REALTIME SOURCE GOES HERE");
$feed = new FeedMessage();
$feed->parse($data);
foreach ($feed->getEntityList() as $entity) {
  if ($entity->hasTripUpdate()) {
    error_log("trip: " . $entity->getId());
  }
}
```

For more details on the naming conventions for the PHP classes generated from
the [gtfs-realtime.proto](https://developers.google.com/transit/gtfs-realtime/gtfs-realtime-proto),
check out the [the gtfs-realtime.php source file](https://github.com/google/gtfs-realtime-bindings-php/blob/master/src/gtfs-realtime.php).
