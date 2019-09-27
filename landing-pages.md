# Landing Pages

A "Landing Page" is the HTML content returned when targets click on the links in Gophish emails.

Landing pages have the following structure:

```text
{
  id                  : int64
  name                : string
  description         : string
  html                : string
  capture_credentials : bool
  capture_passwords   : bool
  modified_date       : string(datetime)
  redirect_url        : string
}
```

{% api-method method="get" host="https://localhost:3333" path="/api/pages/" %}
{% api-method-summary %}
Get Landing Pages
{% endapi-method-summary %}

{% api-method-description %}
Returns a list of landing pages.
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
    "id": 1,
    "name": "Example Page",
    "description": "Description of example landing page",
    "html": "<html><head></head><body>This is a test page</body></html>",
    "capture_credentials": true,
    "capture_passwords": true,
    "redirect_url": "http://example.com",
    "modified_date": "2016-11-26T14:04:40.4130048-06:00"
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/pages/:id" %}
{% api-method-summary %}
Get Landing Page
{% endapi-method-summary %}

{% api-method-description %}
Returns a landing page given an ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The landing page ID
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
   "id": 1,
   "name": "Example Page",
   "description": "Description of example landing page",
   "html": "<html><head></head><body>This is a test page</body></html>",
   "capture_credentials": true,
   "capture_passwords": true,
   "redirect_url": "http://example.com",
   "modified_date": "2016-11-26T14:04:40.4130048-06:00"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Page not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Returns a 404 error if the specified landing page isn't found.

{% api-method method="post" host="https://localhost:3333" path="/api/pages/" %}
{% api-method-summary %}
Create Landing Page
{% endapi-method-summary %}

{% api-method-description %}
Creates a landing page.
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
The JSON representation of the landing page to be created
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=201 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
   "id": 1,
   "name": "Example Page",
   "description": "Description of example landing page",
   "html": "<html><head></head><body>This is a test page</body></html>",
   "capture_credentials": true,
   "capture_passwords": true,
   "redirect_url": "http://example.com",
   "modified_date": "2016-11-26T14:04:40.4130048-06:00"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This method expects the landing page to be provided in JSON format. You must provide a landing page `name` and the `html` for the landing page.

{% hint style="info" %}
**Importing a Site**

Let Gophish do the hard work for you by importing a site. By using the [Import Site](landing-pages.md#import-site) endpoint, you can simply give Gophish a URL and have the site fetched for you and returned in a format that can be used with this method.
{% endhint %}

#### Capturing Credentials

Capturing credentials is a powerful feature of Gophish. By setting certain flags, you have the ability to capture all user input, or just non-password input.

To capture credentials, set the `capture_credentials` attribute. If you want to capture passwords as well, set the `capture_passwords` attribute.

By default, Gophish will not capture passwords, as they are stored in plaintext.

Gophish also provides the ability to redirect users to a URL after they submit credentials. This is controlled by setting the `redirect_url` attribute.

{% api-method method="put" host="https://localhost:3333" path="/api/pages/:id" %}
{% api-method-summary %}
Modify Landing Page
{% endapi-method-summary %}

{% api-method-description %}
Modifies an existing landing page.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The ID of the landing page to modify
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
The JSON representation of the landing page to be modified
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
   "id": 1,
   "name": "Example Page",
   "description": "Description of example landing page",
   "html": "<html><head></head><body>This is a test page</body></html>",
   "capture_credentials": true,
   "capture_passwords": true,
   "redirect_url": "http://example.com",
   "modified_date": "2016-11-26T14:04:40.4130048-06:00"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Page not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Returns a 404 error if the specified landing page isn't found.

This method expects the landing page to be provided in JSON format. You must provide a full landing page, not just the fields you want to update.

This method returns the JSON representation of the landing page that was modified.

{% api-method method="delete" host="https://localhost:3333" path="/api/pages/:id" %}
{% api-method-summary %}
Delete Landing Page
{% endapi-method-summary %}

{% api-method-description %}
Deletes a landing page.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The ID of the landing page to delete
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
  "message": "Page Deleted Successfully",
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
  "message": "Page not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Returns a 404 error if the specified landing page isn't found.

This method returns a status message indicating the landing page was deleted successfully.

{% api-method method="post" host="https://localhost:3333" path="/api/import/site" %}
{% api-method-summary %}
Import Site
{% endapi-method-summary %}

{% api-method-description %}
Fetches a URL to be later imported as a landing page
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="include\_resources" type="boolean" required=false %}
Whether or not to create a `<base>` tag in the resulting HTML to resolve static references \(recommended: `false`\)
{% endapi-method-parameter %}

{% api-method-parameter name="url" type="string" required=true %}
The URL to fetch
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "html": "<html><head>..."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This endpoint simply fetches and returns the HTML from a provided URL. If `include_resources` is `false` \(recommended\), a `<base>` tag is added so that relative links in the HTML resolve from the original URL.

Additionally, if the HTML contains form elements, this endpoint adds another input, `__original_url`, that points to the original URL. This makes it possible to replay captured credentials later.

{% hint style="info" %}
**Note:** This API endpoint doesn't actually create a new landing page. Instead, you can use the HTML returned from this endpoint as an input to the [Create Landing Page](landing-pages.md#create-landing-page) method.
{% endhint %}



