# Threat Actor Information<sup>BETA</sup>

## Get Threat Actor Bio Information 

```shell
curl "https://api.emergingthreats.net/v1/actors/{threatactor}"
  -H "Authorization: SECRETKEY"
```

```python
import requests
api_key = "SECRETKEY"
url = "https://api.emergingthreats.net/v1/actors/{threatactor}"
headers = {'Authorization': f'{api_key}'}
response = requests.get(url, headers=headers)
print(response.json())
```

> The JSON response should look something like:

```json
{
    "success": true,
    "response": {
        "name": "TA453",
        "description": "**Name**\n\nTA453\n\n**Other Names**\n \nCurrent names: CharmingKitten, Phosphorus..."
    }
}
```

This endpoint retrieves the biographical information that PFPT has compiled on the threat actor listed in the rule metadata. Please follow the spelling and capitalization format found in the rule to ensure the response is valid. E.G. TA453

### HTTP Request

`GET https://api.emergingthreats.net/v1/actors/{threatactor}`

### Response Parameters

Parameter | Optional? | Description
--------- | --------- | -----------
name | No | The name of Threat actor.
description | No | The description of Threat Actor.

This will return information on threat actors.  The only variable here is the TA name which can be found on the rule’s metadata (e.g. TA453)

