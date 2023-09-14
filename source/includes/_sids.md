# Signature Information

## Get Signature name

```shell
curl "https://api.emergingthreats.net/v1/sids/{sid}"
  -H "Authorization: SECRETKEY"
```

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/sids/{sid}"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
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

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/sids/{sid}/ips"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
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

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/sids/{sid}/domains"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
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

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/sids/{sid}/samples"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
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

## Get Signature Text

```shell
curl "https://api.emergingthreats.net/v1/sids/{sid}/text"
  -H "Authorization: SECRETKEY"
```

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/sids/{sid}/text"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
```

> The JSON response should look something like:

```json
{
  "success":true,
  "response":
    {
      "sid":2000005,
      "suricata_text":"alert tcp $EXTERNAL_NET any -> $HOME_NET 23 (msg:\"ET EXPLOIT Cisco Telnet Buffer Overflow\"; flow: to_server,established; content:\"|3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 61 7e 20 25 25 25 25 25 58 58|\"; threshold: type limit, track by_src, count 1, seconds 120; reference:url,www.cisco.com/warp/public/707/cisco-sn-20040326-exploits.shtml; reference:url,doc.emergingthreats.net/bin/view/Main/2000005; classtype:attempted-dos; sid:2000005; rev:7;)",
      "snort_text":"alert tcp $EXTERNAL_NET any -> $HOME_NET 23 (msg:\"ET EXPLOIT Cisco Telnet Buffer Overflow\"; flow: to_server,established; content:\"|3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 3f 61 7e 20 25 25 25 25 25 58 58|\"; detection_filter: track by_src, count 1, seconds 120; reference:url,www.cisco.com/warp/public/707/cisco-sn-20040326-exploits.shtml; reference:url,doc.emergingthreats.net/bin/view/Main/2000005; classtype:attempted-dos; sid:2000005; rev:8;)"
    }
}
```

This endpoint retrieves the most recent documentation available for the specified sid.  If you do not have access to the rule requested (i.e. the rule is for ETPro and you do not
have an ETPro subscription, this will return a 403 Forbidden.

### HTTP Request

`GET https://api.emergingthreats.net/v1/sids/{sid}/text`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
sid | No | Sid that was requested
suricata_text | Yes | Example of the rule for Suricata
snort_text | Yes | Example of rule for Snort 2.9


## Get Signature documentation

```shell
curl "https://api.emergingthreats.net/v1/sids/{sid}/documentation"
  -H "Authorization: SECRETKEY"
```

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/sids/{sid}/documentation"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
```

> The JSON response should look something like:

```json
{
  "success": true,
  "response":
    {
      "sid": 2000005,
      "summary": "This alert is triggered when an attempt is made to exploit a vulnerability in a system or application.",
      "description": "An EXPLOIT Attempt event likely occurs when an attacker has attempted to gain
      unauthorized access to an asset or service by exploiting a direct vulnerability in an application or
      operating system. A successful exploitation of an asset or service may lead to malicious code being left
      behind to facilitate remote control. Further investigation may be needed to ascertain if an attacker successfully exploited this asset or service.",
      "impact": "Compromised Server"
    }
}
```
This endpoint retrieves the most recent documentation available for the specified sid.

### HTTP Request

`GET https://api.emergingthreats.net/v1/sids/{sid}/documentation`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
sid | No | Sid that was requested
summary | No | Summary of the information this alert is trying to convey.
description | No | Detailed description of the exploit being caught.
impact | No | What kinds of systems does this impact

## Get Signature references

```shell
curl "https://api.emergingthreats.net/v1/sids/{sid}/references"
  -H "Authorization: SECRETKEY"
```


```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/sids/{sid}/references"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
```

> The JSON response should look something like:

```json
{
  "success":true,
  "response":
    [
      {
        "reference_type":"url",
        "reference_description":"HTTP URL",
        "reference_urls":
          [
            "http://doc.emergingthreats.net/bin/view/Main/2000005",
            "http://www.cisco.com/warp/public/707/cisco-sn-20040326-exploits.shtml"
          ]
      }
    ]
}
```
This endpoint retrieves lookup references for this SID.

### HTTP Request

`GET https://api.emergingthreats.net/v1/sids/{sid}/references`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
reference_type | No | The type of reference this refers to, as a key
reference_description | No | Plain text description of the reference type
reference_urls | No | List of urls to references
