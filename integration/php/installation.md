## How to integrate iFlyChat with any PHP based website.

**Step 1:**  You can get the iFlyChat PHP library via a composer package called iflychat-php. See [https://packagist.org/packages/iflylabs/iflychat-php](https://packagist.org/packages/iflylabs/iflychat-php).

```
$ composer require iflylabs/iflychat-php
```
Or add to `composer.json`:
```
"require": {
    iflylabs/iflychat-php": "^2.0"
}
```
and then run `composer update`.

Or you can clone or download the library files.

**We recommend you** to [use composer](https://getcomposer.org/).


**Step 2:** Generate **APP ID** and **API Key** from [iflychat.com](https://iflychat.com) and copy them.

**Step 3:** Use these credentials in your main php(index) file to create a new ```iFlyChat``` instance.
```php

use Iflylabs\iFlyChat;

const APP_ID = 'YOUR_APP_ID';
const API_KEY = 'YOUR_API_KEY';

$iflychat = new iFlyChat(APP_ID, API_KEY);
```

**Step 4(optional):** In case, you want to create a user for the chat, you just need to call the setUser() function with $user array as a parameter.

Example.
```php
$user = array(
  'user_name' => 'testUser', // string(required)
  'user_id' => '2', // string (required)
  'is_admin' => FALSE, // boolean (optional)
  'user_avatar_url' => 'user-avatar-link', // string (optional)
  'user_profile_url' => 'user-profile-link', // string (optional)
);

$iflychat->setUser($user);
```

**Step 5:** Now, you need to include iFlyChat HTML code in your website. As an example, check out **basic-example.php** (inside iflychat-php/examples folder). To do so, add the following line of code before printing anything on the webpage:
```php
$iflychat_code = $iflychat->getHtmlCode();
```

**Step 6:** Make sure to use the above code before printing any content via PHP, otherwise you will get an error. Next, use the following code anywhere in your PHP file (preferably before body tag ends) to render the chat:
```php
<html>
<head>
</head>
<body>
<h1>How to include iFlyChat in your PHP website?</h1>

<!-- iFlyChat Engine Code Begins -->
<?php print $iflychat_code; ?>
<!-- iFlyChat Engine Code Ends -->

</body>
</html>
```
