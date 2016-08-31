---
title: API Reference

language_tabs:
  - shell
  - javascript
  - json
  - java

toc_footers:
  - <a href='https://hitask.com/signup'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - user
  - team
  - item
  - tag
  - group
  - contact
  - errors

search: true
---

# Introduction

[HiTask](http://hitask.com) is an online task and project management software. With hiTask you can share tasks and projects with your team, add multi-user comments, track time, attach files, produce reports and much more.

* **RESTful.** API is designed in accordance with [REST](http://en.wikipedia.org/wiki/Representational_state_transfer) patterns and is so called RESTful API.
* **JSON.** Hitask support JSON for serialization of data. Response data is returned as root element.





## API Endpoint URL

API endpoint is `https://hitask.com/api/{method}` where {method} is the name of API method. 


# Authentication

This API is SSL/HTTPS only.

All methods require authentication. Authentication achieved through [User.authenticate](#user) which returns session id.
Your application have to provide the session id with every request. There are two ways of doing this:

* Cookie. If your application framework supports cookies automatically you don't have to do anything, cookie will be sent with every request.
* HTTP header parameter. Alternatively you can provide session id as "x-hi-session" header with every request.

### Rate limiting

We only allow a certain number of requests per client per minute. If you exceed this limit you will have to wait before your next request is processed.


## API Key

> To authorize, use this code:

```javascript

```


```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: "
```


> Make sure to replace `your_key` with your API key.

To access the API you need to have API Key. API Key is a unique identifier assigned to you. To get your Key simply go into your hiTask account settings page. You  will be asked to provide the name of your integration/app.
You are required to provide your API Key as a parameter for some methods, for example API Key is required when you authenticate user session: [User.authenticate](#user)


`Authorization: your_key`

<aside class="notice">
You must replace <code>your_key</code> with your personal API key.
</aside>

