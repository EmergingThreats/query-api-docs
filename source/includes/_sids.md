# Signature Information

## Get Signature name

```shell
curl "https://api.emergingthreats.net/v1/sids/{sid}"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": {
    "sid": 2007771,
    "sig_name": "ET TROJAN Pushdo Update URL Detected"
  }
  
}
```

### HTTP Request

`GET https://api.emergingthreats.net/v1/sids/{sid}`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
sid | no | Signature id that reflects request
sig_name | no | Name of the signature requested

This endpoint retrieves the signature name for a particular Signature (SID).

## Get related IP addresses

```shell
curl "https://api.emergingthreats.net/v1/sids/{sid}/ips"
  -H "Authorization: SECRETKEY"
```

### Request Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
sortBy | Yes | Valid values: "ip" and "last_seen", controls the field results are ordered by. Default is "last_seen" if no value or invalid value provided
sortDirection | Yes | Valid values of "ASC" and "DESC", descending is the default if no value provided, or invalid value

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "long_ip": 16909060,
      "ip": "1.2.3.4",
      "first_seen": "2012-04-01",
      "last_seen": "2014-02-05"
    },
    {
      "long_ip": 16909061,
      "ip": "1.2.3.5",
      "first_seen": "2013-12-22",
      "last_seen": "2014-08-17"
    }
  ]
}
```

### HTTP Request

`GET https://api.emergingthreats.net/v1/sids/{sid}/ips`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
long_ip | no | Long number representation of an IP address
ip | no | Dotted notation representation of an IP address
first_seen | no | Date the IP was first observed for this SID
last_seen | no | Date the IP was last observed for this SID

This endpoint retrieves the IPs related to a particular Signature (SID).

## Get domain SID 

```shell
curl "https://api.emergingthreats.net/v1/sids/{sid}/domains"
  -H "Authorization: SECRETKEY"
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response": [
    {
      "domain": "wr.example.com",
      "first_seen": "2012-04-01",
      "last_seen": "2014-02-05"
    },
    {
      "domain": "cc.example.com",
      "first_seen": "2013-12-22",
      "last_seen": "2014-08-17"
    }
  ]
}
```

This endpoint retrieves the Domains related to a particular Signature (SID).

### HTTP Request

`GET https://api.emergingthreats.net/v1/sids/{sid}/domains`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
domain | no | Domain name
first_seen | no | Date the IP was first observed for this SID
last_seen | no | Date the IP was last observed for this SID

## Get sid related malware samples

```shell
curl "https://api.emergingthreats.net/v1/sids/{sid}/samples"
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

This endpoint retrieves the most recent malware samples that communicated with the specified sid.

### HTTP Request

`GET https://api.emergingthreats.net/v1/sids/{sid}/samples`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
source | No | The md5sum of the malware sample.
first_seen | No | The date the malware sample was first seen associated to the SID.
last_seen | No | The date the malware sample was last seen associated to the SID.

