

# Item

Operations with items: tasks, events, projects, notes, files.



|Field        |Type         |Example         |Description|
|-------------|-------------|----------------|-----------|
|`id `      |long        |123000        |Globally unique item Identifier    |
|`guid`        |String (UDID)        |123456abcdef        |Globally unique item Identifier used for public sharing    |
|`user_id`        |long        |123000        |user id of owner, user who created this item    |
|`title`        |String (256)        |My Task        |title    |
|`short_name`        |String (8)        |APIDOCS        |Short name of project. Accepted by projects only. Restrictions: 8 characters length maximum, latin letters and digits.    |
|`issue_id`        |String        |APIDOCS-17        |Unique reference identifier for tasks and projects.    |
|`completed`        |int        |0        |Indication if this item is completed    |
|`color`        |int        |0        |Color tag (index of predefined colors) used for items (tasks, events, notes, ..). Onde of these colors: [no color, '#FB7E6E', '#F8B957', '#F3DF5B', '#C2D95B', '#6CB4FF', '#CAA4DF', '#B8B8B8']    |
|`color_value`        |Strng        |#5e93c3        |Color value used for projects. Default: #5e93c3<br/>One of these colors: ['#5e93c3', '#fc2f6a', '#fd9426', '#fecb2e', '#55ce2e', '#cb77df', '#a18460']    |
|`category`        |int        |1        |Category (type) of item: `0`:project `1`:task `2`:event `4`:note `5`:file `6`:client `7`:contact   |
|`message`        |String (10000)        |Hello        |Item description text    |
|`parent`        |long        |0        |Unique id of parent item. Default: 0. 0 means item is not child of another item and not inside of project    |
|`recurring`        |int        |0        |0: not recurring, 1: daily, 2: weekly, 3: monthly, 4: yearly    |
|`assigneeId`        |long        |0        |Assignee, primary responsible person. User id of user whom item is assigned to    |
|`participants`        |comma separated list of user identifiers        |322,413        |array of user id for this item participants    |
|`start_date`        |Date        |2012-03-15T19:00:00.000+10:00        |Start date and time for this item. Default:null.    | |`end_date`        |Date        |2012-03-15T19:00:00.000+10:00        |End date and time for this item. Default:null.    |
|`is_all_day`        |int        |0        |Indicator that this item is "all day" event. Only date without time should be used from start/end date field..    |
|`alerts`        |JSON array of JSON objects        |  See "Alerts" below    | |
|time_last_update        |Date        |2012-03-15T19:00:00.000+10:00        |Timestamp when this item was last changed (updated).    |
|time_create        |Date        |2012-03-15T19:00:00.000+10:00        |Timestamp when this item was created.    |
|starred        |int        |0        |If item is marked as starred, 1 or 0    |
|time_track        |int        |0        |1/0 flag to specify if time tracking is enabled for htis item. Default:0.    |
|time_est        |float        |0        |Time estimated for this item, in hours. Used in time tracking calculations.Optional.    |
|time_spent        |float        |0        |Total time spent recorded for this item.    |
|priority        |int        |20000        |Arbitrary priority. 10000-19999:low, 20000-29999:normal, 30000:high. Default: 20000 (normal)    |
|tags        |comma separated list of tags        |"work","home"        |array or tags added to item    |
|instances        |array[item_instance]        |[]        |array of instances for recurring item. at PUT/POST requests this field is ignored by the server.    |
|location        |object        |```{"longitude":123.1234567,"latitude":-4.0987654321,"address":"qwe"}```      |Map that contains long/lat coordinates and address    |
| unread | number or null | 0 | Item is "unread" for this user. It was created or modified by someone else |
| permissions | JSON array | See "Permissions" below |
| contact | String|[ \"vcard\", [ [ \"version\", { }, \"text\", \"4.0\" ], [ \"prodid\", { }, \"text\", \"-\\\/\\\/Sabre\\\/\\\/Sabre VObject 3.1.3\\\/\\\/EN\" ], [ \"n\", { }, \"text\", [ \"Pot\", \"Evert\", \"\", \"\", \"\" ] ],  [\"org\", { \"type\": \"work\" }, \"text\", \"Viagenie\"], [ \"email\", { \"type\": [ \"INTERNET\", \"HOME\" ] }, \"text\", \"evert@rooftopsolutions.nl\" ], [ \"email\", { \"type\": [ \"INTERNET\", \"WORK\" ] }, \"text\", \"evert@fruux.com\" ], [ \"tel\", { \"type\": [ \"CELL\", \"VOICE\" ] }, \"text\", \"+1 647 471 2661\" ], [ \"adr\", { \"type\": \"HOME\" }, \"text\", [ \"\", \"\", \"24 Settles Street\", \"London\", \"\", \"E1 1JP\", \"United Kingdom\" ] ], [ \"note\", { }, \"text\", \"Foo\" ], [ \"url\", { \"pref\": \"1\", \"group\": \"ITEM2\" }, \"uri\", \"http:\\\/\\\/evertpot.com\\\/\" ], [ \"bday\", { }, \"date-and-or-time\", \"1985-04-07\" ], [ \"x-jabber\", { \"type\": \"HOME\", \"pref\": \"1\" }, \"unknown\", \"evertpot@gmail.com\" ], [ \"uid\", { }, \"text\", \"35269e7016a018e3\" ] ]] | Contact in jCard format |

### Alerts structure

```javascript
    {
        "id":900,
        "timeType":4,
        "time":5,
        "timeSpecified":"2016-08-31T11:00:00.000+04:00",
        "repeat":2,
        "repeatInterval":5,
        "sound":true,
        "alert":true,
        "email":true,
        "push":true
    }
```

|Field        |Type         |Example         |Description|
|-------------|-------------|----------------|-----------|
|id | long | 900 | optional: if id is not specified then new alert will be created, or existing updated otherwise |
|timeType| long | 4 |  mandatory; possible values: 1 - specified time, 2 - days before, 3 - hours before, 4 - minutes before |
|time | long | 5 | mandatory if timeType in [2, 3, 4] |
|timeSpecified | date | "2016-08-31T11:00:00.000+04:00"|  mandatory if timeType=1, format is same as for start_date and end_date of item object |
|repeat | long | 2 | optional: how many times reminder should be repeated |
|repeatInterval | long | 5| optional: repeat interval in minutes |
|sound | boolean | true |  optional: play sound |
|alert | boolean | true | optional: display notification in desktop/browser version of application |
|email | boolean | true | optional: send email |
|push | boolean | true |optional: send push notification to mobile device |



To Create/Update/Delete reminders:

```javascript
[
    {"timeType":4,"time":0,"repeat":1,
    "repeatInterval":0,"sound":true,"alert":true,
    "email":true,"push":true},
    {"timeType":4,"time":5,"repeat":1,
    "repeatInterval":0,"sound":true,"alert":true,"email":true,
    "push":true},
    {"timeType":3,"time":1,"repeat":1,
    "repeatInterval":0,"sound":true,"alert":true,"email":true,
    "push":true},
    {"timeType":1,"timeSpecified":"2016-08-31T11:00:00.000+04:00",
    "repeat":1,"repeatInterval":0,"sound":true,"alert":true,
    "email":true,"push":true}
]
```

* Create: simply add new alert to array and put data to server
* Update: simply update existing alert in array (id must be specified in alert object) and put data to server
* Delete: simply remove alert from array and put data to server

Alert object description:




### Permissions

Permission is defined by a level integer value.

| Level | Description | Title displayed in client | Sub-title (description) displayed in client app |
|--------|------|-------|------|
| 0/none | Not visible to user. Server does not return this item in user's items | _Not visible_ | |
| 10 | User can see item in list. Item sub-items and file attachments. Item history. | View | |
| 20 | User can add comments to item | *View and Comment* | See in their lists, View details, Add comments |
| 30 | User can add attachments. Can add sub-items, If project- can create new items in project | *Add sub-tasks and attachments* , "Create tasks in project" | |
| 40 | User can assign/reassign | "Assign" | |
| 50 | User can Complete, Log time. Transition to another status (future) | *Complete and Assign* | Complete, reassign to another Team member, Attach documents, Add sub-tasks, Log time. |
| 60 | User can modify all properties (except Sharing permissions) | *Modify* | Modify item except its Sharing permissions |
| 70 | Can change sharing permissions (can add level 70 but not remove) | "Share with others" | |
| 80 | User can archive item |  |
| 100 | User can delete item | *Everything* | Modify, Change sharing, Delete, Archive |


### Unread value

| Unread | What it means | Relationship to item |
|--------- | ------- | -----------|
| 0 or null | Item is read (default) | |
| 1 | Comment added | User is participant or assignee or creator. Comment added by someone else |
| 2 | Modified, sub-item added | Assignee, participant, creator |
| 3 | New item | Assignee, participant, creator |

### Contact item

Contact item type has contact field that contains Contact details in jCard format. Fields compatible ith VCARD encoded with JSON.

```javascript
{
	"title": "201911071638",
	"category": 1,
	"contact": "[ \"vcard\", [ [ \"version\", { }, \"text\", \"4.0\" ], [ \"prodid\", { }, \"text\", \"-\\\/\\\/Sabre\\\/\\\/Sabre VObject 3.1.3\\\/\\\/EN\" ], [ \"n\", { }, \"text\", [ \"Pot\", \"Evert\", \"\", \"\", \"\" ] ],  [\"org\", { \"type\": \"work\" }, \"text\", \"Viagenie\"], [ \"email\", { \"type\": [ \"INTERNET\", \"HOME\" ] }, \"text\", \"evert@rooftopsolutions.nl\" ], [ \"email\", { \"type\": [ \"INTERNET\", \"WORK\" ] }, \"text\", \"evert@fruux.com\" ], [ \"tel\", { \"type\": [ \"CELL\", \"VOICE\" ] }, \"text\", \"+1 647 471 2661\" ], [ \"adr\", { \"type\": \"HOME\" }, \"text\", [ \"\", \"\", \"24 Settles Street\", \"London\", \"\", \"E1 1JP\", \"United Kingdom\" ] ], [ \"note\", { }, \"text\", \"Foo\" ], [ \"url\", { \"pref\": \"1\", \"group\": \"ITEM2\" }, \"uri\", \"http:\\\/\\\/evertpot.com\\\/\" ], [ \"bday\", { }, \"date-and-or-time\", \"1985-04-07\" ], [ \"x-jabber\", { \"type\": \"HOME\", \"pref\": \"1\" }, \"unknown\", \"evertpot@gmail.com\" ], [ \"uid\", { }, \"text\", \"35269e7016a018e3\" ] ]]"
}
```

## 1. Get array of items


* `GET    /item`

This method will return array of all items: tasks, events, files including projects.
It returns X-Cursor HTTP header. Cursor is a unix timestamp (in milliseconds) of server response. Example: 1478802464. It equals to timestamp of latest modified returned item.

```javascript
[{
    "id": 3361634,
    "user_id": 184743,
    "title": "event 5724 1",
    "completed": false,
    "color": 0,
    "color_value": "#2AAEF5",
    "category": 2,
    "message": null,
    "parent": 0,
    "recurring": 0,
    "recurring_interval": 1,
    "recurring_end_date": "2017-08-26T15:56:46.820+04:00",
    "time_last_update": "2016-08-26T18:04:04.340+04:00",
    "time_create": "2016-08-26T18:04:04.340+04:00",
    "start_date": "2016-08-27T00:00:00.000+04:00",
    "end_date": null,
    "due_date": null,
    "is_all_day": true,
    "shared": true,
    "reminder_enabled": null,
    "reminder_time": null,
    "reminder_time_type": null,
    "starred": false,
    "time_track": false,
    "time_est": 0,
    "time_spent": 0,
    "priority": 21720,
    "last_comment_id": null,
    "last_comment": null,
    "last_comment_user_id": null,
    "last_comment_create_datetime": null,
    "guid": "9769a9f9-726c-4ec8-a920-be16193c26a6",
    "parentGuid": null,
    "assignee": 0,
    "tags": null,
    "version": 1,
    "instances": null,
    "participants": null,
    "publish_url": null,
    "location": null,
    "alerts": null,
    "unread": null,
    "short_name": null,
    "issue_id": "164",
    "permission": 100,
    "permissions": [{
      "level": 100,
      "principal": "184743"
    }],
    "previews": null,
    "last_transition_time": null,
    "last_transition_user": null
  }

```

### 1.2 Get delta update of items

* `GET  	/item/since/{timestamp}`

Returns list of items that were changed or added since specified date.
It returns X-Cursor HTTP header. Cursor is a unix timestamp (in milliseconds) of server response. Example: 1478802464. It equals to timestamp of latest modified returned item.
Deprecated. Use /item/delta/{delta} instead.

### 1.3 Get delta update of items

* `GET      /item/delta/{delta}`

Returns list of items that were changed or added since specified delta. Delta is is a unix timestamp (in milliseconds) fetched from header X-Cursor.
It returns X-Cursor HTTP header. Cursor is a unix timestamp (in milliseconds) of server response. Example: 1478802464. It equals to timestamp of latest modified returned item.

```javascript
[{
  "id": 3361634,
  "changed": false
}, {
  "id": 3362490,
  "changed": false
}, {
  "id": 3362767,
  "changed": false
}, {
  "id": 3362336,
  "changed": false
}, {
  "id": 3362771,
  "guid": "123abc",
  "user_id": 184743,
  "title": "delta api",
  "completed": false,
  "color": 0,
  "color_value": "#2AAEF5",
  "category": 1,
  "parent": 0,
  "recurring": 0,
  "recurring_interval": 1,
  "recurring_end_date": "2017-11-14T12:25:29.964+04:00",
  "time_last_update": "2016-11-14T13:36:57.539+04:00",
  "time_create": "2016-11-14T13:36:19.429+04:00",
  "shared": true,
  "starred": true,
  "time_track": false,
  "time_est": 0,
  "time_spent": 0,
  "priority": 21760,
  "guid": "2141ab89-48ee-47b0-878e-c9ad304397b4",
  "assignee": 0,
  "version": 2,
  "changed": true,
  "issue_id": "632",
  "permission": 100,
  "permissions": [{
    "level": 60,
    "principal": "184769"
  }, {
    "level": 60,
    "principal": "184775"
  }, {
    "level": 100,
    "principal": "184743"
  }]
}]

```


## 2. Create Item

* `POST    /item` will create new item

### Mandatory parameters:

Param | Type | Description
------------ | ------------- | ------------
<code>guid</code>| uuid | Unique identifier
<code>title</code>| string | maximum 255 characters

### Optional parameters:

Param | Type | Description
------------ | ------------- | ------------
<code>parentGuid</code>| uuid | Unique identifier of parent item.


```
Example Post data:

title: Project title
message: Desription
category: 0
newProject: true
priority: 21010
user_id: 190150
color_value: #fc2f6a
short_name: PROJ
permissions: [{"principal":190150,"level":100}]
start_date: 2018-05-05T23:59:59.999+02:00
due_date: 2018-05-12T23:59:59.999+02:00
cascadeAcl: 1
permission: 100
doAdd: true
isSubItem: false
manytasks: false
```

### 2.1 Upload file

* `POST /file/upload` will upload file and create respective file item
* Request Content-Type should be `multipart/form-data`

### Mandatory params:
Param | Type | Description
------------ | ------------- | ------------
<code>session_id</code>| text | User session.
<code>file</code>| binary | Content of file to upload.

### Optional params:
Param | Type | Description
------------ | ------------- | ------------
<code>guid</code>| UUID | Item identifier.
<code>parent_id</code>| number | Parent item identifier.

### Response fields:
Field | Type | Description
------------ | ------------- | ------------
<code>id</code>| long | Globally unique primary identifier for a file item.

## 3. Update Item

* `PUT    /item` will update (modify) item

### Mandatory parameters:

Param | Type | Description
------------ | ------------- | ------------
<code>guid</code>| uuid | Unique identifier
<code>title</code>| string | maximum 255 characters

### Optional parameters:

Param | Type | Description
------------ | ------------- | ------------
<code>parentGuid</code>| uuid | Unique identifier of parent item.


### Response codes for Create and Update

HTTP code | API Error code | Description
------------ | ------------- | ------------
200 |  | Created/updated
400 | 73 | Unable to add {principal X} because project/parent item is not shared with {principal X}.
400 | 74 | {principal X} permission can not be {modified/added/removed} because it will conflict with parent {permission X} permissions.
400 | 75 | {user X} can not be {assignee/participant} because they don't have access to project {project name}.
400 | 76 | Owner {owner name} is not allowed to change own permission.
400 | 77 | Permission {principal X} downgrade to {permission X} is not allowed because parent has {permission Y} for this principal.
400 | 78 | Cannot remove {assignee/participant} {user name} permission.
400 | 80 | Short name already used.
400 |	104 | One of the parameters is mandatory



## 4. Delete

* `DELETE    /item/{guid}` will delete item

Parameters:
* {guid}: unique identifier of item.

User performing delete request must have sufficient rights to delete this object

Possible HTTP return responses:

* 200 operation successful
* 404 item not found. It may be already deleted or not visible to current user.
* 403 not authorised

## 5. History

### 5.1 Retrieve item history including comments:

* `GET    /item/history?id={item id}`

### 5.2 Add comment

* `POST    /item/comment` will add a new comment to the item

Parameters: id: item id, message: comment body text

### 5.3 Delete comment

* `DELETE    /item/comment` will delete comment



## 6. Archive

### 6.1 Archive item

Moves item to Archive

* `POST    /item/archive` will archive item

Parameters:
* id or guid: id or guid of item to archive.

User performing request must have sufficient rights to archive specified item.

Possible HTTP return responses:

* 200 operation successful
* 403 not authorised
* 404 item not found; it may be already archived or not visible to current user

### 6.2. Restore item from archive

* `GET    /archive/restore` will restore item from archive

Parameters:
* id or guid: id or guid of item to restore.

User performing request must have sufficient rights to restore specified item.

Possible HTTP return responses:

* 200 operation successful
* 403 not authorised
* 404 item not found
* 507 limit of items exceeded for current account

### 6.3. Restore copy of item from archive

* `GET    /archive/restorecopy` will restore copy of item from archive

Parameters:
* id or guid: id or guid of item which copy to restore.

User performing request must have sufficient rights to restore specified item.

Possible HTTP return responses:

* 200 operation successful
* 403 not authorised
* 404 item not found
* 507 limit of items exceeded for current account

## 7. Multiple items operations

### 7.1 Delete multiple items

* `POST    /item/deletemultiple` will delete items

Parameters:
* id: comma separated list of item identifiers (example: id=1,2,3).

User performing request must have sufficient rights to delete specified items.
No error will be rised and item delete request simply ignored if user does not have rights to delete specific item.

Possible HTTP return responses:

* 200 operation successful
* 400 invalid format of list of identifiers

### 7.2 Archive multiple items

* `POST    /item/archivemultiple` will archive multiple items

Parameters:
* id: comma separated list of item identifiers (example: id=1,2,3).

User performing request must have sufficient rights to archive specified items.
No error will be rised and item archive request simply ignored if user does not have rights to archive specific item.

Possible HTTP return responses:

* 200 operation successful
* 400 invalid format of list of identifiers
