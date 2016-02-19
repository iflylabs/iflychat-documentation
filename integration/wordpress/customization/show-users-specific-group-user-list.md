It is possible to filter the user list on the basis of groups. We provide a WordPress filter named **iflychat_get_user_groups_filter** for this purpose.

If you use this filter then the user won't see site-wide user list in the chat app. Instead they would see the users online only from the group to which they belong. Example - If a user belongs to group A then he would see only the online users in group A. He won't be able to see users who belong to other groups (group B, group C, group D, etc).

You may use the following sample code to use this filter. Add this code to your **function.php** inside the theme template:
~~~
function my_custom_groups_filter($uid){

  /** Get current user information **/
  global $current_user;
  get_currentuserinfo();

  /** Get groups of the current user with the help of custom function
  *   it will be array containing groups like groups  array(‘1’, ‘2’)
  **/
	$groups = array('1', '2');

  return $groups;

}

add_filter('iflychat_get_user_groups_filter', 'my_custom_groups_filter’);
~~~

Please note that this event may fire more than once if the chat is disconnected and then re-connected.
