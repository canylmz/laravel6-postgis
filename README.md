# Laravel 6 PostGIS
This package implemented for calculate or check the distance between point and other database points.

## Installation

[PHP](https://php.net) >=7.2 and [Laravel](http://laravel.com) 6.0 are required.

the package used [Laravel postgis extension](https://github.com/njbarrett/laravel-postgis) to deal with postgres database points in laravel,
so if need more details or how to enable postgis extension in php see previous link.

To get the latest version of Laravel 6 PostGIS, simply require the project using [Composer](https://getcomposer.org):

```bash
composer require canylmz/laravel-postgis
```

## Usage

1 . First of all use `Postgis` trait in your model
```PHP
<?php

namespace App;

use Canylmz\Postgis\Postgis;
use Illuminate\Database\Eloquent\Model;

class UserLocation extends Model
{
    use Postgis;
}
```

2 . By default package assume that the name of the point column is `location` if you want to change it override `location` variable on your model
```PHP
protected $location = "my_column";
```

3 . Also By default package assume that the unit of distance is `meter` if you want to change it override `unit` variable on your model
```PHP
 protected $unit = "km"; //units avialble [mile, km, meter]
```

### Functions

#### 1. withDistance
get the distance between point and other points
```PHP
UserLocation::withDistance(new Point($atitude,$longitude))
            ->with("user")
            ->whereIn("user_id", $users)
            ->get();
```

#### 2. whereDistance
check the distance between a point and other points in database
```PHP
       UserLocation::whereDistance(new Point($atitude,$longitude), ">", 50)
            ->with("user")
            ->whereIn("user_id", $users)
            ->get();
```
