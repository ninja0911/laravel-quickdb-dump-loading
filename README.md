**WORK IN PROGRESS, DO NOT USE**

# An artisan command to create and load snapshots of your database

[![Latest Version on Packagist](https://img.shields.io/packagist/v/spatie/laravel-db-snapshots.svg?style=flat-square)](https://packagist.org/packages/spatie/laravel-db-snapshots)
[![Build Status](https://img.shields.io/travis/spatie/laravel-db-snapshots/master.svg?style=flat-square)](https://travis-ci.org/spatie/laravel-db-snapshots)
[![Quality Score](https://img.shields.io/scrutinizer/g/spatie/laravel-db-snapshots.svg?style=flat-square)](https://scrutinizer-ci.com/g/spatie/laravel-db-snapshots)
[![Total Downloads](https://img.shields.io/packagist/dt/spatie/laravel-db-snapshots.svg?style=flat-square)](https://packagist.org/packages/spatie/laravel-db-snapshots)

This package provides artisan commands to quickly dump the database and load up a previously created dump.

```bash
# create a dump
php artisan snapshot:create my-first-dump

# make some changes to you db
# ...

# create another dump
php artisan snapshot:create my-second-dump

# load up the first dump
php artisan snapshot:load my-second-dump

# list all snapshots
php artisan snapshot:list
```

This package supports MySQL, PostgreSQL and SQLite.

## Postcardware

You're free to use this package (it's [MIT-licensed](LICENSE.md)), but if it makes it to your production environment we highly appreciate you sending us a postcard from your hometown, mentioning which of our package(s) you are using.

Our address is: Spatie, Samberstraat 69D, 2060 Antwerp, Belgium.

We publish all received postcards [on our company website](https://spatie.be/en/opensource/postcards).

## Installation

You can install the package via composer:

``` bash
composer require spatie/laravel-db-snapshots
```

Next, you must install the service provider:

```php
// config/app.php
'providers' => [
    ...
    Spatie\MediaLibrary\DbSnapshotsServiceProvider::class,
];
```

And finally you should add a disk named `snapshots` to `app/config/filesystems.php` on which the snapshots will be saved. This would be a typical configuration:

```php
    ...
	'disks' => [
	    ...
	    
        'snapshots' => [
            'driver' => 'local',
            'root' => database_path('snapshots'),
        ],
    ...    
```

Optionally you may publish the configuration file with:

```bash
php artisan vendor:publish --provider="Spatie\DbSnapshots\DbSnapshotsServiceProvider" --tag="config"
```

This is the content of the published file:

```php
return [

    /*
     * The name of the disk on which the snapshots are stored.
     */
    'disk' => 'snapshots',

    /**
     * The connection to be used to create snapshots. Set this to null
     * to use the default configured in `config/databases.php`
     */
    'default_connection' => null,

    /*
     * The directory where temporary files will be stored.
     */
    'temporary_directory_path' => storage_path('app/laravel-db-snapshots/temp'),
];
```

## Usage

To create a snapshot (which is just a dump from the database) run:

```bash
php artisan snapshot:create my-first-dump
```

Giving your snapshot a name is optional. If you don't pas a name the current date time will be used

```bash
# creates a snapshot named something like `2017-03-17 14:31`
php artisan snapshot:create
```

After you've made some changes to the database you can create another snapshot:

```bash
php artisan snapshot:create my-second-dump
```

To load a previous dump issue this command:

```bash
php artisan snapshot:load my-first-dump
```

To list all the dumps run:

```bash
php artisan snapshot:list
```

A dump can be deleted with:

```bash
php artisan snapshot:delete my-first-dump
```



## Events

There are several events fired which can be used to perform some logic of your own

### `Spatie\DbSnapshots\Events\CreatingSnapshot`

Will be fired before a snapshot is created

### `Spatie\DbSnapshots\Events\CreatedSnapshot`

Will be fired after a snapshot has been created

### `Spatie\DbSnapshots\Events\LoadingSnapshot`

Will be fired before a snapshot is loaded

### `Spatie\DbSnapshots\Events\LoadedSnapshot`

Will be fired after a snapshot has been loaded

### `Spatie\DbSnapshots\Events\DeletingSnapshot`

Will be fired before a snapshot is deleted

### `Spatie\DbSnapshots\Events\DeletedSnapshot`

Will be fired after a snapshot has been deleted

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

``` bash
$ composer test
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Security

If you discover any security related issues, please email freek@spatie.be instead of using the issue tracker.

## Credits

- [Freek Van der Herten](https://github.com/freekmurze)
- [All Contributors](../../contributors)

## About Spatie

Spatie is a webdesign agency based in Antwerp, Belgium. You'll find an overview of all our open source projects [on our website](https://spatie.be/opensource).

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
