# Rabbiit API Documentation V1

* [Introduction](#introduction)
* [Making a request](#make-request)
* [HTTP status codes](#http-status-codes)
* [Authentication](#authentication)
* [Response codes and error handling](#response-codes)
* [API Endpoints](#api-endpoints)

<a name="introduction"></a>
## Introduction

Rabbiit is a [time tracking software](https://rabbiit.com/) for teams and consultants,
that allows you manage time in an easy way.

Rabbiit API is a [RESTful](http://en.wikipedia.org/wiki/Representational_State_Transfer) web service.
Accepts [form-encoded](https://en.wikipedia.org/wiki/POST_(HTTP)#Use_for_submitting_web_forms) request bodies, 
returns [JSON-encoded](https://en.wikipedia.org/wiki/JSON) responses, 
and uses standard HTTP response status codes, authentication, and verbs.

Accepted request types (HTTP verbs) are: GET, POST, DELETE.

Base URL
```shell
https://app.rabbiit.com/api/v1
```

<a name="authentication"></a>
## Authentication

Rabbiit API use [API Tokens](sections/api-tokens.md) to authenticate requests. 

API tokens are generated using email and password of a user.
API tokens carry all privileges of a user 
and grant access to their account, 
so be sure to keep them secure and secret! 
Do not share your API tokens in publicly accessible areas such as GitHub, client-side code, and so forth.

Each API token is valid only to [User Agent](https://en.wikipedia.org/wiki/User_agent) that has generated. 
Call made by another User Agent will return `401 Unauthorized` status code 
and will make this API token permanently invalid.  

Authentication to the API is performed via HTTP Bearer Auth. 
On every request use HTTP header named `Authorization` and `Bearer <api_token>` value. 
You do not need to provide an email or password.

Read the [API Tokens guide](sections/api-tokens.md) for see how generate and manage your API tokens.

<a name="make-request"></a>
## Making a request

All API request must be made over [HTTPS](https://pt.wikipedia.org/wiki/Hyper_Text_Transfer_Protocol_Secure). 
Call made over unsafe HTTP will fail. 

Example request using `curl` for retrieving the projects

```shell
curl https://app.rabbiit.com/api/v1/projects
-H "Authorization: Bearer FrxRtCwWut3PMp9Boj7FQ9ndyZYQggcIF8xtpByI0Fis6-KPOzB1Ownj0b"  
```

Example request using `curl` for updating a customer

```shell
curl https://app.rabbiit.com/api/v1/customers/121
-H "Authorization: Bearer FrxRtCwWut3PMp9Boj7FQ9ndyZYQggcIF8xtpByI0Fis6-KPOzB1Ownj0b"
-d name="ACME INC."  
```

<a name="response-codes"></a>
## Response codes and error handling

Rabbiit API use [HTTP Status codes](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes) to indicate the successful or failure request.
 
The class of `2xx` status code indicates success requests. 
The class of `4xx` status code indicates that failed given the information provided, 
in general the response will contain a message that explains the error reported. 
The classs of `5xx` status code indicates a failured on Rabbiit's server.

<a name="api-endpoints"></a>
## API endpoints

* [Projects](sections/projects.md)

## Help us make it better
. 
If you have any request or if you found a bug, please use GitHub issues. 
Fork these docs and send a pull request with improvements.
