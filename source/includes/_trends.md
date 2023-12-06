# Trends Information<sup>BETA</sup>

## Get Trends Information 

```shell
curl "https://api.emergingthreats.net/v1/actors/{tag-name}/{report-name}"
  -H "Authorization: SECRETKEY"
```

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/actors/{tag-name}/{report-name}"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
```

> The JSON response for cve/rolling-count should look something like:

```json
{
    "success": true,
    "timestamp": "2023-12-05-21:19:15",
    "message_id": "req212112229",
    "response": [
        {
            "tag": "CVE-2021-35394",
            "today-rank": 1,
            "seven-day-rank": 1,
            "thirty-day-rank": 2,
            "ninety-day-rank": 2
        },
        {
            "tag": "CVE-2017-9841",
            "today-rank": 2,
            "seven-day-rank": 2,
            "thirty-day-rank": 3,
            "ninety-day-rank": 3
        }
      ]
}
```
> The JSON response for cve/summaries should look something like:

```json
{
    "success": true,
    "timestamp": "2023-12-05-21:19:15",
    "message_id": "req212112229",
    "response": [
          {
            "tag": "CVE-2021-44228",
            "event-rank": 1
        }
      ]
}
```
> The JSON response for cve/activities should look something like:

```json
{
    "success": true,
    "timestamp": "2023-12-05-21:19:15",
    "message_id": "req212112229",
    "response": [
        {
            "tag": "CVE-2023-27350",
            "current-week-activity-rank": 1,
            "previous-week-activity-rank": 2
        }
      ]
}
```
This endpoint will provide the ET Intel trends in malware activity, threat actor activity, and CVE exploit trends ranked by ET Pro signature fire volume.

### HTTP Request

`GET https://api.emergingthreats.net/v1/tags/{tag-name}/{report-name}`


### Request Parameters

tag-name |   | Description
--------- | --------- | -----------
cve |  | The top ranked CVE exploit attempts observed today.
malware |  | The top ranked malware families observed today.
threat-actor |  | The top ranked threat actors observed today.

Report-name |   | Description
--------- | --------- | -----------
rolling-count |  | Provides the ranking from today, last week, 30 days ago, and 90 days ago.
summaries |  | Provides today’s signature fire volume ranking for today.
activities |  | Provides the week over week ranking based on volume.


### Response Parameters for cve/rolling-count parameter combination

Parameter | Optional? | Description
--------- | --------- | -----------
tag | No | The name/id of CVE exploit.
today-rank | No | CVE exploit ranking from today.
seven-day-rank | No | 7 day ranking for CVE exploit.
thirty-day-rank | No | 30 day ranking for CVE exploit.
ninety-day-rank | No | 90 day ranking for CVE exploit.

### Response Parameters for cve/summaries parameter combination

Parameter | Optional? | Description
--------- | --------- | -----------
tag | No | The name/id of CVE exploits.
event-rank | No | Event ranking for CVE Exploits.

### Response Parameters for cve/activities parameter combination

Parameter | Optional? | Description
--------- | --------- | -----------
tag | No | The name/id of CVE exploit.
current-week-activity-rank| No | Current week activity ranking for CVE exploit.
previous-week-activity-rank | No | Previous week activity ranking for CVE exploit.

Similarily the response parameters are same for other tag-name/report-name combinations