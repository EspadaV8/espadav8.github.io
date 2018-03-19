---
title: 'Redirecting in AWS Python Lambda function'
date: 2017-08-07 00:00:00 
tags: 
layout: post
---
I couldn't find a simple example of how to get a redirect when using Python for Lambda functions (all the examples I could find were for NodeJS). Below is what I ended up finding and it worked just as expected for myself.

```python
try:
    #your really good code

    return {
        "statusCode": 302,
        "headers": {
            "Location": "https://example.com/#success"
        }
    }
except:
    return {
        "statusCode": 302,
        "headers": {
            "Location": "https://example.com/#error"
        }
    }
```
