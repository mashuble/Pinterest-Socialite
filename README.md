# Pinterest OAuth2 Provider for Laravel Socialite

## INSTALLATION

### 1. COMPOSER

// This assumes that you have composer installed globally
`composer require mashuble/pinterest-socialite`

### 2. SERVICE PROVIDER

Remove `Laravel\Socialite\SocialiteServiceProvider` from your providers[] array in config\app.php if you have added it already.

Add `SocialiteProviders\Manager\ServiceProvider` to your providers[] array in config\app.php.

For example:

``` php
'providers' => [
    // a whole bunch of providers
    // remove 'Laravel\Socialite\SocialiteServiceProvider',
    'SocialiteProviders\Manager\ServiceProvider', // add
];
```

Note: If you would like to use the Socialite Facade, you need to [install it](http://laravel.com/docs/5.0/authentication#social-authentication).


### 3. ADD THE EVENT AND LISTENERS

Add `SocialiteProviders\Manager\SocialiteWasCalled` event to your listen[] array in <app_name>/Providers/EventServiceProvider.

Add your listeners (i.e. the ones from the providers) to the `SocialiteProviders\Manager\SocialiteWasCalled[]` that you just created.

The listener that you add for this provider is `'SocialiteProviders\WeixinWeb\PinterestExtendSocialite@handle',`.

Note: You do not need to add anything for the built-in socialite providers unless you override them with your own providers.

For example:

``` php
/**
 * The event handler mappings for the application.
 *
 * @var array
 */
protected $listen = [
    `SocialiteProviders\Manager\SocialiteWasCalled` => [
        // add your listeners (aka providers) here
    ],
];
```

### 4. SERVICES ARRAY AND .ENV

Add to config/services.php.

``` php
'pinterest' => [
    'client_id' => env('PINTEREST_KEY'),
    'client_secret' => env('PINTEREST_SECRET'),
    'redirect' => env('PINTEREST_REDIRECT_URI'),
],
```

Append provider values to your .env file

```
// other values above
PINTEREST_KEY=yourkeyfortheservice
PINTEREST_SECRET=yoursecretfortheservice
PINTEREST_REDIRECT_URI=https://example.com/login
```