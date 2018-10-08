# Sending Profiles

A "Sending Profile" is the SMTP configuration that tells Gophish how to send emails.

Sending profiles support authentication and ignoring invalid SSL certificates.

Sending Profiles have the following structure:

```text
{
  id                 : int64
  name               : string
  username           : string (optional)
  password           : string (optional)
  host               : string
  interface_type     : string
  from_address       : string
  ignore_cert_errors : boolean (default:false)
  modified_date      : string(datetime)
  headers            : array({key: string, value: string}) (optional)
}
```

{% api-method method="get" host="https://localhost" path="/api/smtp/" %}
{% api-method-summary %}
Get Sending Profiles
{% endapi-method-summary %}

{% api-method-description %}
Gets a list of the sending profiles created by the authenticated user.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
A list of the sending profiles created by the authenticated user.
{% endapi-method-response-example-description %}

```javascript
[
  {
    "id" : 1,
    "name":"Example Profile",
    "interface_type":"SMTP",
    "from_address":"John Doe <john@example.com>",
    "host":"smtp.example.com:25",
    "username":"",
    "password":"",
    "ignore_cert_errors":true,
    "modified_date": "2016-11-20T14:47:51.4131367-06:00",
    "headers": [
      {
        "key": "X-Header",
        "value": "Foo Bar"
      }
    ]
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/smtp/:id" %}
{% api-method-summary %}
Get Sending Profile
{% endapi-method-summary %}

{% api-method-description %}
Returns a sending profile given an ID, returning a 404 error if no sending profile with the provided ID is found.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The sending profile ID to return
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id" : 1,
  "name":"Example Profile",
  "interface_type":"SMTP",
  "from_address":"John Doe <john@example.com>",
  "host":"smtp.example.com:25",
  "username":"",
  "password":"",
  "ignore_cert_errors":true,
  "modified_date": "2016-11-20T14:47:51.4131367-06:00",
  "headers": [
    {
      "key": "X-Header",
      "value": "Foo Bar"
    }
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "SMTP not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://localhost:3333" path="/api/smtp" %}
{% api-method-summary %}
Create Sending Profile
{% endapi-method-summary %}

{% api-method-description %}
Creates a sending profile.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
The body of the request is a JSON representation of a sending profile. Refer to the introduction for the valid format of a sending profile.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id" : 1,
  "name":"Example Profile",
  "interface_type":"SMTP",
  "from_address":"John Doe <john@example.com>",
  "host":"smtp.example.com:25",
  "username":"",
  "password":"",
  "ignore_cert_errors":true,
  "modified_date": "2016-11-20T14:47:51.4131367-06:00",
  "headers": [
    {
      "key": "X-Header",
      "value": "Foo Bar"
    }
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
If required fields aren't provided, or if a sending profile already exists with the provided name, a 400: Bad Request error will be returned.
{% endapi-method-response-example-description %}

```javascript
{
  "message": "Error message indicating the issue",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This method expects the sending profile to be provided in JSON format. You must provide a sending profile `name`, the `from_address` which emails are sent from, and the SMTP relay `host`.

Sending Profiles support authentication by setting the `username` and `password`.

Additionally, many SMTP server deployments leverage self-signed certificates. To tell Gophish to ignore these invalid certificates, set the `ignore_cert_errors` field to `true`.

This method returns the JSON representation of the sending profile that was created.

{% api-method method="put" host="https://localhost:3333" path="/api/smtp/:id" %}
{% api-method-summary %}
Modify Sending Profile
{% endapi-method-summary %}

{% api-method-description %}
Modifies an existing sending profile.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The sending profile ID to modify
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
The body of the request is a JSON representation of a sending profile. Refer to the introduction for the valid format of a sending profile.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id" : 1,
  "name":"Example Profile",
  "interface_type":"SMTP",
  "from_address":"John Doe <john@example.com>",
  "host":"smtp.example.com:25",
  "username":"",
  "password":"",
  "ignore_cert_errors":true,
  "modified_date": "2016-11-20T14:47:51.4131367-06:00",
  "headers": [
    {
      "key": "X-Header",
      "value": "Foo Bar"
    }
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
If no sending profile exists with the provided ID, a 404: Not Found error is returned.
{% endapi-method-response-example-description %}

```javascript
{
  "message": "SMTP not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This method expects the sending profile to be provided in JSON format. You must provide a full sending profile, not just the fields you want to update.

This method returns the JSON representation of the sending profile that was modified.

{% api-method method="delete" host="https://localhost:3333" path="/api/smtp/:id" %}
{% api-method-summary %}
Delete Sending Profile
{% endapi-method-summary %}

{% api-method-description %}
Deletes a sending profile by ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The ID of the sending profile to delete
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "SMTP deleted successfully!",
  "success": true,
  "data": null
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "SMTP not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Returns a 404 error if the specified sending profile isn't found.

This method returns a status message indicating the sending profile was deleted successfully.

