# Error handling

You need to check HTTP status in case there's an error. Basic rule is to check that code is not 200. If it's not 200 then expanded error code and error message will be in Json data.

When response statux is not 200 OK. The response contains Json date in format:

```json
{
 "error_message" : "This is an error message";
 "response_status" : 1;
}
```

The  API uses the following HTTP error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- 
401 | Unauthorized -- Your API key is wrong or unauthorized
403 | Forbidden -- The requested is forbidden
404 | Not Found -- The specified item could not be foun
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.

Also, API uses following response codes:

Response Code Name | Response Code | Description Template
------------------ | ------------- | -------
OK | 0 | "Ok"
NOT_FOUND | 1 | "%s not found"
UNIQUE_USER_PARAMETER_VIOLATION | 2 | "User with given %s already exists"
NO_PERMISSIONS | 3 | "No enough permissions %s"
IS_MANDATORY | 4 | "%s is mandatory%s"
INVALID_DATA_FORMAT | 5 | "Invalid data format of %s"
INVALID_DATA | 6 | "%s is not valid %s"
SESSION_NOT_FOUND | 7 | "Session not found, please authenticate first"
INVALID_API_KEY | 8 | "Invalid API Key"
INVALID_JSON_VERSION | 9 | "API version must be %s or higher"
STALE_OBJECT | 10 | "You are trying to update old object, which was cnaged on %s" 
BAD_TARGET_USER | 11 | "Error sending message to user with id=%s" 
LICENSE_OVERUSE | 12 | "You have no enough licenses to add new user"
FILE_NOT_READY | 13 | "File is not ready"
CONTACT_SELF_ADD | 14 | "You can't add yourself to the contact list"
CONTACT_EXIST | 15 | "Contact already exists"
USER_ALREADY_IN_BUSINESS | 16 | "User %s already in a business group"
OPERATION_NOT_ALLOWED | 17 | "%s operation is not allowed"
NO_EMAIL | 18 | "No email provided for user"
EMAIL_NOT_VALIDATED | 19 | "Email is not confirmed: please confirm your email address"
LIMIT_EXCEED | 20 | "%s limit exceeded"
LOGIN_ID_TAKEN | 21 | "Login id is already taken"	
EMAIL_ALREADY_REGISTERED | 22 | "Email is already registered"
CLIENT_UPGRADE_REQUIRED | 23 | "Client upgrade required"
PARTICIPANTS_ADDING_ERROR | 24 | "User %s couldn't be added as participant"
EXCEEDED_SIZE | 25 | "Maximum size for %s is %s"
PAYMENT_ERROR | 30 | "Payment error: %s"
PAYMENT_DATA_INVALID | 31,"Payment data is not valid"
PICTURE_UPLOAD_ERROR | 32 | "Upload failed"
NOT_BUSINESS_USER | 33 | "You are not a business user"
INVALID_PICTURE_CROP_PARAMETERS | 34 | "Crop parameters are invalid"
INVALID_PICTURE_HASH | 35 | "Provided picture hash either does not exist or you are not allowed to modify this picture."
PASSWORD_NOT_MATCH | 36 | "Provided password does not match your current password"
BUSINESS_DOMAIN_NAME_USED | 37 | "This domain name is already in use"
REGISTER_INVALID_EMAIL_FORMAT | 38 | "Invalid data format of email"
REGISTER_INVALID_LOGIN_FORMAT | 39 | "Invalid data format of user name"
REGISTER_INVALID_NAME_FORMAT | 40 | "Invalid data format of first name or last name"
FREE_PROJECTS_LIMIT_EXCEEDED | 41 | "Free projects limit exceeded"
FREE_TASKS_LIMIT_EXCEEDED | 42 | "Free tasks limit exceeded"
API_KEY_ALREADY_EXISTS | 43 | "You already created the API key, please delete it before creating the new"
INVITATION_USED | 45 | "Invitation already used"
INVALID_JSON_BODY | 46 | "The JSON body you provided in request is invalid"
INVALID_RECURRING_INTERVAL | 47 | "Minimum recurring interval value is %d. Maximum recurring interval value is %d"
ACCOUNT_TERMINATED | 48 | "Sorry but your account was terminated"
UNSUPPORTED_EXTERNAL_PROVIDER_ID | 49 | "Such external social provider is not supported"
EXTERNAL_ACCOUNT_DETAILS_INVALID | 50 | "External account details are not full or invalid"
EXTERNAL_ACCOUNT_EMAIL_DOES_NOT_MATCH_INVITATION_EMAIL | 51 | "External account email must be equal to email used in this invitation"
EXTERNAL_SYNC_REFRESH_TOKEN_REQUIRED | 52 | "Refresh token is required for external synchronization because of its offline nature"
EXTERNAL_SYNC_EXTERNAL_ACCOUNT_REQUIRED | 53 | "You do not have required %s account linked"
INSUFFICIENT_API_KEY_PERMISSIONS | 54 | "The API key you provided has not enough permission in order to run requested command"
NOT_READY | 55 | "%s is not ready"
EXTERNAL_ACCOUNT_ALREADY_LINKED | 56 | "This %s account is already used %s"
EXTERNAL_ACCOUNT_TYPE_ALREADY_LINKED | 57 | "You already have external account of this type linked"
MIRROR_ITEM_MODIFICATION_FORBIDDEN | 58 | "You are not allowed to %s this item"
EXTERNAL_SYNC_IS_RUNNING | 59 | "External synchronization is being executed currently.%s"
UNKNOWN_PRODUCT_OR_PLAN | 60 | "Selected product plan and/or product is not supported"
UNKNOWN_PPAYMENT_PROCESSOR | 61 | "Could not process your payment using selected processor %s"
ALREADY_SUBSCRIBED | 62 | "You are already subscribed to this plan."
LICENSE_USAGE_GREATER_THAN_PLAN_LICENSES | 63 | "Current team license usage is greater than number of licenses of selected subscription plan."
ALREADY_PUBLISHED_PLAN | 64 | "Such subscription plan already published."
NO_PERMISSIONS_TO_MANAGE_SUBSCRIPTION | 65 | "Team account administrator %s is responsible for renewing the subscription."
GOOGLE_NOTIFICATIONS_OVERLOADED | 66 | "Google notifications processor overloaded: please try again in few seconds"
CUSTOM_API_KEY_USAGE_LIMIT_EXCEEDED | 67 | "You are performing too many API requests per second"
CANT_REMOVE_PLAN | 68 | "Plan can be removed only if it is unpublished and without customers."
ACCOUNT_EXPIRED | 69 | "Account subscription expired. Please visit http://%s to subscribe.")
EXTERNAL_ACCOUNT_CREDENTIALS_EXPIRED | 70 | "It appears that %s access token expired. Please visit Settings, remove external account and link it again with HiTask. Sorry for the inconvenience."
EXTERNAL_ERROR | 71 | "Error: %s."
TEAM_ACCOUNT_TERMINATED_ERROR | 72 | "Team account terminated."
UNABLE_TO_SHARE_BECAUSE_OF_PROJECT | 73 | "Unable to add %s because project/parent item is not shared with %s"
UNABLE_TO_ALTER_PERMISSION_OF_CHILD_TASK | 74 | "%s permission can not be %s because it will conflict with parent %s permissions."
UNABLE_TO_ASSIGN_OR_PARTICIPATE_BECAUSE_NO_PERMISSIONS | 75 | "%s can not be %s because they don't have access to project %s"
OWNER_CANT_CHANGE_OWN_PERMISSION | 76 | "Owner %s is not allowed to change own permission"
UNABLE_TO_DOWNGRADE_PERMISSION | 77 | "Permission '%s' downgrade to '%s' is not allowed because parent has '%s' for this principal"
UNABLE_TO_REMOVE_PERMISSION_OF_ASSIGNEE_OR_PARTICIPANT | 78 | "Cannot remove %s %s permission"
USER_ALREADY_INVITED_IN_THIS_TEAM | 79 | "User %s already invited in current team"
SHORT_NAME_ALREADY_USED | 80 | "Short name already used"
UNABLE_TO_PARSE_FILE | 81 | "Unable to parse the file"
PARSED_FILE_CONTAINS_NO_ENTRIES | 82 | "Parsed file contains 0 entries"
FILE_FORMAT_NOT_SUPPORTED | 83 | "File format is not supported"
INVALID_GOOGLE_AUTH_CODE | 84 | "%s is not valid google auth code%s"
FORBIDDEN_TO_ACCESS_AREA | 85 | "You are not allowed to access %s. Account upgrade required."
ENDPOINT_DEPRECATED | 86 | "Current endpoint deprecated since %s."
SCORE_LIMIT_REACHED | 87 | "\"%s\" daily limit reached."
INVALID_PICTURE_MINIMUM_EDGE_LENGTH | 88 | "Minimum length for each edge of the picture is %spx"
INTERNAL_ERROR | 100 | "Internal error"
