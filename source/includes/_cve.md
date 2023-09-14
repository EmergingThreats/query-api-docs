# CVE Information <sup>BETA</sup>

## Get CVE Details

```shell
curl "https://api.emergingthreats.net/v1/cve/{CVE}"
  -H "Authorization: SECRETKEY"
```

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/cve/{CVE}"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())

```

> The JSON response should look something like:

```json
{
    "success": true,
    "timestamp": "2023-08-28-15:32:16",
    "message_id": "req877619770",
    "response": {
        "cve": "CVE-2022-30525",
        "description": "A OS command injection vulnerability in the CGI program of Zyxel USG FLEX 100(W) firmware versions 5.00 through 5.21 Patch 1, USG FLEX 200 firmware versions 5.00 through 5.21 Patch 1, USG FLEX 500 firmware versions 5.00 through 5.21 Patch 1, USG FLEX 700 firmware versions 5.00 through 5.21 Patch 1, USG FLEX 50(W) firmware versions 5.10 through 5.21 Patch 1, USG20(W)-VPN firmware versions 5.10 through 5.21 Patch 1, ATP series firmware versions 5.10 through 5.21 Patch 1, VPN series firmware versions 4.60 through 5.21 Patch 1, which could allow an attacker to modify specific files and then execute some OS commands on a vulnerable device.",
        "config_operator": "OR",
        "source_identifier": "security@zyxel.com.tw",
        "vuln_status": "Analyzed",
        "cisa_exploit_add": "2022-05-16",
        "cisa_vulnerability_name": "Zyxel Multiple Firewalls OS Command Injection Vulnerability",
        "known_exploited_vulnerabilities": true,
        "pfpt_recent_observed": true,
        "pfpt_ever_observed": true,
        "pfpt_first_observed": "2023-03-01",
        "pfpt_last_observed": "2023-08-28",
        "seven_day_trend": "increasing",
        "basemetricv3": {
            "type": "Primary",
            "source": "nvd@nist.gov",
            "cvssData": {
                "scope": "UNCHANGED",
                "version": "3.1",
                "baseScore": 9.8,
                "attackVector": "NETWORK",
                "baseSeverity": "CRITICAL",
                "vectorString": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H",
                "integrityImpact": "HIGH",
                "userInteraction": "NONE",
                "attackComplexity": "LOW",
                "availabilityImpact": "HIGH",
                "privilegesRequired": "NONE",
                "confidentialityImpact": "HIGH"
            },
            "impactScore": 5.9,
            "exploitabilityScore": 3.9
        },
        "basemetricv2": {
            "type": "Primary",
            "source": "nvd@nist.gov",
            "cvssData": {
                "version": "2.0",
                "baseScore": 10.0,
                "accessVector": "NETWORK",
                "vectorString": "AV:N/AC:L/Au:N/C:C/I:C/A:C",
                "authentication": "NONE",
                "integrityImpact": "COMPLETE",
                "accessComplexity": "LOW",
                "availabilityImpact": "COMPLETE",
                "confidentialityImpact": "COMPLETE"
            },
            "acInsufInfo": false,
            "impactScore": 10.0,
            "baseSeverity": "HIGH",
            "obtainAllPrivilege": false,
            "exploitabilityScore": 10.0,
            "obtainUserPrivilege": false,
            "obtainOtherPrivilege": false,
            "userInteractionRequired": false
        },
        "weaknesses": [
            {
                "type": "Primary",
                "source": "nvd@nist.gov",
                "description": [
                    {
                        "lang": "en",
                        "value": "CWE-78"
                    }
                ]
            },
            {
                "type": "Secondary",
                "source": "security@zyxel.com.tw",
                "description": [
                    {
                        "lang": "en",
                        "value": "CWE-78"
                    }
                ]
            }
        ],
        "publisheddate": "2022-05-12",
        "lastmodifieddate": "2022-10-19"
    }
}
```

This endpoint retrieves CVE information from NVD and Emerging Threats data. The endpoint relays whether there are known exploits, whether PFPT has observed exploit attempts, the first and last date of the observed exploit attempts and whether the exploit volume is increasing over the last week.  CVEs where we see active exploits should be considered high priority for patching if they are in your environment.


### HTTP Request

`GET https://api.emergingthreats.net/v1/cve/{cve}/`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
cve | No | description | No | The vulnerability identification number.
description | No | The description of CVE.
config_operator | No | It coveys the logical relationship of the CPE or child objects. It is part of configurations object containing the CVE applicability statements that convey which product, or products, are associated with the vulnerability according to the NVD analysis
source_identifier | No | It is an identifier for the source of the CVE.
vuln_status | No | The CVE status in the NVD portal.
cisa_exploit_add | No | The date when CVE is listed in CISA's Known Exploited Vulnerabilities (KEV) Catalog.
cisa_vulnerability_name | No | The name of the CVE vulnerability provided by CISA.
known_exploited_vulnerabilities | No | Boolean value determining if the CVE has known exploitable vulnerability.
pfpt_recent_observed | No | Boolean value determining if  CVE activity is captured by Proofpoint Systems recently.
pfpt_ever_observed | No | Boolean value determining if a CVE activity is captured by Proofpoint Systems.
pfpt_first_observed | No | Date when the CVE activity was first observed by Proofpoint Threat Intelligence Systems.
pfpt_last_observed | No | Date when the CVE activity was last observed by Proofpoint Threat Intelligence System.
seven_day_trend | No | Determines if the CVE activity trend is increasing,decreasing or nochange.
basemetricv3 | Yes | Base metrics for CVSS version 3.1.
    type | Yes | Identifies whether the organization is a primary or secondary source.
    source | Yes | Identifies the organization that provided the metrics information.
    scope | Yes | It is the ability for a vulnerability in one software component to impact resources beyond its means, or privileges.
    version | Yes | Numeric representation of the current CVSS version.
    baseScore | Yes | It reflects the severity of a vulnerability according to its intrinsic characteristics which are constant over time and assumes the reasonable worst case impact across different deployed environments.
    attackVector | Yes | This metric reflects the context by which vulnerability exploitation is possible. This metric value (and consequently the Base score) will be larger the more remote (logically, and physically) an attacker can be in order to exploit the vulnerable component.
    baseSeverity | Yes | It is the severity of a vulnerability.
    vectorString | Yes | It is a text representation of a set of CVSS metrics.
    integrityImpact | Yes | It measures the impact to integrity of a successfully exploited vulnerability. Integrity refers to the trustworthiness and veracity of information.
    userInteraction | Yes | It defines if the attacker relies on User Interaction by another person to perform actions required to exploit the vulnerability.
    attackComplexity | Yes | It describes the conditions beyond the attacker’s control that must exist in order to exploit the vulnerability. 
    availabilityImpact | Yes | It measures the impact to the availability of the impacted component resulting from a successfully exploited vulnerability.
    confidentialityImpact | Yes | It measures the impact to the confidentiality of the information resources managed by a software component due to a successfully exploited vulnerability.
    impactScore | Yes | It is the score of effects of a successfully exploited vulnerability on the component that suffers the worst outcome that is most directly and predictably associated with the attack.
    exploitabilityScore | Yes |  It is the score which reflects the ease and technical means by which the vulnerability can be exploited
