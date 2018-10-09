# Users & Groups

Gophish manages recipients for campaigns in groups. Each group can contain one or more recipients. Groups have the following format:

```text
{
    id              : int64
    name            : string
    targets         : array(Target)
    modified_date   : string(datetime)
}
```

Each recipient in the `targets` field has the following format:

```text
{
    email           : string
    first_name      : string
    last_name       : string
    position        : string
}
```

{% api-method method="get" host="https://localhost:3333" path="/api/groups/" %}
{% api-method-summary %}
Get Groups
{% endapi-method-summary %}

{% api-method-description %}
Returns a list of groups.
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
    "name": "Example Group",
    "modified_date": "2018-10-08T15:56:13.790016Z",
    "targets": [
      {
        "email": "user@example.com",
        "first_name": "Example",
        "last_name": "User",
        "position": ""
      },
      {
        "email": "foo@bar.com",
        "first_name": "Foo",
        "last_name": "Bar",
        "position": ""
      }
    ]
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/groups/:id" %}
{% api-method-summary %}
Get Group
{% endapi-method-summary %}

{% api-method-description %}
Returns a group with the given ID.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The group ID
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
  "name": "Example Group",
  "modified_date": "2018-10-08T15:56:13.790016Z",
  "targets": [
    {
      "email": "user@example.com",
      "first_name": "Example",
      "last_name": "User",
      "position": ""
    },
    {
      "email": "foo@bar.com",
      "first_name": "Foo",
      "last_name": "Bar",
      "position": ""
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
  "message": "Group not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Returns a 404 error if no group is found with the provided ID.

{% api-method method="get" host="https://localhost:3333" path="/api/groups/summary" %}
{% api-method-summary %}
Get Groups Summary
{% endapi-method-summary %}

{% api-method-description %}
Returns a summary of each group.
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
    "name": "Example Group",
    "modified_date": "2018-10-08T15:56:13.790016Z",
    "num_targets": 2
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://localhost:3333" path="/api/groups/:id/summary" %}
{% api-method-summary %}
Get Group Summary
{% endapi-method-summary %}

{% api-method-description %}
Returns a summary for a group.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The group ID
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
  "name": "Example Group",
  "modified_date": "2018-10-08T15:56:13.790016Z",
  "num_targets": 2
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "message": "Group not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

It may be the case that you just want the number of members in a group, not necessarily the full member details. This API endpoint returns a summary for a group.

Returns a 404 error if no group is found with the provided ID.

{% api-method method="post" host="https://localhost:3333" path="/api/groups/" %}
{% api-method-summary %}
Create Group
{% endapi-method-summary %}

{% api-method-description %}
Creates a new group.
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
The group to create in JSON format.
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
  "name": "Example Group",
  "modified_date": "2018-10-08T15:56:13.790016Z",
  "targets": [
    {
      "email": "user@example.com",
      "first_name": "Example",
      "last_name": "User",
      "position": ""
    },
    {
      "email": "foo@bar.com",
      "first_name": "Foo",
      "last_name": "Bar",
      "position": ""
    }
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
If an invalid request is provided, an error message will be returned
{% endapi-method-response-example-description %}

```
{
  "message": "Group name not specified",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

When creating a new group, you must specify a unique `name`, as well as a list of `targets`. Here's an example request body:

```javascript
{
    "name": "Example Group",
    "targets": [
    {
        "email": "user@example.com",
        "first_name": "Example",
        "last_name": "User",
        "position": ""
    },
    {
        "email": "foo@bar.com",
        "first_name": "Foo",
        "last_name": "Bar",
        "position": ""
    }
    ]
}
```

{% api-method method="put" host="https://localhost:3333" path="/api/groups/:id" %}
{% api-method-summary %}
Modify Group
{% endapi-method-summary %}

{% api-method-description %}
Modifies a group.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="integer" required=true %}
The group ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Payload" type="object" required=true %}
The updated group content. The full group must be provided in JSON format.
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
  "name": "Example Modified Group",
  "modified_date": "2018-10-08T15:56:13.790016Z",
  "targets": [
    {
      "email": "foo@bar.com",
      "first_name": "Foo",
      "last_name": "Bar",
      "position": ""
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
  "message": "Group not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This API endpoint allows you to modify an existing group. The request must include the complete group JSON, not just the fields you're wanting to update. This means that you need to include the matching `id` field. Here's an example request:

```javascript
{
    "id": 1,
    "name": "Example Modified Go",
    "targets": [
    {
        "email": "foo@bar.com",
        "first_name": "Foo",
        "last_name": "Bar",
        "position": ""
    }
    ]
}
```

Returns a 404 if no group is found with the provided ID.

{% api-method method="delete" host="https://localhost:3333" path="/api/groups/:id" %}
{% api-method-summary %}
Delete Group
{% endapi-method-summary %}

{% api-method-description %}
Deletes a group
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="number" required=true %}
The group ID
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
  "message": "Group deleted successfully!",
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
  "message": "Group not found",
  "success": false,
  "data": null
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Returns a 404 error if no group is found with the provided ID.

{% api-method method="post" host="https://localhost:3333" path="/api/import/group" %}
{% api-method-summary %}
Import Group
{% endapi-method-summary %}

{% api-method-description %}
Reads and parses a CSV, returning data that can be used to create a group.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
A valid API key
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="file" type="object" required=true %}
A file upload containing the CSV content to parse.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
[
  {
    "email": "foobar@example.com",
    "first_name": "Example",
    "last_name": "User",
    "position": "Systems Administrator"
  },
  {
    "email": "johndoe@example.com",
    "first_name": "John",
    "last_name": "Doe",
    "position": "CEO"
  }
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

This API endpoint allows you to upload a CSV, returning a list of group targets. For example, you can use the following `curl` command to upload the CSV:

```text
curl -k https://localhost:3333/api/import/group -XPOST \
    -F "file=@group_template.csv" \
    -H "Authorization: Bearer 0123456789abcdef"
```

The results of this API endpoint can be used as the `targets` parameter in a call to the [Create Group](users-and-groups.md#create-group) endpoint.

