## Introduction

Requests from apps using Basic Authentication to the Stores API are limited to 20,000 per hour, with a rolling window that updates every minute.

These limits help to manage load on our servers, ensuring that high API request volumes don’t impact on overall store performance. They also help to protect stores from deliberate or accidental denial of service as a result of the API being flooded with requests.

It is important for API client applications to be aware of these limits and handle them appropriately.

## HTTP Headers and Response Codes

Every response from the Stores API has an `**X-BC-ApiLimit-Remaining**` header, which provides information about how many requests are remaining in your client’s quota. This limit is based on total requests across the entire API.

For example, the following response header signals that your client can make up to 900 additional requests within the current window:

```
X-BC-ApiLimit-Remaining: 900

```

When the limit remaining drops to zero, additional requests result in **Bandwidth Limit Exceeded** responses with the `**509**` status code:

```
HTTP/1.1 509
Date: Wed, 04 Dec 2013 10:36:32 GMT
Content-Type: application/json
X-BC-ApiLimit-Remaining: 0

[
  {
    "status": 509,
    "message": "The requests-per-hour limit has been reached."
  }
]

```

If your client is rate limited, you won’t be able to make further requests until your quota resets.

## Working With Rate Limits

Applications that make a large volume of parallel requests or frequently poll resources to detect changes are particularly susceptible to being limited.

We recommend spreading API requests across the full one hour rolling window using the rate limit information returned to you from API responses, and minimizing the number of simultaneous API requests per store.

If you’re writing a high volume application, the following strategies will help you get the most out of the API.

### Caching

Cache everything and refer to local information in your app where possible, rather than making repetitive API calls.

### Throttling

You can limit the rate at which you send requests to the API by using a queue to keep track of outgoing calls, and throttling back calls that are going faster than your predefined limit.

For example, if you wanted to limit your outgoing API usage to four calls per second, you could use the following pattern:

*   Send first API call and record the timestamp
*   Send second, third, and fourth API calls
*   Check the timestamp before sending the fifth call
*   If less than a second has passed, wait until the second has elapsed
*   Send the next request

### Pause and Resume

Simple applications running as background tasks can use the standard `**sleep**` function in their host environment to pause between outgoing requests.
