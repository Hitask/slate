# User

Operations related to current user's account: authenticate, sign up, etc.

## Authenticate

```js

{
    "api_key" : myapikey;
    login : john;
    password : XXXXXXXXX;
}
```
> Will produce the response: 


```js
{
    id : 12345678;
    level : 300;
    "session_id" : "e0f93451-5ad6-4550-b991-efb0ce1e271b";
}
```

* `GET /user/authenticate` will authenticate user using user name and password

Input parameters:

* user name
* password

Response values:

* id: unique user id used to identify this user account
* level: account level
* session_id: session token

<aside class="notice">
You must provide <code>ApiKey</code> with the request.
</aside>




## Sign out

End current session

* `GET /user/logout` Close user's session.

Input parameters:
* session_id: session token


## User Account information

> Example response:

```javascript
{
    businessId : 123,
    businessLevel : 100,
	email : "name@email.com",
	emailConfirmed : "name@email.com",
	id : 123,
	isOnline : 1,
	level : 0,
	login : "john",
	firstName : "Mick",
	lastName : "Johnson",
	pictureSource: 1000,
	pictureHash: "4b0c75c8-14cc-4d9b2-80aa-b49f5cf62daf"
}
```

* `GET /user`  Get current user account information


### Response fields:

|Field|Type|Description|
|-----|----|-----------|
|id|long|Globally unique primary identifier for a user. This is an integer, but it is recommended to handle it as String to avoid limitations with the way JavaScript integers are expressed.|
|accountType|String|User's account type: *TEAM_BASIC, TEAM_BUSINESS, PERSONAL_FREE, PERSONAL_PREMIUM*|
|login|String|user login id|
|firstName|String|user's First Name|
|lastName       |String        |user's Last Name|
|emailConfirmed        |String        |Email address that was confirmed by the user. (By clicking confirmaiton link sent to this email address.)|
|email        |String        |Email address that user entered but not confirmed.|
|businessId        |Integer        |unique identifier of user's Team Business account, if applicable |
|businessLevel        |Integer        |Membership level of user in Business account: 1 - member, 2 - manager, 10 - administrator, 100 - owner|
|pictureHash        |String        |Unique avatar identifier that should be used in order to build user avatar URL|
|pictureSource|Integer| Type of user avatar: See below  |

#### Type of user avatar

* 0 Avatar is missing (only happens if generation failed)
* 1 Avatar is auto-generating (searching social sources or auto generating: only happens if user registered few seconds ago)
* 2 Auto generated (initials on background)
* 10 Google
* 11 Facebook
* 12 Gravatar
* 100 User uploaded
* 1000 Unknown
    

#### User avatar sizes

Available user avatar image pixel sizes are: 16, 20, 22, 24, 32, 40, 44, 48, 64, 80, 88, 96, 100, 128, 192, 200



## Update User Account information

* `PUT /user`  Update current user account information

Input parameters:

* firstname: First Name
* lastname: Last Name
* email: e-mail address. If email address is different from previously stored, an email message with address confirmation will be sent


## Update User Avatar

>Example response:

```js
{"hash":"4b0c75c8-14cc-49b2-80aa-b49f5cf62daf"}
```

* `POST /user/picture`  Update current user avatar

Input parameters:

* picture: Picture data
* x: (Optional) X coordinate of top left corner of square that will be used to crop the picture (x, y and width must be specified to crop the picture)
* y: (Optional) Y coordinate of top left corner of square that will be used to crop the picture (x, y and width must be specified to crop the picture)
* width: (Optional) Width of square that will be used to crop the picture (x, y and width must be specified to crop the picture)

Restrictions:

* max picture size is 1MB
* allowed image formats: "gif", "jpeg", "jpg", "png"

Error codes:

* HTTP 400 and code 32: picture upload failed, retry required
* HTTP 400 and code 34: crop parameters are invalid
* HTTP 400 and code 6: uploaded data is not a valid picture
* HTTP 400 and code 5: picture format is not valid
* HTTP 400 and code 25: picture exceeded maximum allowed size

Response:

JSON object with one property "hash": unique picture identifier.


## Delete User Avatar

* `DELETE /user/picture`  Delete current user avatar

Input parameters:

* returninfo: (optional) if "true" then full account info will be returned as described in `GET /user`


## Get User Preferences

* `GET /user/preferences`

> Example response:

```js
{
    "notify_app_item_deleted": "true",
    "notify_app_item_completed": "true",
    "ttstart": "06:00",
    "first_day_of_week": "1",
    "comment_order": "1",
    "notify_app": "true",
    "default_new_item_use_last": "true",
    "show_confirmation_complete": "true",
    "notify_app_item_tags": "true",
    "notify_web": "true",
    "default_sharing_permission_auto": "[{\"principal\":16686710,\"level\":100}]",
    "default_new_item_sharing_permission": "[{\"principal\":18556710,\"level\":100}]",
    "show_issue_sequence_id": "false",
    "notify_web_item_participant": "true",
    "desktopNotifyState": "0",
    "notify_email": "true",
    "time_zone": "Europe/Paris",
    "language": "en",
    "default_sharing_permission_last": "[{\"level\":100,\"principal\":\"18556710\"}]",
    "notify_web_item_attachment": "true",
    "main_assign_user": "186905",
    "notify_app_item_comment": "true",
    "notify_email_item_tags": "true",
    "enable_time_tracking": "false",
    "notify_app_item_participant": "true",
    "default_sharing_permission": "50",
    "notify_email_item_modify": "true",
    "notify_web_item_completed": "true",
    "notify_web_item_priority": "true",
    "default_shared_1": "false",
    "notify_web_item_comment": "true",
    "default_shared_0": "true",
    "time_format": "24",
    "notify_email_item_reminder": "true",
    "notify_email_item_priority": "true",
    "default_assign_user": "0",
    "sub_task_complete_affect_parent": "false",
    "notify_email_item_attachment": "true",
    "duplicate_with_files": "false",
    "notify_email_item_participant": "true",
    "daily_summary_email_6": "true",
    "daily_summary_email_7": "true",
    "daily_summary_email_4": "true",
    "daily_summary_email_5": "true",
    "daily_summary_email_2": "true",
    "daily_summary_email_3": "true",
    "daily_summary_email_1": "true",
    "bigCalendarMode": "month",
    "daily_summary_email_": "true",
    "override_parent_permission_with_last_used": "false",
    "notify_web_item_modify": "true",
    "notify_app_item_attachment": "true",
    "notify_email_item_comment": "true",
    "notify_web_item_tags": "true",
    "notify_email_item_completed": "true",
    "date_format": "d-m-y",
    "notify_email_item_deleted": "true",
    "taskfilter": "0",
    "notify_web_item_deleted": "true",
    "notify_app_item_priority": "true",
    "notify_app_item_assigned": "true",
    "notify_web_item_assigned": "true",
    "notify_email_item_assigned": "true",
    "default_shared": "false",
    "item.action.combobutton.last-used": "DELETE",
    "notify_app_item_modify": "true",
}
```


## Set User Preferences

* `POST /user/preferences`

Request body contain dictionary of key-value pairs

> Example request body:

```js
{
notify_app_item_deleted: "true"
}
```