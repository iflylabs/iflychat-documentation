## iFlyChat Filters Implementation
To implement Wordpress filter in your module, you just need to add the filter definition of these filter in your main plugin file. Sample implementations are given below:

**Note:** These filters are supported from version >= **4.2.5**

**1: iflychat_get_username_filter -** Assigns a username to a given user.

```php
/**
 * Implements my_custom_get_username()
 * @params $user_name string 
 * @params $uid string 
 */
function my_custom_get_username($user_name,$uid){
  $user_name = 'SampleName';
  return $user_name;
}
add_filter('iflychat_get_username_filter','my_custom_get_username',10,2);
```

**2: iflychat_get_user_avatar_url_filter() -** Assigns a avatar url to the given user.

```php
/**
 * Implements my_custom_get_user_avatar_url()
 * @params $user_avatar_url string 
 * @params $uid string 
 */
function iflychat_get_user_avatar_url($user_avatar_url,$uid){
  $user_avatar_url = 'http://sample-avatar-url';
  return $user_avatar_url;
}
add_filter('iflychat_get_user_avatar_url_filter','my_custom_get_user_avatar_url',10,2);
```
**3: iflychat_get_user_profile_url_filter() -** Assigns a profile url to a given user.

```php
/**
 * Implements my_custom_get_profile_url(). 
 * @params $user_profile_url string 
 * @params $uid string 
 */
function my_custom_get_profile_url($user_profile_url,$uid){
  $user_profile_url = 'http://sample-profile-url';
  return $user_profile_url;
}
add_filter('iflychat_get_user_profile_url_filter','my_custom_get_profile_url',10,2);
```

**4: iflychat_get_user_roles_filter() -** Assigns roles to a given user.

```php
/**
 * Implements my_custom_get_user_roles().
 * @params $roles associative array 
 * @params $uid string 
 */

function my_custom_get_user_roles($roles,$uid){
  if($uid === 0){
    $roles['sample-role-index-1'] = 'Sample-Role-Name-1'; // users with odd user id have Sample-Role-1;
  }else{
    $roles['sample-role-index-2'] = 'Sample-Role-Name-2'; // users with even user id have Sample-Role-2;
  }
  return $roles;
}
add_filter('iflychat_get_user_roles_filter','my_custom_get_user_roles',10,2);
```

**5: iflychat_get_user_groups_filter() -** Assigns a group to a given user.

```php
/**
 * Implements my_custom_groups().
 * @params $user_groups array 
 * @params $uid string 
 */

 function my_custom_groups($user_groups,$uid){
  global $current_user;
  if($current_user->ID % 2 === 0){
    $user_groups['A'] = "A";
 } else {
    $user_groups['B'] = "B";
 }
    return (array)$user_groups;
 };
 add_filter('iflychat_get_user_groups_filter','my_custom_groups',10,2);
```

**6: iflychat_get_user_friends_filter() -** Assigns a relationship to a given user.

```php
/**
 * Implements my_custom_friends().
 * @params $friends array 
 * @params $uid string 
 */
function my_custom_get_friends($friends,$uid){
  $friends = ['1','2','3'];    //Id's of friends
  return (array)$friends;
}
add_filter('iflychat_get_user_friends_filter', 'my_custom_get_friends');
```

**6: iflychat_check_access_filter() -** Display chat to a limited set of users.
```php
/**
 * Implements my_custom_filter().
 * @params $access boolean
 * @params $uid string 
 */
function my_custom_filter($access,$uid) {
  $access = true;
  /** Get current user information **/
  global $current_user;
  get_currentuserinfo();
  /** Return $access as true or false based on your custom code */ 
  return $access;
}
add_filter('iflychat_check_access_filter', 'my_custom_filter',10,2);
```

For reference - https://developer.wordpress.org/reference/functions/add_filter/
