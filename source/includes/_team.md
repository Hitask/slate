# Team

## 1. Get Team account information

* `GET /business`

> Will produce the response: 

```js
{
    "domainName": "doman",
    "title": "Development Team",
    "licensesNumber": 15,
    "licensesUsed": 12,
    "storageQuota": 7500,
    "storageUsed": 157,
    "storageQuotaFormatted": "7.50GB",
    "storageUsedFormatted": "157MB",
    "expirationDate": "2016-10-17T00:00:00.000+00:00",
    "emailInbox": "2187b87d0bsds2dd9fe@hitask.com"}
```
### Response

  | Description 
------------ | ------------- 
domainName | subdomain name e.g. comapny.hitask.com 
title | Team name
licensesNumber | number of user licenses
licensesUsed | number of used user licenses
storageQuota | file storage space available (integer)
storageUsed | file storage space used (integer)
storageQuotaFormatted | file storage space available as humnan readable string
storageUsedFormatted | file storage space available as humnan readable string
expirationDate | Account expiration date for TRIAL or Next billing date for TEAM BUSINESS
emailInbox | Unique email address used to create tasks for team by email



Team members and team properties

## 2. Get list of team members

* `GET /team`

## 3. Invite to join team account

* `POST 	/team/member` 

### Parameters

Parameter | Type | Description
------------ | ------------- | ------------
email | string | Valid email address. **Required**
name | string | Full name. First name and last name separated by space. e.g. "Firstname Lastname"

### Response codes

HTTP code | API Error code | Description
------------ | ------------- | ------------
200 |  | Invited,added
400 | 5 | bad request, email address invalid
412 | 16 | Already a member, (this email address is already member of Team)
412 | 79 | User already invited in this team
400 | 12 | User licenses exceeded


## 4. Remove team member

Removes team member or invited user

* `DELETE /team/member`

### Parameters

Parameter | Type | Description
------------ | ------------- | ------------
id | integer | member user id

### Response codes

HTTP code | API Error code | Description
------------ | ------------- | ------------
200 |  | member removed
404 | 1 | member not found
400 | 4 | "id" parameter is mandatory

## 5. Resend invitation

In case user did not receive email invitation use this method to re-send invitation again

* `POST /team/member/resend`

### Parameters

Parameter | Type | Description
------------ | ------------- | ------------
email | string | Valid email address. **Required**

### Response codes

HTTP code | API Error code | Description
------------ | ------------- | ------------
200 |  | Invited,added
400 | 5 | bad request, email address invalid
412 | 16 | Already a member, (this email address is already member of Team)
400 | 12 | User licenses exceeded
