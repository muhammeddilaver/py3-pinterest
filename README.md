# py3-pinterest
Unofficial Pinterest API implemented in python 3 that can do almost all pinterest tasks like comment, pin, repin, follow, unfollow and more.
It is implemented by directly calling the pinterest servers, mimicking an actual browser, so you don't need pinterest API key.

If you see any issues, or find bugs feel free to report them here on the github repo.


## Install using pip
```pip install py3-pinterest```


### NOTE: for each of the functionalities listed below there is a working example under the project root.

### Create new instance of the API

```pinterest = Pinterest(email='your email goes here', password='password goes here', username='look in pinterest url', cred_root='cred root dir')```

cred_root is the dir (automatically created if missing) that will store some cookies nad sessions, so you don't need to login before each request.
Make sure you specify a path with read/write persmissions.


# The following features are currently supported

## Login
Login is required to permit actions to the Pinterest servers. Login will store auth cookies for later use. These cookies are usually valid for ~15 days, then you will start getting 403 and 401 errors, which means you need to call login again. 

```pinterest.login()```



## Load profile
You can load profile for currently logged in user or any user specified by username.

```user_profile = pinterest.get_user_overview()```


## Board and pin management

### Get all boards of user:

```boards = pinterest.boards(username='username')```

### List all pins in board
```pins = pinterest.board_feed(board_id=board_id)```

If username is left blank, current logged in user will be used.


### Delete pin
```pinterest.delete_pin(pin_id='pin_id')```

### Repin

```pinterest.repin(board_id='board_id', pin_id='pin_id')```

### Get pinnable images
A pinterest feature they use to pin from websites

```pinterest.get_pinnable_images(url='https://www.tumblr.com/search/food')```

### Pin

```pinterest.pin(board_id=board_id, image_url=image_url, description=description, title=title)```

### Get home feed pins

``` home_feed_batch = pinterest.home_feed()```

### Get board recommendations (this is the 'more ideas' api)

```rec_batch = pinterest.board_recommendations(board_id=board_id)```

### Get pin by id

```pinterest.load_pin(pin_id='pin_id')```

### Section support
```pinterest.create_board_section(board_id=board_id, section_name=section_name)```
```pinterest.delete_board_section(section_id=section_id)```
```pinterest.get_board_sections(board_id=board_id)```

You can also pin and repin to sections.


## Follow/Unfollow

### Follow
```pinterest.follow_user(user_id='target_user_id', username='target_username')```

Follow limit is 300 per day, after that they might place you on watch list


### Unfollow

```pinterest.unfollow_user(user_id='target_user_id', username='target_username')```

Unfollow limit is 350 per day, after that they might place you on watch list

### Get following

```following_batch = pinterest.get_following(username='some_user')```

If username is not provided current user will be used

### Get followers

```followers_batch=pinterest.get_user_followers(username='some_user')```

If username is not provided current user will be used

### Follow board

```pinterest.follow_board(board_id=board_id)```

### Unfollow board

```pinterest.unfollow_board(board_id=board_id)```


## Search

```search_batch = pinterest.search(scope='boards', query='food')```

Current pinterest scopes are: pins, buyable_pins, my_pins, videos, users, boards


## User interactions
### Invite to board

```pinterest.invite(board_id=board_id, user_id=target_user_id)```

### Delete board invite

```pinterest.delete_invite(board_id=board_id, invited_user_id=target_user_id)```

### Get board invites

```invites_batch = pinterest.get_board_invites(board_id=board_id)```

### Comment

```pinterest.comment(pin_id=pin_id, text=comment_text)```

### Delete comment 
```pinterest.delete_comment(pin_id=pin_id, comment_id=comment_id)```

### Get Pin comments

```pinterest.get_comments(pin_id='pin_id')```


### Send perosnal message
```pinterest.send_message(conversation_id=conversation_id, pin_id="(pin_id)", message="hey")```




