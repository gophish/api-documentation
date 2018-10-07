# Settings

{% api-method method="post" host="https://localhost:3333" path="/api/reset" %}
{% api-method-summary %}
Reset API Key
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to reset your API key to a new, randomly generated key.  
  
This method requires you to authenticate using your existing API key.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
The existing API key.
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
API key successfully reset. The new API key is provided in the `data` response parameter.
{% endapi-method-response-example-description %}

```javascript
{
    "success": true,
    "message": "API Key successfully reset!",
    "data": "0123456789abcdef"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



