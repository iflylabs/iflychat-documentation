### How to integrate chat with any PHP based website.

**Step 1:**  Download [iFlyChat PHP Client](https://github.com/iflylabs/iflychat-php) from [https://github.com/iflylabs/iflychat-php/archive/master.zip](https://github.com/iflylabs/iflychat-php/archive/master.zip) (direct download link) and extract it. Copy iflychat-php folder to your root directory..

**Step 2:** Include the iflychat.php in your website. To do so, add the following code in your index file.
```php
require_once('./iflychat-php/iflychat.php');
```

**Step 3:** Generate API Key and APP ID from [iflychat.com](https://iflychat.com) and copy them.

**Step 4:** Now paste the API Key and APP ID in your website by adding the following code in your main php(index) file.
```php
const API_KEY = 'your-api-key';
const APP_ID =  'your-app-id';
```

**Step 5:** Now create a settings array to set/update your settings on our server. Example of a settings array is as follows:
```php
$settings = array(
  'SHOW_POP_UP_CHAT' => true // to show chat as popup
);
```
**Step 6:** Create an object of iflychat by passing the API Key, APP ID and settings array. Example
```php
$iflychat = new iFlyChat(API_KEY, APP_ID, $settings);
```

**Step 7:** In case, you want to create a user for the chat, you just need to call the setUser() function with $user array as a parameter. 
Example.
```php
$user = array(
  'user_name' => 'testUser', // string(required)
  'user_id' => '2', string (required)
  'is_admin' => FALSE, // boolean (optional)
  'user_avatar_url' => 'user-avatar-link', // string (optional)
  'user_profile_url' => 'user-profile-link', // string (optional)
);
$iflychat->setUser($user);
```

**Step 8:** Now, you need to include iFlyChat HTML code in your website. As an example, check out **index.php** (inside iflychat-php folder). To do so, add the following line of code before printing anything on the webpage:
```php
$ifly_html_code = $iflychat->getHtmlCode();
```

**Step 9:** Make sure to use the above code before printing any content via PHP, otherwise you will get an error. Next, use the following code anywhere in your PHP file (preferably before body tag ends) to render the chat:
```php
print $ifly_html_code;
```
