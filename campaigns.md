# Campaigns

Campaigns have the following structure:

```text
{
  id                  : int64
  name                : string
  created_date        : string(datetime)
  launch_date         : string(datetime)
  completed_date      : string(datetime)
  template            : Template
  page                : Page
  status              : string
  results             : []Result
  groups              : []Group
  timeline            : []Event
  smtp                : SMTP
  url                 : string
}
```

The `template`, `page`, `groups`, and `smtp` objects are all Gophish objects. Their format can be found at their various API endpoints.

Gophish keeps track of every event for a campaign in it's `timeline`. Each event has the following format:

```text
{
  email                : string
  time                 : string(datetime)
  message              : string
  details              : string
}
```

In addition to this, campaign results are maintained in the `results` attribute. This has a format similar to the members of a `Group`, in that they have the following structure:

```text
{
  id                   : int64
  first_name           : string
  last_name            : string
  position             : string
  status               : string
  ip                   : string
  latitude             : float
  longitude            : float
  send_date            : string(datetime)
}
```

## Get Campaigns

Returns a list of campaigns.

```http
GET /api/campaigns/?api_key=12345678901234567890123456789012
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `api_key` | `string` | **Required**. Your Gophish API key |

```text
[
  {
    <TODO>
  }
]
```

## Get Campaign

Returns a campaign given an ID.

Returns a 404 error if the specified campaign isn't found.

```http
GET /api/campaigns/1?api_key=12345678901234567890123456789012
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `id` | `int64` | **Required**. The landing page ID |

```text
{
  <TODO>
}
```

## Create Campaign

Creates a campaign.

This method expects the campaign to be provided in JSON format. You must provide the following details in a campaign:

#### Scheduling a Campaign

You can schedule a campaign to launch at a later time. To do this, simply put the desired time you want the campaign to launch in the `launch_date` attribute.

Here's an example:

```http
POST /api/campaigns/?api_key=12345678901234567890123456789012
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `name` | `int64` | **Required, Unique**. The landing page name. |
| `html` | string | **Required** The landing page HTML |

```text
{
  "name": "Example Page",
  "html": "<html><head></head><body>This is a test page</body></html>",
  "capture_credentials": true,
  "capture_passwords": true,
  "redirect_url": "http://example.com"
}
```

## Modify Landing Page

Modifies an existing landing page.

This method expects the landing page to be provided in JSON format. You must provide a full landing page, not just the fields you want to update.

This method returns the JSON representation of the landing page that was modified.

```http
PUT /api/pages/1?api_key=12345678901234567890123456789012
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `id` | `int64` | **Required**. The landing page ID |
| `name` | `int64` | **Required, Unique**. The landing page name. |
| `html` | string | **Required** The landing page HTML |

```text
{
  "name": "Example Page",
  "html": "<html><head></head><body>This is a test page</body></html>",
  "capture_credentials": true,
  "capture_passwords": true,
  "redirect_url": "http://example.com"
}
```

## Delete Campaign

Deletes a campaign by ID.

Returns a 404 error if the specified campaign isn't found.

This method returns a status message indicating the campaign was deleted successfully.

```http
DELETE /api/campaigns/1?api_key=12345678901234567890123456789012
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `api_key` | `string` | **Required**. Your Gophish API key |
| `id` | `int64` | **Required**. The landing page ID |

### Response

```text
{
  "message": "Campaign deleted successfully!",
  "success": true,
  "data": null
}
```

## Get Campaign Summary

## Complete Campaign