basemetricv2 | No |  Base metrics for CVSS version 2.0
    type | Yes | Identifies whether the organization is a primary or secondary source.
    version | Yes | Numeric representation of the current CVSS version
    baseScore | Yes | It reflects the severity of a vulnerability according to its intrinsic characteristics which are constant over time and assumes the reasonable worst case impact across different deployed environments.
    accessVector | Yes | This metric reflects how the vulnerability is exploited.
    vectorString | Yes | It is a text representation of a set of CVSS metrics.
    authentication | Yes |  measures the number of times an attacker must authenticate to a target in order to exploit a vulnerability. This metric does not gauge the strength or complexity of the authentication process, only that an attacker is required to provide credentials before an exploit may occur.
    integrityImpact | Yes | It measures the impact to integrity of a successfully exploited vulnerability. Integrity refers to the trustworthiness and guaranteed veracity of information.
    accessComplexity | Yes | It measures whether or not extra conditions are required to exploit a vulnerability
    availabilityImpact | Yes | It measures the impact to availability of a successfully exploited vulnerability. Availability refers to the accessibility of information resources.
    confidentialityImpact | Yes | It  measures the impact on confidentiality of a successfully exploited vulnerability. Confidentiality refers to limiting information access and disclosure to only authorized users, as well as preventing access by, or disclosure to, unauthorized ones.
    weaknesses | No | Information on specific weaknesses, considered the cause of the vulnerability.
