### Creating a iFlyChat User

**Step 1:** Declare an associative array
```php
$user = array(
  'user_name' => 'testUser', // string(required)
  'user_id' => '2', string (required)
  'is_admin' => TRUE, // boolean (optional)
  'user_avatar_url' => 'user-avatar-link', // string (optional)
  'user_profile_url' => 'user-profile-link', // string (optional)
  'user_roles' => 'user-role', //string if admin else associative array (optional)
  'user_groups' => 'groups-user-belongs-to', // associative array (optional)
  'user_relationships' => 'friends-of-user' // associative array (optional)
);

// sample $user array
$user = array(
  'user_name' => 'testUser',
  'user_id' => '2', 
  'is_admin' => TRUE, 
  'user_avatar_url' => '//www.gravatar.com/avatar/caef045b3bbc44130320edef1ec710fe?s=50&#038;r=g&#038;d=mm', 
  'user_profile_url' => 'http://facebook.com/sample-user-profile', 
  'user_roles' => 'admin', 
  'user_groups' => array(
  	'A' => 'A'
  ), 
  'user_relationships' => array(
  	'1' => array(
  		'name' => 'friend',
  		'plural' => 'friends',
  		'valid_uids' => array('1', '3')
  	)
  )
);
```

**Step 2:** Pass this user array to the setUser() function.
```php
$iflychat->setUser($user);
```

#### Setting individual properties of a user.

##### **is_admin**
```php
$iflychat = new iFlyChat(API_KEY, APP_ID, $settings);
$is_admin = TRUE;
$iflychat->setIsAdmin($is_admin);
```

#### **user_avatar_url**
```php
$avatar_url = '//www.gravatar.com/avatar/caef045b3bbc44130320edef1ec710fe?s=50&#038;r=g&#038;d=mm'
$iflychat->setAvatarUrl($avatar_url);
```

#### **user_profile_url**
```php
$profile_url = 'http://facebook.com/sample-user-profile'
$iflychat->setProfileLink($avatar_url);
```

#### **relationships_set**
```php
$iflychat->setRelationshipSet(TRUE); // to allow relationships.
$iflychat->setRelationshipSet(FALSE); // to restrict realtionships.

default value is FALSE.
```

#### **user_roles**
```php
// for admin
$iflychat->setRoomRoles('admin');

// for other users
$user_roles = array(
	'subscriber' => 'subscriber'
);
$iflychat->setRoomRoles($user_roles);
```

#### **user_groups**
```php
$user_groups = array(
	'group1' => 'Sample Group'
);
$iflychat->setUserGroups($user_groups);
```

#### **user_relationships**
```php
$list = array();
$list['1']['name'] = 'friend';
$list['1']['plural'] = 'friends';
$list['1']['valid_uids'] = array('3', '4', '5');
$iflychat->setUserRelationships($list);
```

#### **all_roles**
```php
$user_site_roles = array(
	'subscriber' => 'subscriber',
    'editor' => 'editor',
    'author' => 'author'
);
$iflychat->setAllRoles($user_site_roles);
```

