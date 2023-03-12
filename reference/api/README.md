# API

{% hint style="info" %}
If you prefer OpenAPI/Swagger Documentations, click [here](https://api.cartesius.io/beta/openapi#/default/ForwardController\_forwardRequest).
{% endhint %}

### URL

`https://api.cartesius.io/<version>/<endpoint>`

HTTP requests will automatically be redirected to HTTPS.

### Authentication

To use the API, you need an [API Key.](../../cartesius-studio/api-keys.md) You can create an API Key by [registering at Cartesius](https://app.cartesius.io/auth/signup). With a paid plan, you can also create multiple API Keys with [CORS](./#cors) and [IP-Restrictions](./#ip-restrictions).&#x20;

On HTTP API Requests, you can use the API Key in the query parameters with the key `apiKey` or you can add it in the request headers with `X-API-KEY`. If you use an Integration of Cartesius, please consult the documentation to see how to authenticate your requests.

### API Response Model

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "license": {
      "type": "string",
      "default": "https://cartesius.io/credits-and-licences/"
    },
    "code": {
      "type": "integer",
      "description": "HTTP Status Code"
    },
    "status": {
      "type": "string",
      "description": "Indicates whether the request was successful",
      "enum": ["success", "fail", "error"]
    },
    "messages": {
      "type": "array",
      "description": "Error messages and warnings",
      "items": {
        "type": "string"
      }
    },
    "data": {
      "type": "object",
      "description": "Request result data (such as list of geo-features)"
    },
    "traceId": {
      "type": "string",
      "description": "Unique request identifier for support requests"
    }
  },
  "required": ["code", "status", "traceId"]
}
```

### Rate Limiting

Depending on your plan, you are allowed to send a specific number of requests per day and per second, with a soft (overage is allowed) or hard limit (capped).

If you exceed one of the restrictions, the server will respond with a `429 Too Many Requests`.  The following headers will be sent to specify when you can send requests again:

| Header                                         | Description                                                         |
| ---------------------------------------------- | ------------------------------------------------------------------- |
| <pre><code>Retry-After
</code></pre>           | Number of seconds until a request will be allowed again.            |
| <pre><code>X-RateLimit-Remaining
</code></pre> | Remaining requests, you can send in the current timeframe (second). |
| <pre><code>X-RateLimit-Reset
</code></pre>     | Timestamp of the rate limit reset.                                  |
| <pre><code>X-RateLimit-Limit
</code></pre>     | Number of requests allowed per second.                              |

### CORS

Each API Key can have its own CORS restrictions. Cross-Origin Resource Sharing (CORS) is an HTTP-header based mechanism that allows a server to indicate any origins (domain, scheme, or port) apart from its own from which a browser should permit loading resources. You can specify domains for CORS in the [Studio](https://app.cartesius.io). They will be sent as `access-control-allow-origin`header.

### IP-Restrictions

Next to CORS, each API Key can also have its own IP restrictions. You can manage IPs that are allowed to access the API in the [Studio](https://app.cartesius.io). If an IP tries to call the API, that is not whitelisted, the request will be rejected `401 - Unauthorized`. The requests will not count towards your daily and secondly request limit.

### Versioning

{% hint style="warning" %}
Cartesius is currently in beta. We intend to deliver the first stable version (v1) mid-2023.
{% endhint %}

A new version will always be deployed if there are breaking changes. You will be informed on the new version via email or in the [Studio](https://app.cartesius.io).&#x20;

**Current Versions**

| Version Tag | URL                                        | Changelog     |
| ----------- | ------------------------------------------ | ------------- |
| beta        | `https://api.cartesius.io/beta/<endpoint>` | Nightly build |
| v1          | Coming mid-2023                            |               |
