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

> Summary of Resource URL Patterns

```plaintext
/v1/domains/{domain}/urls

/v1/domains/{domain}/samples

/v1/domains/{domain}/ips

/v1/domains/{domain}/events

/v1/domains/{domain}/nameservers

/v1/domains/{domain}/whois

/v1/ips/{ip}/urls

/v1/ips/{ip}/samples

/v1/ips/{ip}/domains

/v1/ips/{ip}/events

/v1/samples/{md5}

/v1/samples/{md5}/connections

/v1/samples/{md5}/dns

/v1/samples/{md5}/http

/v1/samples/{md5}/events
```

The IQRisk Query API is organized around REST with JSON responses. Our API is designed to use HTTP response codes to indicate API success/errors. We support cross-origin resource sharing (CORS) to allow you to interact with our API from a client-side web application. JSON will be returned in all responses from the API.

The IQRisk Query API can be used to get information such as up-to-date reputation of domains and IPs, as well as related information on our entire database of over 100 million malware samples.

We currently have code examples using curl, and are working on other language examples. If you have a particular language you'd like to see API examples for, please let us know. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authenticate, use this code:

```shell
# With curl, you can just pass the correct header with each request
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


# Domain Information

## Get domain malware-requested URLs

```shell
curl "https://api.emergingthreats.net/v1/domains/{domain}/urls"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    "/index.php?id=XXXXXXXXXXXXXXX&scn=X&inf=X&ver=XX&cnt=XXX",
    "/index.php?id=XXXXXXXXXXXXXX&scn=X&inf=X&ver=XX&cnt=XXX",
    "/index.php?id=XXXXXXXXXXXXXXXXXX&scn=X&inf=X&ver=XX&cnt=XXX"
  ]
}
```

This endpoint retrieves the most recent http requests made by malware to the specified domain.

### HTTP Request

`GET https://api.emergingthreats.net/v1/domains/{domain}/urls`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
url | No | The url string of the request with query parameter values masked.

## Get domain related malware samples

```shell
curl "https://api.emergingthreats.net/v1/domains/{domain}/samples"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "source": "45999bfea907bf37acbab63d5d9ea683",
      "first_seen": "2014-02-13",
      "last_seen": "2014-02-13"
    },
    {
      "source": "f75da3cd3a38aadebdcf86eb53c6eb1c",
      "first_seen": "2014-02-13",
      "last_seen": "2014-02-13"
    }
  ]
}
```

This endpoint retrieves the most recent malware samples that communicated with the specified domain.

### HTTP Request

`GET https://api.emergingthreats.net/v1/domains/{domain}/samples`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
source | No | The md5sum of the malware sample.
first_seen | No | The date the malware sample was first seen associated to the domain.
last_seen | No | The date the malware sample was last seen associated to the domain.

## Get domain related IPs

```shell
curl "https://api.emergingthreats.net/v1/domains/{domain}/ips"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": {
    "213.219.245.212": [
      "2011-12-04 - 2012-02-27"
    ],
    "78.109.30.160": [
      "2014-02-22 - 2014-04-02"
    ]
  }
}
```

This endpoint retrieves the most recent IPs that have been associated with the specified domain.

### HTTP Request

`GET https://api.emergingthreats.net/v1/domains/{domain}/ips`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
ip | No | 
dates | No | The dates the IP has been observed to have been associated with the specified domain.

## Get domain related IDS events

```shell
curl "https://api.emergingthreats.net/v1/domains/{domain}/events"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "domain": "citi-bank.ru",
      "date": "2014-03-31",
      "source": false,
      "sid": "2803583",
      "signature": "ETPRO TROJAN Win32.Sality.At Checkin",
      "count": 1
    },
    {
      "domain": "citi-bank.ru",
      "date": "2014-03-23",
      "source": false,
      "sid": "2803583",
      "signature": "ETPRO TROJAN Win32.Sality.At Checkin",
      "count": 2
    }
  ]
}
```

This endpoint retrieves the most recent IDS events that have been observed against the specified domain.

### HTTP Request

`GET https://api.emergingthreats.net/v1/domains/{domain}/events`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
domain | No | 
date | No | The date the IDS event was observed.
source | No | Indicates whether the domain was the source of the IDS event.
sid | No | The SID that generated the IDS event.
signature | No | The signature name of the SID that generated the IDS event.
count | No | How many times this particular IDS event was observed in our sensor net for the given date.


## Get domain nameserver info

```shell
curl "https://api.emergingthreats.net/v1/domains/{domain}/nameservers"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "server": "ns1.yourhostingaccount.com.",
      "first_seen": "2013-02-15",
      "last_seen": "2013-11-17"
    },
    {
      "server": "ns1.mydomain.com",
      "first_seen": "2013-08-16",
      "last_seen": "2013-11-17"
    }
  ]
}
```

This endpoint retrieves the nameserver information related to the specified domain.

### HTTP Request

