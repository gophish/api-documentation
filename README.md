# Gophish API Reference

Gophish was built from the ground-up with a JSON API that makes it easy for developers and sysadmins to automate simulated phishing campaigns.

These docs describe how to use the [gophish](https://getgophish.com) API.

## Authorization
{% method %}
All API requests require the use of a generated API key. You can find your API key, or generate a new one, by navigating to the /settings endpoint, or clicking the “Settings” sidebar item.

When making requests, simply append the `api_key=[API_KEY]` as a GET parameter to authorize yourself to the API.

{% sample lang="http" %}
```
GET /api/campaigns/?api_key=12345678901234567890123456789012
```
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| `api_key` | `string` | **Required**. Your Gophish API key |
{% endmethod %}

