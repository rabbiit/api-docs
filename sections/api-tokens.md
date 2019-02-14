# API Tokens

* [Security](#security)
* [Generate API token](#generate)
* [Distroy a API token](#distroy)

Authentication to the API is performed via HTTP Bearer Auth.   
On every request you must send on HTTP header `Authorization: Bearer <api_token>`.   
You do not need to provide an email or password on your request after get your API token.

<a name="security"></a>
## Security

API tokens are generated using email and password of a user.
API tokens carry all privileges of a user 
and grant access to their account, 
so be sure to keep them secure and secret! 
Do not share your API tokens in publicly accessible areas such as GitHub, client-side code, and so forth.

Each API token is valid only to [User Agent](https://en.wikipedia.org/wiki/User_agent) that has generated. 
Call made by another User Agent will return `401 Unauthorized` status code 
and will distroy this API token and make permanently invalid for news requests.

API Tokens without access for more than 30 days are automatically distroyed.  

<a name="generate"></a>
## Generate API token

**POST** `/api/v1/auth`

Argument|Type|Description
---------|----|-----
email | text | Access email of user
password | text | Password of user 
account_id | text | Id of Rabbiit account.

The `account_id` argument could be found on the URL of web app. 
When you be logged on the Rabbiit app, find the account_id on the URL after `/a/`. 
The URL should be similar to the pattern `https://app.rabbiit.com/a/{ACCOUNT_ID}/#/projects` 

Example request

```shell
curl https://app.rabbiit.com/api/v1/auth
-d email=john@acme.inc
-d password=123456
-d account_id=124893893dd8
```

Example response:
```json
{
    "token": "FrxRtCwWut3PMp9Boj7FQ9ndyZYQggcIF8xtpByI0Fis6-KPOzB1Ownj0b",
    "account_id": "124893893dd8"
} 
```
   
Now copy the token generated and replace into `<api_token>` on HTTP header named `Authorization`.  

```shell
curl https://app.rabbiit.com/api/v1/projects
-H "Authorization: Bearer <api_token>"  
```

<a name="distroy"></a>
## Distroy a API token

**GET** `/api/v1/auth/revoke`

Example request:

```shell
curl https://app.rabbiit.com/api/v1/auth/revoke
-H "Authorization: Bearer FrxRtCwWut3PMp9Boj7FQ9ndyZYQggcIF8xtpByI0Fis6-KPOzB1Ownj0b"
```

Response body empty with status code `200`.
