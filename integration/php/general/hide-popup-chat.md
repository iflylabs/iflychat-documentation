###How to hide popup chat on a PHP page

You may hide the popup chat on a PHP page as explained below:

Define a settings array with one of the index as `SHOW_POPUP_CHAT`. This index should be set to `FALSE`.

```
$settings = array(
  'SHOW_POPUP_CHAT' => FALSE,
);
```

Pass this settings array as third argument while initializing the object of iFlyChat class.

```
$iflychat = new iFlyChat(APP_ID, API_KEY, $settings);
```

So the complete code will look like this:

```
<?php
require __DIR__ . '/vendor/autoload.php'; //path to your autoload.php

use Iflylabs\iFlyChat;

$settings = array(
  'SHOW_POPUP_CHAT' => TRUE,
);

$iflychat = new iFlyChat(APP_ID, API_KEY, $settings);

?>
<html>
<head>
</head>
<body>
  <div>Chat</div>
  <?php print $iflychat->getHtmlCode(); ?>
</body>
</html>
```

That's it. Now the popup chat won't appear on the PHP page. 

*Note*: Please note that in order to render embed version of the chat you would need to add embed code separately.
