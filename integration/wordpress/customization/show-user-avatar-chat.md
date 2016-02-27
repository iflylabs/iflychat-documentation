We provide integration of user avatar used in WordPress into the chat. By default the avatar uploaded by user in WordPress is shown in the chat. You may change this option from the chat plugin's settings page.

We offer direct integration with all popular WordPress avatar plugins. Few of them are listed below:

* Gravatar
* WP User Avatar
* BuddyPress
* UserPro
* Ultimate Member
* User Avatar
* Simple Local Avatars


Apart from this, we also provide a WordPress filter which enables you to use avatar from any third party or custom avatar plugin in our chat. The WordPress filter name is `iflychat_get_user_avatar_url_filter`.

You may use this filter in the following manner:

~~~
function my_custom_user_avatar_url_filter(){

  /** Get current user information **/
  global $current_user;
  get_currentuserinfo();

  /** Get avatar of the current user with the help of your custom function
   *   it should return the user avatar url
  **/
  $user_avatar_url = get_custom_avatar_url($current->ID);

  return $user_avatar_url;

}

add_filter('iflychat_get_user_avatar_url_filter', 'my_custom_user_avatar_url_filter’);
~~~

Add the above code to your `function.php` inside the theme template. Also, replace the function named `get_custom_avatar_url()` with the actual function name which will provide the user avatar in chat.
