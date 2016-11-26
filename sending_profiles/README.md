# Sending Profiles

A "Sending Profile" is the SMTP configuration that tells Gophish how to send emails.

Sending profiles support authentication and ignoring invalid SSL certificates.

Sending Profiles have the following structure:

```
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
}
```

## Get Sending Profiles
{% method %}

Returns a list of sending profiles.

{% sample lang="http" %}
```http
GET /api/smtp/?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |

```
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
    "modified_date": "2016-11-20T14:47:51.4131367-06:00"
  }
]
```
{% endmethod %}

## Get Sending Profile
{% method %}

Returns a sending profile given an ID. 

Returns a 404 error if the specified sending profile isn't found.

{% sample lang="http" %}
```http
GET /api/smtp/1?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `id`      | `int64`  | **Required**. The sending profile ID      |

```
{
  "id" : 1,
  "name":"Example Profile",
  "interface_type":"SMTP",
  "from_address":"John Doe <john@example.com>",
  "host":"smtp.example.com:25",
  "username":"",
  "password":"",
  "ignore_cert_errors":true,
  "modified_date": "2016-11-20T14:47:51.4131367-06:00"
}
```
{% endmethod %}

## Create Sending Profile
{% method %}

Creates a sending profile.

This method expects the sending profile to be provided in JSON format. You must provide a sending profile `name`, the `from_address` which emails are sent from, and the SMTP relay `host`.

Sending Profiles support authentication by setting the `username` and `password`.

Additionally, many SMTP server deployments leverage self-signed certificates. To tell Gophish to ignore these invalid certificates, set the `ignore_cert_errors` to `true`.

This method returns the JSON representation of the sending profile that was created.

{% sample lang="http" %}
```http
GET /api/smtp/?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `name`    | `int64`  | **Required, Unique**. The sending profile name.|
| `from_address` | string | **Required** The address to send emails from |
| `host`    | string | **Required** The `host:port` of the SMTP relay to send emails through

```
{
  "name":"Example Profile",
  "interface_type":"SMTP",
  "from_address":"John Doe <john@example.com>",
  "host":"smtp.example.com:25",
  "username":"",
  "password":"",
  "ignore_cert_errors":true
}
```
{% endmethod %}

## Modify Sending Profile
{% method %}

Modifies an existing sending profile.

This method expects the sending profile to be provided in JSON format. You must provide a full sending profile, not just the fields you want to update.

This method returns the JSON representation of the sending profile that was modified.

{% sample lang="http" %}
```http
PUT /api/smtp/1?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `name`      | `int64`  | **Required, Unique**. The sending profile name.|
| `from_address` | string | **Required** The address to send emails from |
| `host`    | string | **Required** The `host:port` of the SMTP relay to send emails through

```
{
  "id" : 1,
  "name":"Example Profile",
  "interface_type":"SMTP",
  "from_address":"John Doe <john@example.com>",
  "host":"smtp.example.com:25",
  "username":"",
  "password":"",
  "ignore_cert_errors":true
}
```
{% endmethod %}

## Delete Sending Profile
{% method %}

Deletes a sending profile by ID. 

Returns a 404 error if the specified sending profile isn't found.

This method returns a status message indicating the sending profile was deleted successfully.

{% sample lang="http" %}
```http
DELETE /api/smtp/1?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key  |
| `id`      | `int64`  | **Required**. The sending profile ID|

### Response
```
{
  "message": "SMTP deleted successfully!",
  "success": true,
  "data": null
}
```
{% endmethod %}


