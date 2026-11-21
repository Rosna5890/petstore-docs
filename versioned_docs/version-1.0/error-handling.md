---
title: Error Handling
sidebar_position: 4
---

# Error Handling

The Document API uses standard HTTP status codes. Codes in the `2xx` range mean success, codes in the `4xx` range mean there is a problem with your request, and codes in the `5xx` range mean a problem on our side.

## Error response format

Errors return a JSON body that describes what went wrong:

```json
{
  "error": {
    "code": "MISSING_FIELD",
    "message": "signerEmail is required.",
    "field": "signerEmail"
  }
}
```

## Status Codes

| Status | Meaning | What to do |
|---|---|---|
| `400` | The request is invalid, for example a required field is missing. | Check the request body against the endpoint reference. |
| `401` | The API Key is missing or invalid. | Check the `X-API-Key` header. |
| `403` | The key is valid, but not allowed to do the particular action. | Check the assigned permissions of the key. |
| `404` | No resource exists with this ID. | Check the resource ID and the request path. |
| `429` | You exceeded the rate limit. | Wait for the time in the 'Retry-After' header and try again. |
| `500` | An unexpected error occured on our side. | Wait a few seconds and retry, then contact support if it continues. |

## Handling Rate Limits

The API allows 100 requests per minute for each API key. When you exceed the limit, the response includes a `Retry-After` header with the number of seconds to wait.

:::tip
Retry with increasing delays: wait 1 second, then 2, then 4. This is called exponential backoff, and it avoids hitting the limit again straight away.
:::

## Handling Server Errors

:::warning
Before retrying a failed `POST` request, check whether the document was already created. Retrying blindly can create a duplicate.
:::

If a `500` error continues, contact support and include the time of the request and the request ID from the response.