---
title: IQRisk Query API Reference

language_tabs:
  - shell
  - python: Python (2.x)

toc_footers:
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - domains
  - ips
  - samples
  - sids
  - errors

search: true
---

# Introduction

> Summary of Resource URL Patterns

```plaintext
/v1/repcategories

/v1/domains/{domain}/events
/v1/domains/{domain}/geoloc
/v1/domains/{domain}/ips
/v1/domains/{domain}/nameservers
/v1/domains/{domain}/reputation
/v1/domains/{domain}/samples
/v1/domains/{domain}/urls
/v1/domains/{domain}/whois

/v1/ips/{ip}/domains
/v1/ips/{ip}/events
/v1/ips/{ip}/geoloc
/v1/ips/{ip}/reputation
/v1/ips/{ip}/samples
/v1/ips/{ip}/urls

/v1/samples/{md5}
/v1/samples/{md5}/connections
/v1/samples/{md5}/dns
/v1/samples/{md5}/events
/v1/samples/{md5}/http

/v1/sids/{sid}
/v1/sids/{sid}/ips
/v1/sids/{sid}/domains
/v1/sids/{sid}/samples
```

The IQRisk Query API is organized around REST with JSON responses. Our API is designed to use HTTP response codes to indicate API success/errors. We support cross-origin resource sharing (CORS) to allow you to interact with our API from a client-side web application. JSON will be returned in all responses from the API.

The IQRisk Query API can be used to get information such as up-to-date reputation of domains and IPs, as well as related information on our entire database of over 100 million malware samples.

We currently have code examples using curl, and are working on other language examples. If you have a particular language you'd like to see API examples for, please let us know. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authenticate, use this code:

```shell
# With curl, you can just pass the correct header with each request
curl https://api.emergingthreats.net/v1/repcategories -H "Authorization: SECRETKEY"
```

```python
from urllib2 import Request, urlopen
request = Request("api_endpoint_here")
request.add_header("Authorization", "SECRETKEY")
```

> Make sure to replace `SECRETKEY` with your API key.

Emerging Threats uses API keys to allow access to our API. If your company has paid for API access, you can find your API key by visiting [https://portal.emergingthreats.net/api-access](https://portal.emergingthreats.net/api-access).

The Query API expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: SECRETKEY`

<aside class="notice">
You must replace `SECRETKEY` with your personal API key.
</aside>


# Rate-limiting

The IQRisk Query API will rate limit requests on a per-API key basis. If you exceed your rate limit you will receive an API response with a 429 HTTP status code and a brief message indicating you have exceeded your rate limit.
To increase your rate limit, contact sales.

> The JSON response associated with an exceeded rate limit should look something like:

```json
{
  "success": false,
  "message": "Rate limit exceeded",
  "response": {}
}
```

# Reputation Metadata

## List reputation categories

```shell
curl https://api.emergingthreats.net/v1/repcategories -H "Authorization: SECRETKEY"
```

```python
from urllib2 import Request, urlopen
request = Request("https://api.emergingthreats.net/v1/repcategories")
request.add_header("Authorization", "SECRETKEY")
result = urlopen(request)
print result.read()
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "name": "Bot",
      "description": "Known Infected Bot"
    },
    {
      "name": "CnC",
      "description": "Malware Command and Control Server"
    },
    {
      "name": "Spam",
      "description": "Known Spam Source"
    }
  ]
}
```

This endpoint lists all of the possible categories for reputation categorization and a brief description of each item.

### HTTP Request

`GET https://api.emergingthreats.net/v1/repcategories`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
name | No | The name of the reputation category.
description | No | A brief description of the category.
