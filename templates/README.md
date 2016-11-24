# Templates
{% set exampleTemplate = "{
  \"id\" : 1,
  \"name\" : \"Example Template\",
  \"subject\" : \"{{.FirstName}}, please reset your password\",
  \"text\" : \"Click here to reset your password {{.URL}}\",
  \"html\" : \"<html><head></head><body>Click <a href=\"{{.URL}}\">here</a> to reset your password.{{.Tracker}}</body></html>\"
}" %}

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

> Note: The `modified_date` field is updated automatically. It is not required to set this when creating or modifying a template.

```
Templates support sending attachments. Attachments have the following structure:

```
  content: string
  type   : string`
  name   : string`
```

> Note: The `content` field in an attachment is expected to be base64 encoded.

## Get Templates
{% method %}
Returns an list of templates.

{% sample lang="http" %}
```http
GET /api/templates/?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |

```
[
  {{exampleTemplate}}
]
```
{% endmethod %}