`GET https://api.emergingthreats.net/v1/domains/{domain}/nameservers`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
server | No | The address of a nameserver associated with the domain.
first_seen | Yes | The date the nameserver was first seen associated to the domain.
last_seen | Yes | The date the nameserver was last seen associated to the domain.


## Get domain whois info

```shell
curl "https://api.emergingthreats.net/v1/domains/{domain}/whois"
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
      "expires": "2019-01-30"
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

`GET https://api.emergingthreats.net/v1/{domain}/whois`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
domain | No | The domain associated with the whois record.
registrant.name | Yes | Name of the domain registrant.
registrant.email | Yes | Email address of the domain registrant.
registrant.created | Yes | Date the whois record was originally created.
registrant.updated | Yes | Date the whois record was last updated.
registrant.expires | Yes | Date the whois record will expire.
registrar.name | Yes | Name of the domain registrar.
registrar.country | Yes | Home country of the domain registrar.
registrar.website | Yes | Homepage for the domain registrar.


# IP Information

## Get IP malware-requested URLs

```shell
curl "https://api.emergingthreats.net/v1/ips/{ip}/urls"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    "/index.php?id=XXXXXXXXXXXXXXX&scn=X&inf=X&ver=XX&cnt=XXX",
    "/index.php?id=XXXXXXXXXXXXXX&scn=X&inf=X&ver=XX&cnt=XXX",
    "/index.php?id=XXXXXXXXXXXXXXXXXX&scn=X&inf=X&ver=XX&cnt=XXX"
  ]
}
```

This endpoint retrieves the most recent http requests made by malware to the specified IP.

### HTTP Request

`GET https://api.emergingthreats.net/v1/ips/{ip}/urls`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
url | No | The url string of the request with query parameter values masked.

## Get IP related malware samples

```shell
curl "https://api.emergingthreats.net/v1/ips/{ip}/samples"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": {
    "2eba8dff8d8f7a3cb2fe00b8c829a5d1": {
      "dates": "2014-02-02 - 2014-02-02"
    },
    "ca00817016fcfed6f9e81062a74343da": {
      "dates": "2014-01-05 - 2014-01-05"
    }
  }
}
```

This endpoint retrieves the most recent malware samples that communicated with the specified IP.

### HTTP Request

`GET https://api.emergingthreats.net/v1/ips/{ip}/samples`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
md5 | No | The md5sum of the malware sample.
dates | No | The dates the malware sample has been observed to have actively communicated with the specified IP.

## Get IP related domains

```shell
curl "https://api.emergingthreats.net/v1/ips/{ip}/domains"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": {
    "salemnet.vo.llnwd.net": [
      "2012-09-01 - 2014-02-15"
    ],
    "oversee.vo.llnwd.net": [
      "2012-08-17 - 2014-02-28"
    ]
  }
}
```

This endpoint retrieves the most recent domains that have been associated with the specified IP.

### HTTP Request

`GET https://api.emergingthreats.net/v1/ips/{ip}/domains`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
domain | No | 
dates | No | The dates the domain has been observed to have been associated with the specified IP.


## Get IP related IDS events

```shell
curl "https://api.emergingthreats.net/v1/ips/{ip}/events"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "ip": "208.111.161.254",
      "date": "2014-04-08",
      "source": false,
      "sid": "2008365",
      "signature": "ET TROJAN Playtech Downloader Online Gaming Checkin",
      "count": 1
    },
    {
      "ip": "208.111.161.254",
      "date": "2014-04-02",
      "source": false,
      "sid": "2008365",
      "signature": "ET TROJAN Playtech Downloader Online Gaming Checkin",
      "count": 1
    }
  ]
}
```

This endpoint retrieves the most recent IDS events that have been observed against the specified IP.

### HTTP Request

`GET https://api.emergingthreats.net/v1/ips/{ip}/events`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
ip | No | The string representation of the IP address, or "private" if it was a private IP.
date | No | The date the IDS event was observed.
source | No | Indicates whether the IP was the source of the IDS event.
sid | No | The SID that generated the IDS event.
signature | No | The signature name of the SID that generated the IDS event.
count | No | How many times this particular IDS event was observed in our sensor net for the given date.


# Malware Samples

## Get sample details

```shell
curl "https://api.emergingthreats.net/v1/samples/{md5}"
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
    "sha256": "e12012672d33cbcb22cf953ff787af250f8f5e920c565f03d4496a619c13a889"
  }
}
```

This endpoint retrieves metadata information for a single malware sample.

### HTTP Request

`GET https://api.emergingthreats.net/v1/samples/{md5}`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
submit_date | No | The date and time the malware was originally submitted to Emerging Threats; format is yyyy-MM-dd HH:mm:ss
file_type | Yes | 
file_size | Yes | The size of the binary in bytes.
sha256 | Yes | The SHA-256 hash of the binary.

## Get sample connections

