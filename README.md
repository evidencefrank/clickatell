# Clickatell notifications channel for Laravel

This package makes it easy to send notifications using [clickatell.com](https://www.clickatell.com/) with Laravel 5.5+, 6.x, 7.x & 8.x.

## Contents

- [Installation](#installation)
    - [Setting up the Clickatell service](#setting-up-the-clickatell-service)
- [Usage](#usage)
    - [Available Message methods](#available-message-methods)
- [Changelog](#changelog)
- [Testing](#testing)
- [Security](#security)
- [Contributing](#contributing)
- [Credits](#credits)
- [License](#license)


## Installation

You can install the package via composer:

```bash
composer require evidencefrank/clickatell
```

### Setting up the clickatell service

Add your Clickatell user, password and api identifier  to your `config/services.php`:

```php
// config/services.php
...
'clickatell' => [
    'user'  => env('CLICKATELL_USER'),
    'pass' => env('CLICKATELL_PASS'),
    'api_id' => env('CLICKATELL_API_ID'),
],
...
```

## Usage

To route Clickatell notifications to the proper phone number, define a ```routeNotificationForClickatell```  method on your notifiable entity:
```php
class User extends Authenticatable
{
    use Notifiable;

    /**
     * Route notifications for the Nexmo channel.
     *
     * @param  \Illuminate\Notifications\Notification  $notification
     * @return string
     */
    public function routeNotificationForClickatell($notification)
    {
        return $this->phone_number; 
    }
}
```

You can use the channel in your `via()` method inside the notification:

```php
use Illuminate\Notifications\Notification;
use NotificationChannels\Clickatell\ClickatellMessage;
use NotificationChannels\Clickatell\ClickatellChannel;

class AccountApproved extends Notification
{
    public function via($notifiable)
    {
        return [ClickatellChannel::class];
    }

    public function toClickatell($notifiable)
    {
        return (new ClickatellMessage())
            ->content("Your {$notifiable->service} account was approved!");
    }
}
```

### Available methods

TODO

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

``` bash
$ composer test
```

## Security

If you discover any security related issues, please email evidencefrank.mandizvidza@gmail.com instead of using the issue tracker.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

## Credits

- [etiennemarais](https://github.com/etiennemarais)
- [etiennemarais](https://github.com/laravel-notification-channels/clickatell) (forked from this repository)
- [arcturial](https://github.com/arcturial)
    - For the [Clickatell Client implementation](https://github.com/arcturial/clickatell) which I leverage on for this wrapper

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
