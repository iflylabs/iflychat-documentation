## iFlyChat Hooks Implementation
To implement wordpress action hooks in your module, you just need to add the filter definition of these hooks in your main plugin file. Sample implementations are given below:

**Note:** These hooks are supported from version >= **7.x-2.5**

**1: iflychat_get_username -** Assigns a username to a given user with user id = $id.  

```php
/**
 * Implements iflychat_get_username().
 * @params $user_name string 
 * @params $id string
 */
function iflychat_get_username($user_name,$id){
  $user_name = 'SampleName';
  return $user_name;
}
add_filter('iflychat_get_username_filter','iflychat_get_username',10,2);
```

**2: iflychat_get_user_avatar_url() -** Assigns a avatar url to the given user with user id = $id.

```php
/**
 * Implements iflychat_get_user_avatar_url().
 * @params $user_avatar_url string 
 * @params $id string
 */
function iflychat_get_user_avatar_url($user_avatar_url,$id){
  $user_avatar_url = 'http://sample-avatar-url';
  return $user_avatar_url;
}
add_filter('iflychat_get_user_avatar_url_filter','iflychat_get_user_avatar_url',10,2);
```
**3: iflychat_get_profile_url() -** Assigns a profile url to a given user with user id = $id.

```php
/**
 * Implements iflychat_get_profile_url(). 
 * @params $user_profile_url string 
 * @params $id string
 */
function iflychat_get_profile_url($user_profile_url,$id){
  $user_profile_url = 'http://sample-profile-url';
  return $user_profile_url;
}
add_filter('iflychat_get_user_profile_url_filter','iflychat_get_profile_url',10,2);
```

**4: iflychat_get_user_roles() -** Assigns roles to a given user with user id = $id.

```php
/**
 * Implements iflychat_get_user_roles().
 * @params $roles associative array 
 * @params $id string
 */

function iflychat_get_user_roles($roles,$uid){
  if($uid % 2 === 0){
    $roles['sample-role-index-1'] = 'Sample-Role-Name-1'; // users with odd user id have Sample-Role-1;
  }else{
    $roles['sample-role-index-2'] = 'Sample-Role-Name-2'; // users with even user id have Sample-Role-2;
  }
  return $roles;
}
add_filter('iflychat_get_user_roles_filter','iflychat_get_user_roles',10,2);
```

**5: iflychat_get_user_groups() -** Assigns a group to a given user with user id = $id.

```php
/**
 * Implements iflychat_get_user_groups().
 * @params $user_groups associative array 
 * @params $id string
 */

 function iflychat_get_user_groups($user_groups,$uid){
 if ($uid % 2 == 0 ) {
    $user_groups['A'] = "A";
 } else {
    $user_groups['B'] = "B";
 }
    return (array)$user_groups;
 };
 add_filter('iflychat_get_user_groups_filter','iflychat_get_user_groups',10,2);
```

**6: iflychat_get_friends() -** Assigns a relationship to a given user with user id = $id.

```php
/**
 * Implements iflychat_get_friends().
 * @params $friends associative array 
 * @params $id string
 */
function iflychat_get_friends($friends,$id){
  $friends = ['1','2','3'];    //Id's of friends
  return (array)$friends;
}
add_filter('iflychat_get_user_friends_filter', 'iflychat_get_friends',10,2);
```