```shell
curl "https://api.emergingthreats.net/v1/samples/{md5}/connections"
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

`GET https://api.emergingthreats.net/v1/samples/{md5}/connections`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
source | No | The source of the connection.
date | No | The date the connection was observed.
source_ip | No | The source IP of the traffic associated with the connection.
destination_ip | No | The destination IP of the traffic associated with the connection.
source_port | No | The source port of the traffic associated with the connection.
destination_port | No | The destination port of the traffic associated with the connection.
bytes_down | Yes | The total number of bytes downloaded via this connection.
bytes_up | Yes | The total number of bytes uploaded via this connection.
bytes_total | Yes | The total number of bytes transmitted via this connection.
packets_down | Yes | The total number of packets downloaded via this connection.
packets_up | Yes | The total number of packets uploaded via this connection.
packets_total | Yes | The total number of packets transmitted via this connection.
protocol | Yes | The communication protocol associated with this connection (e.g. tcp, udp).

## Get sample dns lookups

```shell
curl "https://api.emergingthreats.net/v1/samples/{md5}/dns"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "source": "177f3c8a2623d4efb41b0020d680be83",
      "date": "2014-04-02",
      "domain": "partirenimmobilier.fr",
      "address": "10.10.10.1",
      "record_type": "A"
    },
    {
      "source": "177f3c8a2623d4efb41b0020d680be83",
      "date": "2014-04-02",
      "domain": "www.fredianipueyrredon.com.ar",
      "address": "10.10.10.1",
      "record_type": "A"
    }
  ]
}
```

This endpoint retrieves the most recent dns lookups an individual malware sample was observed to have made.

### HTTP Request

`GET https://api.emergingthreats.net/v1/samples/{md5}/dns`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
source | No | The source of the dns lookup.
date | No | The date the lookup was observed.
domain | No | The domain whose DNS record was being queried.
answer | Yes | If the DNS response was not an A record pointing to an IP, this field will contain the DNS query response (e.g. the CNAME).
address | Yes | If the DNS response was an A record pointing to an IP, this field will contain the IP in question.
record_type | Yes | The DNS record type (e.g. A, CNAME, etc.)

## Get sample http requests

```shell
curl "https://api.emergingthreats.net/v1/samples/{md5}/http"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "source": "177f3c8a2623d4efb41b0020d680be83",
      "date": "2014-04-02",
      "domain": "vicaire.fr",
      "source_ip": "10.10.10.102",
      "destination_ip": "10.10.10.1",
      "source_port": 49367,
      "destination_port": 80,
      "method": "GET",
      "url": "/images/1/filenames.php",
      "user_agent": "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)"
    },
    {
      "source": "177f3c8a2623d4efb41b0020d680be83",
      "date": "2014-04-02",
      "domain": "www.danielalmeida.adv.br",
      "source_ip": "10.10.10.102",
      "destination_ip": "10.10.10.1",
      "source_port": 49351,
      "destination_port": 80,
      "method": "GET",
      "url": "/images/1/filenames.php",
      "user_agent": "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 6.1; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)"
    }
  ]
}
```

This endpoint retrieves the most recent http requests an individual malware sample was observed to have made.

### HTTP Request

`GET https://api.emergingthreats.net/v1/samples/{md5}/http`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
source | No | The source of the http request.
date | No | The date the request was observed.
domain | No | The domain the request was destined for.
source_ip | No | The source IP of the http request.
destination_ip | No | The IP the request was destined for.
source_port | No | The source port of the traffic associated with the request.
destination_port | No | The port the request was destined for.
method | Yes | The HTTP method used in the request.
url | Yes | The URL requested.
user_agent | Yes | The user agent string associated with the request.

## Get sample IDS events

```shell
curl "https://api.emergingthreats.net/v1/samples/{md5}/events"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "source": "177f3c8a2623d4efb41b0020d680be83",
      "date": "2014-04-02",
      "sid": 2010228,
      "source_ip": "10.10.10.102",
      "destination_ip": "10.10.10.1",
      "source_port": 49191,
      "destination_port": 80,
      "revision": "7",
      "signature_name": "ET POLICY Suspicious Microsoft Windows NT 6.1 User-Agent Detected"
    },
    {
      "source": "177f3c8a2623d4efb41b0020d680be83",
      "date": "2014-03-31",
      "sid": 2001117,
      "source_ip": "10.10.10.1",
      "destination_ip": "10.10.10.104",
      "source_port": 53,
      "destination_port": 51394,
      "revision": "6",
      "signature_name": "ET DNS Standard query response, Name Error"
    }
  ]
}
```

This endpoint retrieves the most recent IDS events an individual malware sample was observed to have triggered.

### HTTP Request

`GET https://api.emergingthreats.net/v1/samples/{md5}/events`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
source | No | The source of the event.
date | No | The date the event was observed.
sid | No | The SID associated with the event.
source_ip | No | The source IP of the traffic associated with the event.
destination_ip | No | The destination IP of the traffic associated with the event.
source_port | No | The source port of the traffic associated with the event.
destination_port | No | The destination port of the traffic associated with the event.
revision | Yes | The rule revision of the SID in question.
signature_name | Yes | The name of the signature associated with this SID.
