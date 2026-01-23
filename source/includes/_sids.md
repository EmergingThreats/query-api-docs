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


## Get Signature Summary and Metadata

```shell
curl "https://api.emergingthreats.net/v1/sids/{sid}/summary"
  -H "Authorization: SECRETKEY"
```

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/sids/{sid}/summary"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
```

> Example 1: AI-Generated Description (SID 2032904)

```json
{
  "success": true,
  "response": {
    "sid": 2032904,
    "metadata": {
      "rev": "1",
      "sid": "2032904",
      "tag": "CISA_KEV, Description Generated By Proofpoint Nexus",
      "name": "[FIREEYE] Suspicious Pulse Secure HTTP Request (CVE-2021-22893) M1",
      "type": "SID",
      "ruleset": "ET",
      "category": "EXPLOIT",
      "severity": "Major",
      "classtype": "attempted-admin",
      "tls_state": null,
      "mitre_tags": [],
      "description": "This Suricata rule detects exploitation attempts targeting Pulse Secure VPN appliances, specifically CVE-2021-22893. The rule alerts when HTTP traffic contains suspicious requests to Pulse Secure's web interface paths.\n\nThe rule looks for HTTP requests directed to the home network or HTTP servers with URIs starting with \"/dana\" followed by specific paths like \"/meeting\", \"/fb/smb\", \"/namedusers\", or \"/metric\". It excludes legitimate traffic containing \"welcome.cgi\" to reduce false positives.\n\nCVE-2021-22893 is a critical authentication bypass vulnerability in Pulse Connect Secure 9.0R3/9.1R1 and higher. The vulnerability affects the Windows File Share Browser and Pulse Secure Collaboration features, allowing unauthenticated attackers to execute arbitrary code on the Pulse Connect Secure gateway. This vulnerability has been exploited in the wild.\n\nThe rule references FireEye's research and countermeasures for this vulnerability. The classification \"attempted-admin\" indicates attackers are trying to gain administrative access to the affected systems.\n\nThis is a high-severity threat as it allows unauthenticated remote code execution on VPN appliances that typically serve as critical network entry points for organizations.",
      "attack_target": "Server",
      "creation_date": "2021-05-05",
      "cve_reference": "CVE-2021-22893",
      "url_reference": "url,github.com/fireeye/pulsesecure_exploitation_countermeasures|url,www.fireeye.com/blog/threat-research/2021/04/suspected-apt-actors-leverage-bypass-techniques-pulse-secure-zero-day.html|cve,2021-22893",
      "malware_family": null,
      "affected_products": "Pulse_Secure",
      "deprecation_reason": null,
      "last_modified_date": "2021-05-05",
      "performance_impact": "Low",
      "signature_deployment": "Perimeter"
    }
  }
}
```

> Example 2: Standard Description (SID 2029740)

```json
{
  "success": true,
  "response": {
    "sid": 2029740,
    "metadata": {
      "rev": "1",
      "sid": "2029740",
      "tag": null,
      "name": "Cobalt Strike Malleable C2 (Havex APT)",
      "type": "SID",
      "ruleset": "ET",
      "category": "MALWARE",
      "severity": "Major",
      "classtype": "command-and-control",
      "tls_state": null,
      "mitre_tags": [
        {
          "mitre_tactic_id": "TA0011",
          "mitre_tactic_name": "Command_And_Control",
          "mitre_technique_id": "T1001",
          "mitre_technique_name": "Data_Obfuscation"
        }
      ],
      "description": "Also classifies as MITRE ATT&CK subtechnique .003 - Protocol Impersonation",
      "attack_target": "Client_Endpoint",
      "creation_date": "2020-03-26",
      "cve_reference": "",
      "url_reference": "url,github.com/rsmudge/Malleable-C2-Profiles/blob/master/APT/havex.profile",
      "malware_family": "Cobalt Strike",
      "affected_products": "Windows_XP/Vista/7/8/10/Server_32/64_Bit",
      "deprecation_reason": null,
      "last_modified_date": "2020-03-26",
      "performance_impact": null,
      "signature_deployment": "Perimeter"
    }
  }
}
```

This endpoint retrieves comprehensive metadata and documentation for the specified signature (SID), including AI-generated descriptions when available. The metadata includes detailed threat information, MITRE ATT&CK mappings, affected products, CVE references, and deployment recommendations. This is the primary endpoint used by the ET Intelligence UI for displaying signature information.

### HTTP Request

`GET https://api.emergingthreats.net/v1/sids/{sid}/summary`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
sid | No | Signature ID that was requested
metadata | No | JSON object containing all signature metadata and documentation

### Metadata Object Fields

Field | Optional? | Description
----- | --------- | -----------
sid | No | Signature ID as a string
rev | No | Revision number of the signature
name | No | Full name of the signature/rule
tag | Yes | Comma-separated tags indicating special properties (e.g., "CISA_KEV, Description Generated By Proofpoint Nexus")
description | No | Detailed description of the threat. May be AI-generated (indicated by tag field) or manually written by threat researchers
type | No | Type of signature (typically "SID")
ruleset | No | Ruleset name (e.g., "ET" for Emerging Threats, "ETPRO" for ET Pro)
category | No | Threat category (e.g., "EXPLOIT", "MALWARE", "TROJAN", "POLICY")
severity | No | Severity level (e.g., "Major", "Minor", "Critical")
classtype | No | Snort/Suricata classification type (e.g., "attempted-admin", "trojan-activity")
tls_state | Yes | TLS/SSL state information if applicable
mitre_tags | Yes | Array of MITRE ATT&CK framework mappings
attack_target | Yes | Primary attack target (e.g., "Server", "Client_Endpoint", "Network")
creation_date | No | Date the signature was created (YYYY-MM-DD format)
last_modified_date | No | Date the signature was last modified (YYYY-MM-DD format)
cve_reference | Yes | Related CVE identifier(s), pipe-separated if multiple
url_reference | Yes | Related reference URLs, pipe-separated
malware_family | Yes | Associated malware family name if applicable
affected_products | Yes | Products/systems affected by this threat
deprecation_reason | Yes | Reason for deprecation if signature is deprecated
performance_impact | Yes | Expected performance impact (e.g., "Low", "Medium", "High")
signature_deployment | Yes | Recommended deployment location (e.g., "Perimeter", "Internal")

### MITRE Tags Object Fields

Field | Description
----- | -----------
mitre_tactic_id | MITRE ATT&CK Tactic ID (e.g., "TA0011")
mitre_tactic_name | MITRE ATT&CK Tactic name (e.g., "Command_And_Control")
mitre_technique_id | MITRE ATT&CK Technique ID (e.g., "T1001")
mitre_technique_name | MITRE ATT&CK Technique name (e.g., "Data_Obfuscation")

### Important Notes

- **AI-Generated Descriptions**: When the `tag` field contains "Description Generated By Proofpoint Nexus" or similar text, the description has been generated or augmented using AI/LLM technology to provide more comprehensive threat context.
- **Description Length**: AI-generated descriptions are typically much longer and more detailed than manually written descriptions, often including technical details, attack vectors, impact analysis, and mitigation context.
- **MITRE ATT&CK Integration**: The `mitre_tags` array provides direct mapping to the MITRE ATT&CK framework for threat intelligence correlation.
- **Null Values**: Some fields may be `null` if the information is not applicable or not available for that particular signature.
- **ETPro Access**: If you request a signature that requires an ETPro subscription and you don't have access, this endpoint will return a 402 Payment Required status.

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
