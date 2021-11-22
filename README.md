# CAS Authentication for CakePHP 3.x

Very basic CAS Authentication for CakePHP 3.

## What's new/different in this version?

New features via configuration parameters:

* **casVersion** - ability to specify CAS version (defaults to CAS_VERSION_2_0 for backwards compatibility).
* **loginEvent** - specify event to call after CasAuth.authenticate if needed

Example config file using new parameters:

```php
$this->Auth->config('authenticate', [
    'CasAuth.Cas' => [
        'casVersion' => 'CAS_VERSION_3_0',
        'loginEvent' => \CakeDC\Users\Controller\Component\UsersAuthComponent::EVENT_AFTER_LOGIN,
    ]
]);
```
***


## Installing via composer

Install into your project using [composer](http://getcomposer.org).
For existing applications you can add the
following to your composer.json file (requires:

    "require": {
        "snelg/cakephp-3-cas": "dev-develop-um"
    },
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/umaine-research/cakephp-3-cas"
        }
    ]

And run `php composer.phar update`

## Usage

Load the Cake AuthComponent, including CasAuth.Cas as an authenticator.
For example:
```php
$this->loadComponent('Auth');

$this->Auth->config('authenticate', [
    'CasAuth.Cas' => [
        'hostname' => 'cas.mydomain.com',
        'uri' => 'authpath']]);
```

Or combine the load and configuration into one step:
```php
$this->loadComponent('Auth', [
    'authenticate' => [
        'CasAuth.Cas' => [
            'hostname' => 'cas.mydomain.com',
            'uri' => 'authpath']]]);

```

CAS parameters can be specified during Auth->config as above,
or by writing to the "CAS" key in Configure::write, e.g.
```php
Configure::write('CAS.hostname', 'cas.myhost.com');
Configure::write('CAS.port', 8443);
```

## Parameters

* **hostname** is required
* **port** defaults to 443
* **uri** defaults to '' (an empty string)
* *debug* (optional) if true, then phpCAS will write debug info to logs/phpCAS.log
* *cert_path* (optional) if set, then phpCAS will use the specified CA certificate file to verify the CAS server
* *curlopts* (optional) key/value paired array of additional CURL parameters to pass through to phpCAS::setExtraCurlOption, e.g.
```php
    'curlopts' => [CURLOPT_PROXY => 'http://proxy:5543', CURLOPT_CRLF => true]
```
