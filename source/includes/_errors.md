# Errors

The IQRisk Query API uses the following error codes:

Error Code | Meaning
---------- | -------
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- The API key does not have access to the requested action
404 | Not Found -- The requested action does not exist
408 | Request Timeout -- The request took too long to complete on our side. Please reduce the amount of information you are requesting, or try again later.
500 | Internal Server Error -- We had a problem internal to our systems. Please try again later.