publisheddate | No | The date and time that the CVE was published to the NVD.
lastmodifieddate | No | The date and time that the CVE was last modified,.

## Get Top trending CVEs


```shell
curl "https://api.emergingthreats.net/v1/cve/top-trending"
  -H "Authorization: SECRETKEY"
```

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/cve/top-trending?limit=5"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
```

> The JSON response should look something like:

```json
{
    "success": true,
    "timestamp": "2023-08-29-20:31:23",
    "message_id": "req-2013631568",
    "response": [
        {
            "cve": "CVE-2022-22965",
            "percent_change": 4891.857142857143,
            "cvss_v3_score": "9.8",
            "description": "A Spring MVC or Spring WebFlux application running on JDK 9+ may be vulnerable to remote code execution (RCE) via data binding. The specific exploit requires the application to run on Tomcat as a WAR deployment. If the application is deployed as a Spring Boot executable jar, i.e. the default, it is not vulnerable to the exploit. However, the nature of the vulnerability is more general, and there may be other ways to exploit it."
        },
        {
            "cve": "CVE-2021-44228",
            "percent_change": 4751.073250490516,
            "cvss_v3_score": "10.0",
            "description": "Apache Log4j2 2.0-beta9 through 2.15.0 (excluding security releases 2.12.2, 2.12.3, and 2.3.1) JNDI features used in configuration, log messages, and parameters do not protect against attacker controlled LDAP and other JNDI related endpoints. An attacker who can control log messages or log message parameters can execute arbitrary code loaded from LDAP servers when message lookup substitution is enabled. From log4j 2.15.0, this behavior has been disabled by default. From version 2.16.0 (along with 2.12.2, 2.12.3, and 2.3.1), this functionality has been completely removed. Note that this vulnerability is specific to log4j-core and does not affect log4net, log4cxx, or other Apache Logging Services projects."
        },
        {
            "cve": "CVE-2023-21690",
            "percent_change": 2399.0,
            "cvss_v3_score": "9.8",
            "description": "Microsoft Protected Extensible Authentication Protocol (PEAP) Remote Code Execution Vulnerability"
        },
        {
            "cve": "CVE-2020-25078",
            "percent_change": 2251.9411764705883,
            "cvss_v3_score": "7.5",
            "description": "An issue was discovered on D-Link DCS-2530L before 1.06.01 Hotfix and DCS-2670L through 2.02 devices. The unauthenticated /config/getuser endpoint allows for remote administrator password disclosure."
        },
        {
            "cve": "CVE-2017-17215",
            "percent_change": 1999.0,
            "cvss_v3_score": "8.8",
            "description": "Huawei HG532 with some customized versions has a remote code execution vulnerability. An authenticated attacker could send malicious packets to port 37215 to launch attacks. Successful exploit could lead to the remote execution of arbitrary code."
        }
    ]
}
```

This endpoint retrieves the top 5 CVEs with highest exploit velocity over the last week.

### HTTP Request

`GET https://api.emergingthreats.net/v1/cve/top-trending?limit=5`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
cve | No | The vulnerability identification number.
percent_change | No | The weekly percentage change by event volume.
cvss_v3_score | No | CVSS version 3.X base score for a vulnerability.
description | No | The description of vulnerability.

This endpoint the highest volume exploit growth week over week targeting CVEs.  You can change the query from 5 to 10 if desired. 