# User Management

Gophish supports having multiple user accounts. Each of these accounts are separate, with their own campaigns, landing pages, templates, etc.

Each user account in Gophish is assigned a **role**. These are global roles that describe the user's permissions within Gophish.

At the time of this writing, there are two roles:

| Role | Slug | **Description** |
| :--- | :--- | :--- |
| User | `user` | A non-administrative user role. Users with this role can create objects and launch campaigns. |
| Admin | `admin` | An administrative user. Users with this role can manage system-wide settings as well as other user accounts within Gophish. |

Users have the following format:

```text
{
    id              : int64
    username        : string
    role            : Role
    modified_date   : string(datetime)
}
```

Each Role has the following format:

```text
{
    name            : string
    slug            : string
    description     : string
}
```

{% api-method method="get" host="https://localhost:3333" path="/api/users/" %}
{% api-method-summary %}
Get Users
{% endapi-method-summary %}

{% api-method-description %}
Returns a list of all user accounts in Gophish.
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
    "username": "admin",
    "role": {
      "slug": "admin",
      "name": "Admin",
      "description": "System administrator with full permissions"
    }
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/users/:id" %}
{% api-method-summary %}
Get User
{% endapi-method-summary %}

{% api-method-description %}
Returns a user with the given ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The user ID
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
[
  {
    "id": 1,
    "username": "admin",
    "role": {
      "slug": "admin",
      "name": "Admin",
      "description": "System administrator with full permissions"
    }
  }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "User not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://localhost:3333" path="/api/users/" %}
{% api-method-summary %}
Create User
{% endapi-method-summary %}

{% api-method-description %}
Creates a new user.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="role" type="string" required=true %}
The role slug to use for the account
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=true %}
The password to set for the account
{% endapi-method-parameter %}

{% api-method-parameter name="username" type="string" required=true %}
The username for the account
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": 2,
  "username": "exampleuser",
  "role": {
    "slug": "user",
    "name": "User",
    "description": "User role with edit access to objects and campaigns"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
If an invalid request is provided, an error will be returned with the following format
{% endapi-method-response-example-description %}

```javascript
{
  "message": "Username already taken",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://localhost:3333" path="/api/users/:id" %}
{% api-method-summary %}
Modify User
{% endapi-method-summary %}

{% api-method-description %}
Modifies a user account. This can be used to change the role, reset the password, or change the username.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
The user ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="role" type="string" required=false %}
The role slug to use for the account
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=false %}
The password to set for the account
{% endapi-method-parameter %}

{% api-method-parameter name="username" type="string" required=true %}
The username for the account
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "id": 2,
  "username": "exampleuser",
  "role": {
    "slug": "user",
    "name": "User",
    "description": "User role with edit access to objects and campaigns"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
If an invalid request is provided, an error will be returned in the following format:
{% endapi-method-response-example-description %}

```javascript
{
  "message": "Username already taken",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "User not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="https://localhost:3333" path="/api/users/:id" %}
{% api-method-summary %}
Delete User
{% endapi-method-summary %}

{% api-method-description %}
Deletes a user, as well as every object \(landing page, template, etc.\) and campaign they've created.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
The user ID
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
  "message": "User deleted Successfully!",
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
  "message": "User not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Returns a 404 error if no user is found with the provided ID.

