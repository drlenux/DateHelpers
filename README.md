
[![Latest Stable Version](https://img.shields.io/packagist/v/drlenux/date-helper.svg)](https://packagist.org/packages/drlenux/date-helper)
[![Total Downloads](https://img.shields.io/packagist/dt/drlenux/date-helper.svg)](https://packagist.org/packages/drlenux/date-helper)
[![Build Status](https://travis-ci.org/drlenux/DateHelper.svg?branch=master)](https://travis-ci.org/drlenux/DateHelper)
[![php version](https://img.shields.io/packagist/php-v/drlenux/date-helper.svg)](https://packagist.org/packages/drlenux/date-helper)
[![scrutinizer](https://scrutinizer-ci.com/g/drlenux/DateHelper/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/drlenux/DateHelper/?branch=master)
[![scrutinizer](https://scrutinizer-ci.com/g/drlenux/DateHelper/badges/code-intelligence.svg?b=master)](https://scrutinizer-ci.com/g/drlenux/DateHelper/?branch=master)
[![scrutinizer](https://scrutinizer-ci.com/g/drlenux/DateHelper/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/drlenux/DateHelper/?branch=master)


Author: `DrLenux`

License: `MIT`

Allow method `DateChange`:
```php
interface DateChange {
    function addDay(int $count = 1): self;
    function addMonth(int $count = 1): self;
    function addYear(int $count = 1): self;
    function addHour(int $count = 1): self;
    function addMinute(int $count = 1): self;
    function addSeconds(int $count = 1): self;

    function subDay(int $count = 1): self;
    function subMonth(int $count = 1): self;
    function subYear(int $count = 1): self;
    function subHour(int $count = 1): self;
    function subMinute(int $count = 1): self;
    function subSeconds(int $count = 1): self;
    
    function diff(DateChange $date): DateInterval|bool;
}
```

Example `DateChange`:
```php
<?php

use DrLenux\DataHelper\DateChange; 

$date = (new DateChange('2012-12-12'))
            ->addYear()
            ->addMonth(2)
            ->subDay();
```

Allow method `DateFill`:
```php
interface DateFill {
    function to(string $to)
    function from(string $from)
    function inclusiveStart(bool $status)
    function inclusiveEnd(bool $status)
    function interval(string $interval)
    function format(string $format)
    function timezone(\DateTimeZone $timezone = null)

    function fill()
    function getErrors()
}
```

Example `DateFill`:
```php
<?php

use DrLenux\DataHelper\DateFill;

$fillArray = (new DateFill())
    ->from('2011-01-01')
    ->to('2011-01-02')
    ->interval(DateFill::INTERVAL_HOUR)
    ->fill();

/*
return [
    '2011-01-01 01:00:00',
    ...
    '2011-01-01 23:00:00'
];
 */
```

Example `Interval`:
```php
<?php

use DrLenux\DataHelper\DateFill;

(new DateFill())
    ->from('2011-10-09 23:59:59')
    ->to('2011-10-09 23:50:00')
    ->interval('PT2M') // every 2 minute
    ->format('H:i:s')
    ->fill(); 

/*
return [
    '23:57:59',
    '23:55:59',
    '23:53:59',
    '23:51:59'
];
*/
```

Example `Diff`:
```php
<?php

use DrLenux\DataHelper\DateChange;

$date1 = new DateChange('01-01-2018');
$date2 = new DateChange('01-01-2017');

$diff = $date1->diff($date2);
echo $diff->days;

/*
return 365;
*/
```