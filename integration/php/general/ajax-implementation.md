### AJAX based iFlyChat Integration

If you plan to use single sign-on integration, then user information is passed to iFlyChat endpoint and a chat access token is provided for the user as response which is later on used in frontend by our app to connect to our chat service. Our PHP client does this automatically when you call `getHtmlCode()` function after `setUser()` function.

The call to iFlyChat endpoint might increase the page load time since the page doesn't get rendered before getting a response. If performance is a major concern for you or you have a high traffic website then we would recommend integrating iFlyChat in a slightly different manner using AJAX as described below:

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

**Step 3:** Use these credentials in your main php (index) file to create a new ```iFlyChat``` instance.

```php

use Iflylabs\iFlyChat;

const APP_ID = 'YOUR_APP_ID';
const API_KEY = 'YOUR_API_KEY';

$settings = array(
  'AUTH_URL' => 'https://yourwebsite.com/chat-token.php' // This AJAX endpoint is created separately below
);

$iflychat = new iFlyChat(APP_ID, API_KEY, $settings);
```

**Step 4:** Now, you need to include iFlyChat HTML code in your website. To do so, add the following line of code before printing anything on the webpage:

```php
$iflychat_code = $iflychat->getHtmlCode();
```

**Step 5:** Make sure to use the above code before printing any content via PHP, otherwise you will get an error. Next, use the following code anywhere in your PHP file (preferably before body tag ends) to render the chat:
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



**Step 6:** Create a new API POST endpoint of on your server say https://yourwebsite.com/chat-token.php. Add the following code to `chat-token.php`:

```
<?php

use Iflylabs\iFlyChat;

const APP_ID = 'YOUR_APP_ID';
const API_KEY = 'YOUR_API_KEY';

$settings = array(
  'AUTH_URL' => 'https://yourwebsite.com/chat-token.php'
);

$iflychat = new iFlyChat(APP_ID, API_KEY, $settings);

// Sample User array. Change values below and get correct values from your $_SESSION variables.

$user = array(
  'user_name' => 'shashwat', // string(required)
  'user_id' => '1', // string (required)
  'is_admin' => TRUE, // boolean (optional)
  'user_avatar_url' => 'user-avatar-link', // string (optional)
  'user_profile_url' => 'user-profile-link', // string (optional)
);

$iflychat->setUser($user);

$access_key = $iflychat->getToken();

$data = array(
  'key' => $access_key
);

header('Content-type:application/json;charset=utf-8');
echo json_encode($data);

```


Now our PHP client won't make request to iFlyChat endpoint for token when your website page loads instead our app in frontend will send an AJAX request to your newly created endpoint and then get access token. Since this will be an AJAX request, the page load time of your website won't be affected.
