# Templates

A "Template" is the content of the emails that are sent to targets. They can be imported from an existing email, or created from scratch.

Additionally, templates can contain tracking images so that gophish knows when the user opens the email.

Templates have the following structure:

```text
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

Templates support sending attachments. Attachments have the following structure:

```text
  content: string
  type   : string
  name   : string
```

> Note: The `content` field in an attachment is expected to be base64 encoded.

{% api-method method="get" host="https://localhost:3333" path="/api/templates" %}
{% api-method-summary %}
Get Templates
{% endapi-method-summary %}

{% api-method-description %}
Returns a list of templates.
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

{% endapi-method-response-example-description %}

```javascript
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
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/templates/:id" %}
{% api-method-summary %}
Get Template
{% endapi-method-summary %}

{% api-method-description %}
Returns a template with the provided ID.  
  
Returns a 404: Not Found error if the specified template doesn't exist.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The template ID
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
    "name" : "Password Reset Template",
    "subject" : "{{.FirstName}}, please reset your password.",
    "text" : "Please reset your password here: {{.URL}}",
    "html" : "<html><head></head><body>Please reset your password <a href\"{{.URL}}\">here</a></body></html>",
    "modified_date" : "2016-11-21T18:30:11.1477736-06:00",
    "attachments" : [],
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Template not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://localhost:3333" path="/api/templates/" %}
{% api-method-summary %}
Create Template
{% endapi-method-summary %}

{% api-method-description %}
Creates a new template from the provided JSON request body.
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
The request body should be a JSON representation of a template. See the schema at the top of this page for the template format.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
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
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
At least one text or HTML field must be specified, otherwise a 400: Bad Request error is returned
{% endapi-method-response-example-description %}

```javascript
{
  "message": "Need to specify at least plaintext or HTML content",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This method expects the template to be provided in JSON format. You must provide a template `name` and the `text` and/or `html` for the template.

{% hint style="info" %}
**Importing an Existing Email** 

What better way to make pixel-perfect emails than by importing an existing email you already have in your inbox?

Using the [Import Email](templates.md#import-template) endpoint, you can take a raw email and parse it as a valid Gophish template.
{% endhint %}

To add tracking, make sure you specify a `{{.Tracker}}` in the `html` field. The UI adds this automatically, but it needs to be specified if you're using the API.

This method returns the JSON representation of the template that was created.

{% api-method method="put" host="https://localhost:3333" path="/api/templates/:id" %}
{% api-method-summary %}
Modify Template
{% endapi-method-summary %}

{% api-method-description %}
Modifies an existing template.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The template ID to modify
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
The JSON representation of the template you wish to modify. The entire template must be provided, not just the fields you wish to update.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This method expects the template to be provided in JSON format. You must provide a full template, not just the fields you want to update.

This method returns the JSON representation of the template that was modified.

{% api-method method="delete" host="https://localhost:3333" path="/api/templates/:id" %}
{% api-method-summary %}
Delete Template
{% endapi-method-summary %}

{% api-method-description %}
Deletes a template by ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Template deleted successfully!",
  "success": true,
  "data": null
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
If no template is found with the provided ID, a 404: Not Found error is returned
{% endapi-method-response-example-description %}

```javascript
{
  "message": "Template not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Returns a 404 error if the specified template isn't found.

This method returns a status message indicating the template was deleted successfully.

{% api-method method="post" host="https://localhost:3333" path="/api/import/email" %}
{% api-method-summary %}
Import Template
{% endapi-method-summary %}

{% api-method-description %}
Imports an email as a template.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="convert\_links" type="boolean" required=true %}
Whether or not to convert the links within the email to {{.URL}} automatically.
{% endapi-method-parameter %}

{% api-method-parameter name="content" type="string" required=true %}
The original email content in RFC 2045 format, including the original headers.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "text": "Email text",
  "html": "Email HTML",
  "subject": "Email subject"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

 Gophish provides the ability to parse an existing email to be used as a template. This makes it easy to repurpose legitimate emails for your phishing assessments.

This endpoint expects the raw email content in [RFC 2045 format](https://www.ietf.org/rfc/rfc2045.txt), including the original headers. Usually, this is found using the "Show Original" feature of email clients.

The request body for this endpoint is a JSON request in the form of:

```javascript
{
    content:       string
    convert_links: boolean
}
```

By setting the `convert_links` attribute to `true`, Gophish will automatically change all the links in the email to `{{.URL}}`.

{% hint style="info" %}
**Note:** This method doesn't fully import the email as a template. Instead, it parses the email, returning a response that can be used with the "[Create Template](templates.md#create-template)" endpoint.
{% endhint %}

