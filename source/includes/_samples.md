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
    "md5sum": "fa86e86e9dfb7a4571b3c3091fbf4bff",
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
md5 | Yes | The MD5 hash of the binary.
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
source_port | Yes | The source port of the traffic associated with the request.
destination_port | Yes | The port the request was destined for.
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
