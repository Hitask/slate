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
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
