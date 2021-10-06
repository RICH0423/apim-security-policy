# apim-security-policy

- [user service api](https://6151c8204a5f22001701d425.mockapi.io/api/v1/users)

## Demo1: Threat Protection security

- api proxy endpoint: http://rich04230-eval-prod.apigee.net/users
- SQL injection sample:
```
?query=password’ OR 1=1
?query=1; DROP TABLE user;
```

## Demo2: API Key based API security
- api proxy endpoint: http://rich04230-eval-prod.apigee.net/users-apikey 
- apikey=BkGt9uWbraoBcNy9asyEizt7HMIks8D1


## Demo3: OAuth 2.0 based API security (Client Credentials)

- Get a valid OAuth access token

```bash
curl -X POST -H 'Content-Type: application/x-www-form-urlencoded' -H 'Accept: application/json' \
"https://rich04230-eval-prod.apigee.net/oauth/client_credential/accesstoken?grant_type=client_credentials" \
-d 'client_id=BkGt9uWbraoBcNy9asyEizt7HMIks8D1&client_secret=iZayCC7pYbrYNGLz'
```

```json
{
  "refresh_token_expires_in" : "0",
  "api_product_list" : "[user-service-product]",
  "api_product_list_json" : [ "user-service-product" ],
  "organization_name" : "rich04230-eval",
  "developer.email" : "rich04230@gmail.com",
  "token_type" : "BearerToken",
  "issued_at" : "1632884161113",
  "client_id" : "BkGt9uWbraoBcNy9asyEizt7HMIks8D1",
  "access_token" : "br1G6Kfn8EaGGVc50iECDFg8ORuw",
  "application_name" : "eea80998-537c-4a75-94aa-e688e4252d06",
  "scope" : "",
  "expires_in" : "3599",
  "refresh_count" : "0",
  "status" : "approved"
}
```

- test the protected API by passing in the valid access token
```bash
curl -X GET -H "Authorization: Bearer {ACCESS_TOKEN}" https://rich04230-eval-prod.apigee.net/users-oauth
```
