## About

Bulk Email Verification Tool at https://mailveri.com.

## Free API

This API can be used to verify whether an email is valid when a user signs up for an account on a website.

This API involves two steps: first, you need to send a <b>POST</b> request, and then you use the <b>token</b> received in the response to retrieve the result by making a <b>GET</b> request.

Here is the API documentation with a self-explanatory cURL example:

### POST

```
curl -X POST https://free.mailveri.com --data-urlencode "mail=<verifyingEmail>"
```

Success response with HTTP status code 200 with JSON body:

| Field  | Type    | Description |
| ------ | ------- | ----------- |
| token  | string  | Unique token to be used in the next step |
| wait   | integer | Wait time in milliseconds before making the next request |


Error response with HTTP status codes 4xx with JSON body:

| Field  | Type    | Description |
| ------ | ------- | ------------|
| error  | string  | Error details |
| wait   | integer | Wait time in milliseconds before making the next request |

### GET

```
curl -X GET https://free.mailveri.com/?mail=<verifyingEmail>&token=<tokenReturnedFromPOST>
```

Success response with HTTP status code 200 with JSON body:

| Field  | Type    | Description |
| ------ | ------- | ----------- |
| status | string  | GOOD: The email is good to send emails <br> BAD: The email is bad; do not send to it <br> UGLY (aka. UNKNOWN): No result available yet, result expired, or domain not supported |
| info   | string  | (Optional) Additional information |

Error response with HTTP status codes 4xx with empty body.
