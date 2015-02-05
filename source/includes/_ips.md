# IP Information

## Get current IP reputation

```shell
curl "https://api.emergingthreats.net/v1/ips/{ip}/reputation"
  -H "Authorization: SECRETKEY"
  ```

```python
from urllib2 import Request, urlopen
request = Request("https://api.emergingthreats.net/v1/domains/{ip}/reputation")
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

This endpoint retrieves the current reputation scores in categories that are currently associated with the specified IP.

### HTTP Request

`GET https://api.emergingthreats.net/v1/ips/{ip}/reputation`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
category | No | The category of reputation under which this score falls.
score | No | The numerical reputation score for this category.  Scores are non-negative integers ranging from 0 to 127.


## Get IP malware-requested URLs

```shell
curl "https://api.emergingthreats.net/v1/ips/{ip}/urls"
  -H "Authorization: SECRETKEY"
```


```python
from urllib2 import Request, urlopen
request = Request("https://api.emergingthreats.net/v1/domains/{ip}/urls")
request.add_header("Authorization", "SECRETKEY")
result = urlopen(request)
print result.read()
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

```python
from urllib2 import Request, urlopen
request = Request("https://api.emergingthreats.net/v1/domains/{ip}/samples")
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
      "source": "6c885bee0b4ef2f539b26298b252212d",
      "first_seen": "2014-05-13",
      "last_seen": "2014-05-13"
    },
    {
      "source": "8449da068aec412fbec6fd48bc675396",
      "first_seen": "2014-05-03",
      "last_seen": "2014-05-03"
    }
  ]
}
```

This endpoint retrieves the most recent malware samples that communicated with the specified IP.

### HTTP Request

`GET https://api.emergingthreats.net/v1/ips/{ip}/samples`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
source | No | The md5sum of the malware sample.
first_seen | No | The date the malware sample was first seen associated to the IP.
last_seen | No | The date the malware sample was last seen associated to the IP.

## Get IP related domains

```shell
curl "https://api.emergingthreats.net/v1/ips/{ip}/domains"
  -H "Authorization: SECRETKEY"
```

```python
from urllib2 import Request, urlopen
request = Request("https://api.emergingthreats.net/v1/domains/{ip}/domains")
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
      "domain": "citi-bank.ru",
      "first_seen": "2014-02-22",
      "last_seen": "2014-04-09"
    },
    {
      "domain": "tat-neftbank.ru",
      "first_seen": "2014-04-04",
      "last_seen": "2014-04-04"
    }
  ]
}
```

This endpoint retrieves the most recent domains that have been associated with the specified IP.

### HTTP Request

`GET https://api.emergingthreats.net/v1/ips/{ip}/domains`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
domain | No |
first_seen | No | The date the domain was first seen associated to the IP.
last_seen | No | The date the domain was last seen associated to the IP.


## Get IP related IDS events

```shell
curl "https://api.emergingthreats.net/v1/ips/{ip}/events"
  -H "Authorization: SECRETKEY"
```

```python
from urllib2 import Request, urlopen
request = Request("https://api.emergingthreats.net/v1/domains/{ip}/events")
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


## Get IP geolocation info

```shell
curl "https://api.emergingthreats.net/v1/ips/{ip}/geoloc"
  -H "Authorization: SECRETKEY"
```

```python
from urllib2 import Request, urlopen
request = Request("https://api.emergingthreats.net/v1/domains/{ip}/geoloc")
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
      "ip": "216.38.198.78",
      "country": "US",
      "region": "CO",
      "city": "Henderson",
      "latitude": 39.88650131225586,
      "longitude": -104.88099670410156
    }
  ]
}
```

This endpoint retrieves geolocation info for a single IP address.

### HTTP Request

`GET https://api.emergingthreats.net/v1/ips/{ip}/geoloc`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
ip | No | The IP address specified.
country | No | The country in which the IP was last observed.
region | Yes | A two character [ISO-3166-2](http://en.wikipedia.org/wiki/ISO_3166-2) or [FIPS 10-4](http://en.wikipedia.org/wiki/FIPS_10-4) code for the state or region associated with the IP.
city | Yes | The city or town name associated with the IP.
latitude | Yes | The latitude associated with the IP.
longitude | Yes | The longitude associated with the IP.
