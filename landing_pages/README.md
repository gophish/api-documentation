# Landing Pages

A "Landing Page" is the HTML content returned when targets click on the links in Gophish emails.

Landing pages have the following structure:

```
{
  id                  : int64
  name                : string
  html                : string
  capture_credentials : bool
  capture_passwords   : bool
  modified_date       : string(datetime)
  redirect_url        : string
}
```

## Get Landing Pages
{% method %}

Returns a list of landing pages.

{% sample lang="http" %}
```http
GET /api/pages/?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |

```
[
  {
    "id": 1,
    "name": "Example Page",
    "html": "<html><head></head><body>This is a test page</body></html>",
    "capture_credentials": true,
    "capture_passwords": true,
    "redirect_url": "http://example.com",
    "modified_date": "2016-11-26T14:04:40.4130048-06:00"
  }
]
```
{% endmethod %}

## Get Landing Page
{% method %}

Returns a landing page given an ID. 

Returns a 404 error if the specified landing page isn't found.

{% sample lang="http" %}
```http
GET /api/pages/1?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `id`      | `int64`  | **Required**. The landing page ID  |

```
{
  "id": 1,
  "name": "Example Page",
  "html": "<html><head></head><body>This is a test page</body></html>",
  "capture_credentials": true,
  "capture_passwords": true,
  "redirect_url": "http://example.com",
  "modified_date": "2016-11-26T14:04:40.4130048-06:00"
}
```
{% endmethod %}

## Create landing page
{% method %}

Creates a landing page.

This method expects the landing page to be provided in JSON format. You must provide a landing page `name` and the `html` for the landing page.

> Note: The `modified_date` field is updated automatically. It is not required to set this when creating or modifying a landing page.

#### Capturing Credentials

Capturing credentials is a powerful feature of Gophish. By setting certain flags, you have the ability to capture all user input, or just non-password input.

To capture credentials, set the `capture_credentials` attribute. If you want to capture passwords as well, set the `capture_passwords` attribute.

By default, Gophish will not capture passwords, as they are stored in plaintext.

Gophish also provides the ability to redirect users to a URL after they submit credentials. This is controlled by setting the `redirect_url` attribute.

This method returns the JSON representation of the landing page that was created.

{% sample lang="http" %}
```http
GET /api/pages/?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `name`      | `int64`  | **Required, Unique**. The landing page name.|
| `html` | string | **Required** The landing page HTML |

```
{
  "name": "Example Page",
  "html": "<html><head></head><body>This is a test page</body></html>",
  "capture_credentials": true,
  "capture_passwords": true,
  "redirect_url": "http://example.com"
}
```
{% endmethod %}

## Modify Landing Page
{% method %}

Modifies an existing landing page.

This method expects the landing page to be provided in JSON format. You must provide a full landing page, not just the fields you want to update.

This method returns the JSON representation of the landing page that was modified.

{% sample lang="http" %}
```http
PUT /api/pages/1?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `id`      | `int64`  | **Required**. The landing page ID  |
| `name`      | `int64`  | **Required, Unique**. The landing page name.|
| `html` | string | **Required** The landing page HTML |

```
{
  "name": "Example Page",
  "html": "<html><head></head><body>This is a test page</body></html>",
  "capture_credentials": true,
  "capture_passwords": true,
  "redirect_url": "http://example.com"
}
```
{% endmethod %}

## Delete Landing Page
{% method %}

Deletes a landing page by ID. 

Returns a 404 error if the specified landing page isn't found.

This method returns a status message indicating the landing page was deleted successfully.

{% sample lang="http" %}
```http
DELETE /api/landing pages/1?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `id`      | `int64`  | **Required**. The landing page ID  |

### Response
```
{
  "message": "Page deleted successfully!",
  "success": true,
  "data": null
}
```
{% endmethod %}



