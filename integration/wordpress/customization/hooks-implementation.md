## iFlyChat Hooks Implementation
To implement wordpress action hooks in your module, you just need to add the filter definition of these hooks in your main plugin file. Sample implementations are given below:

**Note:** These hooks are supported from version >= **7.x-2.5**

**1: my_custom_get_username -** Assigns a username to a given user.

```php
/**
 * Implements my_custom_get_username().
 * @params $user_name string 
 */
function my_custom_get_username($user_name){
  $user_name = 'SampleName';
  return $user_name;
}
add_filter('iflychat_get_username_filter','my_custom_get_username',10,2);
```

**2: my_custom_get_user_avatar_url() -** Assigns a avatar url to the given user.

```php
/**
 * Implements my_custom_get_user_avatar_url().
 */
function iflychat_get_user_avatar_url(){
  $user_avatar_url = 'http://sample-avatar-url';
  return $user_avatar_url;
}
add_filter('iflychat_get_user_avatar_url_filter','my_custom_get_user_avatar_url');
```
**3: my_custom_get_profile_url() -** Assigns a profile url to a given user.

```php
/**
 * Implements my_custom_get_profile_url(). 
 */
function my_custom_get_profile_url(){
  $user_profile_url = 'http://sample-profile-url';
  return $user_profile_url;
}
add_filter('my_custom_get_user_profile_url_filter','iflychat_get_profile_url');
```

**4: my_custom_get_user_roles() -** Assigns roles to a given user.

```php
/**
 * Implements iflychat_get_user_roles().
 * @params $roles associative array 
 */

function iflychat_get_user_roles($roles){
  global $current_user;
  if($current_user->ID % 2 === 0){
    $roles['sample-role-index-1'] = 'Sample-Role-Name-1'; // users with odd user id have Sample-Role-1;
  }else{
    $roles['sample-role-index-2'] = 'Sample-Role-Name-2'; // users with even user id have Sample-Role-2;
  }
  return $roles;
}
add_filter('iflychat_get_user_roles_filter','iflychat_get_user_roles');
```

**5: my_custom_groups_filter() -** Assigns a group to a given user.

```php
/**
 * Implements my_custom_groups_filter().
 * @params $uid string
 */

 function my_custom_groups_filter($uid){
  global $current_user;
  if($current_user->ID % 2 === 0){
    $user_groups['A'] = "A";
 } else {
    $user_groups['B'] = "B";
 }
    return (array)$user_groups;
 };
 add_filter('iflychat_get_user_groups_filter','my_custom_groups_filter');
```

**6: my_custom_friends_filter() -** Assigns a relationship to a given user.

```php
/**
 * Implements my_custom_friends_filter
 ().
 * @params $friends array 
 */
function iflychat_get_friends($friends){
  $friends = ['1','2','3'];    //Id's of friends
  return (array)$friends;
}
add_filter('iflychat_get_user_friends_filter', 'iflychat_get_friends');
```

**6: my_custom_filter() -** Display chat to a limited set of users.

```php
/**
 * Implements my_custom_filter
 ().
 * @params $access boolean 
 */
function my_custom_filter($access) {
  $access = true;
  /** Get current user information **/
  global $current_user;
  get_currentuserinfo();
  /** Return $access as true or false based on your custom code */ 
  return $access;
}
add_filter('iflychat_check_access_filter', 'my_custom_filter');
```
**Important:** If you like to access user_id inside filter function. You need to change the definition of add_filter little bit. you need to add two extra arguments.
For example : 
```php
 add_filter('iflychat_get_user_groups_filter','my_custom_groups_filter',10,2);
 function my_custom_groups_filter(,$user_groups,$uid){
   if($uid % 2 === 0){
     $user_groups['A'] = "A";
  } else {
     $user_groups['B'] = "B";
  }
     return (array)$user_groups;
  };
```
For reference - https://developer.wordpress.org/reference/functions/add_filter/
