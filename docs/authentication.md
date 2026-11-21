---
title: Authentication
sidebar_position: 3
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Authentication

Every request to the Document API must include your API key. Requests without a valid key are rejected with a `401` status.

## Send the key with each request

Send your key in the `X-API-Key` header:

<Tabs>
  <TabItem value="curl" label="cURL" default>

```bash
curl -X GET https://api.example.com/v1/documents/doc_12345 \
  -H "X-API-Key: YOUR_API_KEY"
```

  </TabItem>
  <TabItem value="python" label="Python">

```python
import requests

response = requests.get(
    "https://api.example.com/v1/documents/doc_12345",
    headers={"X-API-Key": "YOUR_API_KEY"},
)
print(response.status_code)
```

  </TabItem>
  <TabItem value="javascript" label="JavaScript">

```javascript
const response = await fetch(
  "https://api.example.com/v1/documents/doc_12345",
  { headers: { "X-API-Key": "YOUR_API_KEY" } }
);
console.log(response.status);
```

  </TabItem>
</Tabs>

:::warning
Keep your API key secret. Never put it in public code or a shared repository.
:::