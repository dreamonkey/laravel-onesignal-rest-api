#  OneSignal REST API Wrapper For Laravel/Lumen

## Introduction

This project is a Laravel 5 / Lumen wrapper for the OneSignal REST API v1.
It supports all operations currently supported by the API.

## Installation (Laravel and Lumen)

Require the package with composer.

```sh
composer require dreamonkey/laravel-onesignal-rest-api
```

## Laravel Users:
From Laravel 5.5 onwards, it's possible to take advantage of auto-discovery of the service provider.

For Laravel versions before 5.5, you must register the service provider in your config/app.php

Update `config/app.php` by adding the following entries.
```php
'providers' => [
    // ...
    Dreamonkey\OneSignal\OneSignalServiceProvider::class,
];

'aliases' => [
   	// ...
   	'OneSignal' => Dreamonkey\OneSignal\Facades\OneSignal::class,
];
```

## Lumen Users:
Update `bootstrap/app.php`, adding the following entry
```php
$app->register( \Dreamonkey\OneSignal\OneSignalServiceProvider::class );
class_alias( 'Dreamonkey\OneSignal\OneSignalFacade', 'OneSignal' );
```


## Configuration
There are three values that need to be set in order to use the library: your default OneSignal app ID, the REST API key and your account User Auth Key.
All of these items can be found in your Control Panel on the OneSignal site.
First two are app-related and can be found inside your app settings in the "Keys & IDs" tab (upper left corner), the third is account-related and can be found pressing your account avatar (lower right corner) and selecting "Account & API Keys".

Place the 3 keys into your .env file, as such:
```
ONESIGNAL_APP_ID=
ONESIGNAL_REST_API_KEY=
ONESIGNAL_USER_AUTH_KEY=
```

## Usage

There is a function for each of the OneSignal API calls.  They are broken down here.
All methods will return an array formatted like this:
```
    [
        'status' => < HTTP status code of the request >,
        'data' => [
            < data returned by OneSignal REST API in array format >
        ],
    ]
```

**Note:** In all instances where an $app_id is asked for, omitting it will grab the default OneSignal App ID specified in the .env file

### Apps

##### getApps() - Get all Apps for the user
```
$response = OneSignal::getApps();
```

##### getApp( $app_id ) - Get the given App

##### postapp( $data ) - Create a new App

##### putApp( $app_id, $data ) - Update an App

### Players

##### getPlayers( $app_id, $limit, $offset ) - Get Players from an App

##### getPlayer( $id ) - Get Player of the given ID

##### postPlayer ( $data, $app_id ) - Add Player to an App

##### putPlayer( $data, $app_id ) - Update Player object for an App

##### postCSVExport( $app_id ) - Get a CSV dump of all Players for an App

##### postPlayerOnSession( $data ) - Start a new device session for this Player

##### postPlayerOnPurchase( $data ) - Track a new purchase for this Player

##### postPlayerOnFocus( $data ) - Increment the Players total session length

### Notifications

##### getNotifications( $app_id, $limit, $offset ) - Get all Notifications for an App

##### getNotification( $id,  $app_id ) - Get a Notification from an App

##### postNotification( $data, $app_id ) - Add a Notification to an App
```
$response = OneSignal::postNotification([
    "tags"                  =>  [ ["key" => "myKey", "relation" => "=", "value" => 1 ] ],
    "contents"              => ["en" => "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aenean et iaculis enim. Sed egestas porttitor laoreet."],
    "headings"              => ["en" => "Aliquam consectetur odio sed"],
]);
```

##### putNotificationTrackOpen( $id, $app_id, $opened ) - Track whether a Notification was opened

##### deleteNotification( $id, $app_id ) - Delete a Notification from an App



## References
The official OneSignal API documentation is listed here:
https://documentation.onesignal.com/docs/server-api-overview


## Acknowledgements
This project has been forked and evolved by Dreamonkey from https://github.com/jmrieger/onesignal-laravel
