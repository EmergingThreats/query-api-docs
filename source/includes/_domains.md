# Domain Information

## Get current domain reputation

```shell
curl "https://api.emergingthreats.net/v1/domains/{domain}/reputation"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "category": "DynDNS",
      "score": 120
    },
    {
      "category": "CnC",
      "score": 100
    },
    {
      "category": "SpywareCnC",
      "score": 95
    }
  ]
}
```

This endpoint retrieves the current reputation scores in categories that are currently associated with the specified domain.

### HTTP Request

`GET https://api.emergingthreats.net/v1/domains/{domain}/reputation`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
category | No | The category of reputation under which this score falls.
score | No | The numerical reputation score for this category.  Scores are non-negative integers ranging from 0 to 127.


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
  "response": [
    {
      "ip": "213.219.245.212",
      "first_seen": "2011-12-04",
      "last_seen": "2012-02-27"
    },
    {
      "ip": "78.109.30.160",
      "first_seen": "2014-02-22",
      "last_seen": "2014-04-09"
    }
  ]
}
```

This endpoint retrieves the most recent IPs that have been associated with the specified domain.

### HTTP Request

`GET https://api.emergingthreats.net/v1/domains/{domain}/ips`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
ip | No | 
first_seen | No | The date the IP was first seen associated to the domain.
last_seen | No | The date the IP was last seen associated to the domain.

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

`GET https://api.emergingthreats.net/v1/domains/{domain}/whois`

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


## Get domain geolocation info

```shell
curl "https://api.emergingthreats.net/v1/domains/{domain}/geoloc"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "ip": "74.117.114.119",
      "country": "KY"
    },
    {
      "ip": "8.5.1.37",
      "country": "US",
      "region": "CA",
      "city": "Costa Mesa"
    }
  ]
}
```

This endpoint retrieves geolication info for a single domain.

### HTTP Request

`GET https://api.emergingthreats.net/v1/domains/{domain}/geoloc`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
ip | No | An IP associated with the specified domain.
country | No | The country in which the IP was last observed.
region | Yes | A two character [ISO-3166-2](http://en.wikipedia.org/wiki/ISO_3166-2) or [FIPS 10-4](http://en.wikipedia.org/wiki/FIPS_10-4) code for the state or region associated with the IP.
city | Yes | The city or town name associated with the IP.
