# SimpleCAS PHP 5 CAS Client

This is a PHP 5 client library for [JA-SIG Central Authentication Service (CAS)](http://www.ja-sig.org/products/cas/).

Compatible with servers using version 1 or 2 of the CAS protocol.

## Install with Composer
A sample composer.json for your project that might requires SimpleCAS might look like:
```
{
    "repositories": [
        {
            "type": "composer",
            "url": "https://packagist.org"
        },
        {
            "type": "vcs",
            "url": "https://github.com/cnxh/SimpleCAS.git"
        }
    ],
    "require": {
        "pear/pear_exception": "1.0.*@dev",
        "pear/http_request2": "*",
        "simple-cas/simple-cas": "dev-master"
    }
}
```

## Manual install
Manually install by downloading the latest release and extracting the files,
along with [HTTP_Request2](http://pear.php.net/package/HTTP_Request2/) from PEAR.

Quick Example:

```php
<?php

require_once 'SimpleCAS/Autoload.php';
require_once 'HTTP/Request2.php';

$options = array('hostname' => 'login.unl.edu',
                 'port'     => 443,
                 'uri'      => 'cas');
$protocol = new SimpleCAS_Protocol_Version2($options);

$client = SimpleCAS::client($protocol);
$client->forceAuthentication();

if (isset($_GET['logout'])) {
    $client->logout();
}

if ($client->isAuthenticated()) {
    echo '<h1>Authentication Successful!</h1>
          <p>The user\'s login is '.$client->getUsername().'</p>
          <a href="?logout">Logout</a>';
}
?>
```
