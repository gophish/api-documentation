# Gophish API Reference

Gophish was built from the ground-up with a JSON API that makes it easy for developers and sysadmins to automate simulated phishing campaigns.

These docs describe how to use the [gophish](https://getgophish.com) API.

## Authorization
{% method %}
All API requests require the use of a generated API key. You can find your API key, or generate a new one, by navigating to the /settings endpoint, or clicking the “Settings” sidebar item.

When making requests, simply append the `api_key=[API_KEY]` as a GET parameter to authorize yourself to the API.

{% sample lang="http" %}
```http
GET /api/campaigns/?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
{% endmethod %}

## Responses
Many API endpoints return the JSON representation of the resources created or edited. However, if an invalid request is submitted, or some other error occurs, Gophish returns a JSON response in the following format:

```
{
  "message" : string,
  "success" : bool,
  "data"    : string
}
```

The `message` attribute contains a message commonly used to indicate errors or, in the case of deleting a resource, success that the resource was properly deleted.

The `success` attribute describes if the transaction was successful or not.

The `data` attribute contains any other metadata associated with the response. This will be an escaped string containing JSON data.

## Status Codes
Gophish returns the following status codes in its API:

| Status Code | Description |
|-------------| ----------- |
| 200 | `OK` |
| 201 | `CREATED` |
| 400 | `BAD REQUEST` |
| 404 | `NOT FOUND` |
| 500 | `INTERNAL SERVER ERROR`|