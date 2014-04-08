---
title: API Reference

language_tabs:
  - curl

toc_footers:
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

---

# Introduction

The IQRisk Query API is organized around REST with JSON responses. Our API is designed to use HTTP response codes to indicate API success/errors. We support cross-origin resource sharing (CORS) to allow you to interact with our API from a client-side web application. JSON will be returned in all responses from the API.

The IQRisk Query API can be used to get information such as up-to-date reputation of domains and IPs, as well as related information on our entire database of over 100 million malware samples.

We currently have code examples using curl, and are working on other language examples. If you have a particular language you'd like to see API examples for, please let us know. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authenticate, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: SECRETKEY"
```

> Make sure to replace `SECRETKEY` with your API key.

Emerging Threats uses API keys to allow access to our API. If your company has paid for API access, you can find your API key by visiting [https://portal.emergingthreats.net/api-access](https://portal.emergingthreats.net/api-access).

The Query API expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: SECRETKEY`

<aside class="notice">
You must replace `SECRETKEY` with your personal API key.
</aside>


# Malware Samples

## Get sample details

```shell
curl "https://api.emergingthreats.net/v1/samples/<md5>"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": {
    "submit_date": "2012-06-11 04:00:00",
    "file_type": "PE32 executable for MS Windows (DLL) (console) Intel 80386 32-bit",
    "file_size": 69459,
    "sha256": "e12012672d33cbcb22cf953ff787af250f8f5e920c565f03d4496a619c13a889",
    "ssdeep": "12288:ANkX6n+UtdHEhnLaoO2Ze9c+pq2NmUR0SEDRqHW2BUddM5d0HWO2QIbQ:8kX6n+uuNWoO2497p/NmURUyUddM5d0x"
  }
}
```

This endpoint retrieves metadata information for a single malware sample.

### HTTP Request

`GET https://api.emergingthreats.net/v1/samples/<md5>`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
md5 | None | The md5sum of the malware sample to be retrieved.

## Get sample connections

```shell
curl "https://api.emergingthreats.net/v1/samples/<md5>/connections"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "source": "177f3c8a2623d4efb41b0020d680be83",
      "date": "2014-03-31",
      "source_ip": "10.10.10.104",
      "destination_ip": "178.254.11.36",
      "source_port": 49382,
      "destination_port": 80,
      "bytes_down": 508,
      "bytes_up": 306,
      "bytes_total": 814,
      "packets_down": 4,
      "packets_up": 6,
      "packets_total": 10,
      "protocol": "tcp"
    },
    {
      "source": "177f3c8a2623d4efb41b0020d680be83",
      "date": "2014-03-31",
      "source_ip": "10.10.10.104",
      "destination_ip": "208.117.232.117",
      "source_port": 49381,
      "destination_port": 80,
      "bytes_down": 0,
      "bytes_up": 0,
      "bytes_total": 0,
      "packets_down": 2,
      "packets_up": 4,
      "packets_total": 6,
      "protocol": "tcp"
    }
  ]
}
```

This endpoint retrieves the most recent connections an individual malware sample was observed to have made.

### HTTP Request

`GET https://api.emergingthreats.net/v1/samples/<md5>/connections`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
md5 | None | The md5sum of the malware sample whose connections are to be retrieved.

# Whois Info

## Get Domain Whois Info

```shell
curl "https://api.emergingthreats.net/v1/whois-info/bing.com"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": {
    "domain": "bing.com",
    "registrant": {
      "name": "Microsoft Corporation",
      "email": "domains@microsoft.com",
      "created": "1996-01-29",
      "updated": "2012-11-29",
      "expired": "2019-01-30"
    },
    "registrar": {
      "name": "MarkMonitor Inc.",
      "country": "USA",
      "website": "http://www.markmonitor.com"
    }
  }
}
```

This endpoint retrieves whois info for a single domain.

### HTTP Request

`GET https://api.emergingthreats.net/v1/whois-info/<domain>`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | None | The domain of the whois info to be retrieved.
