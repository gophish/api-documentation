# Templates

A "Template" is the content of the emails that are sent to targets. They can be imported from an existing email, or created from scratch.

Additionally, templates can contain tracking images so that gophish knows when the user opens the email.

Templates have the following structure:

```
{
  id            : int64
  name          : string
  subject       : string
  text          : string
  html          : string
  modified_date : string(datetime)
  attachments   : list(attachment)
}
```

> Note: The `modified_date` field is updated automatically. It is not required to set this when creating or modifying a template.

To add tracking, make sure you specify a `{{.Tracker}}` in the `html` field. The UI adds this automatically, but it needs to be specified if you're using the API.

Templates support sending attachments. Attachments have the following structure:

```
  content: string
  type   : string`
  name   : string`
```

> Note: The `content` field in an attachment is expected to be base64 encoded.

## Get Templates
{% method %}

Returns a list of templates.

{% sample lang="http" %}
```http
GET /api/templates/?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |

```
[
  {
    "id" : 1,
    "name" : "Password Reset Template",
    "subject" : "{{.FirstName}}, please reset your password.",
    "text" : "Please reset your password here: {{.URL}}",
    "html" : "<html><head></head><body>Please reset your password <a href\"{{.URL}}\">here</a></body></html>",
    "modified_date" : "2016-11-21T18:30:11.1477736-06:00",
    "attachments" : [],
  }
]
```
{% endmethod %}

## Get Template
{% method %}

Returns a template given an ID. 

Returns a 404 error if the specified template isn't found.

{% sample lang="http" %}
```http
GET /api/templates/1?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `id`      | `int64`  | **Required**. The template ID      |

```
{
  "id" : 1,
  "name" : "Password Reset Template",
  "subject" : "{{.FirstName}}, please reset your password.",
  "text" : "Please reset your password here: {{.URL}}",
  "html" : "<html><head></head><body>Please reset your password <a href\"{{.URL}}\">here</a></body></html>",
  "modified_date" : "2016-11-21T18:30:11.1477736-06:00",
  "attachments" : [],
}
```
{% endmethod %}

## Create Template
{% method %}

Creates a template.

This method expects the template to be provided in JSON format. You must provide a template `name` and the `text` and/or `html` for the template.

This method returns the JSON representation of the template that was created.

{% sample lang="http" %}
```http
GET /api/templates/?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `name`      | `int64`  | **Required, Unique**. The template name.|
| `text` or `html` | string | **Required** The template text or HTML |

```
{
  "id" : 1,
  "name" : "Password Reset Template",
  "subject" : "{{.FirstName}}, please reset your password.",
  "text" : "Please reset your password here: {{.URL}}",
  "html" : "<html><head></head><body>Please reset your password <a href\"{{.URL}}\">here</a></body></html>",
  "modified_date" : "2016-11-21T18:30:11.1477736-06:00",
  "attachments" : [],
}
```
{% endmethod %}

## Modify Template
{% method %}

Modifies an existing template.

This method expects the template to be provided in JSON format. You must provide a full template, not just the fields you want to update.

This method returns the JSON representation of the template that was modified.

{% sample lang="http" %}
```http
PUT /api/templates/1?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `name`      | `int64`  | **Required, Unique**. The template name.|
| `text` or `html` | string | **Required** The template text or HTML |

```
{
  "id" : 1,
  "name" : "Password Reset Template",
  "subject" : "{{.FirstName}}, please reset your password.",
  "text" : "Please reset your password here: {{.URL}}",
  "html" : "<html><head></head><body>Please reset your password <a href\"{{.URL}}\">here</a></body></html>",
  "modified_date" : "2016-11-21T18:30:11.1477736-06:00",
  "attachments" : [],
}
```
{% endmethod %}

## DELETE Template
{% method %}

Deletes a template by ID. 

Returns a 404 error if the specified template isn't found.

This method returns a status message indicating the template was deleted successfully.

{% sample lang="http" %}
```http
DELETE /api/templates/1?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `id`      | `int64`  | **Required**. The template ID      |

### Response
```
{
  "message": "Template deleted successfully!",
  "success": true,
  "data": null
}
```
{% endmethod %}


