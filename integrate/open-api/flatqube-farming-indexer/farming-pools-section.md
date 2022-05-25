# Farming pools section

{% swagger method="post" path="/farming_pools" baseUrl="https://farming-pool-indexer.broxus.com/v1" summary="Farming pools data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
curl -X 'POST' \
  'https://farming.flatqube.io/farming_pools' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "aprGe": "52.6300",
  "aprLe": "60",
  "favoritePoolAddresses": ["0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0"],
  "isActive":true,
  "isAwaitingStart": true,
  "isLowBalance": false,
  "isWithMyFarming": true,
  "leftAddress": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
  "leftCurrency": "WEVER",
  "limit": 0,
  "offset": 0,
  "ordering": "tvlascending",
  "rightAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
  "rightCurrency": "BRIDGE",
  "rootAddresses": ["0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1", "0:9f20666ce123602fd7a995508aeaa0ece4f92133503c0dfbd609b3239f3901e2"],
  "tvlGe": "12017899.724891808371",
  "tvlLe": "12217899.724891808371",
  "userAddress": "0:102cf118b6875d201a3011d5dc17a358ee4d4333ad7e167824515171ed8f6f63",
  "whiteCurrencyAddresses": [],
  "whiteListUri": "https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json"
}'
```
{% endswagger-response %}
{% endswagger %}

This method is used to display a list of all desired farming pools, for example to show a list of farming pools that the user marked as favorite. \
List is filtered by request body params such as left and right currencies and token addresses, farming pool root address, total value locked change, pool activity, etc.

### Request parameters

Body required. Data used for postman tests:

| Field name            | Example Value                                                                                                                          | Comment                                                                   |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| aprGe                 | 52.6300                                                                                                                                | value used for filtering all pools with APR greater than or equal to this |
| aprLe                 | 60                                                                                                                                     | value used for filtering all pools with APR less than or equal to this    |
| favoritePoolAddresses | 0:39c1ba1305438e59c444267f8887d3ceb7312ab906760b8b891c865217ea8ff0                                                                     | address/addresses marked as favorite                                      |
| isActive              | true                                                                                                                                   | true if active pools should be retrieved, false if not                    |
| isAwaitingStart       | true                                                                                                                                   | true if the pools should be awaiting the start of farming, false if not   |
| isLowBalance          | false                                                                                                                                  | true if the balance should be low, false if not                           |
| isWithMyFarming       | true                                                                                                                                   | true if yes, false if no                                                  |
| leftAddress           | 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d                                                                     | root address of the left currency                                         |
| leftCurrency          | WEVER                                                                                                                                  | symbol representing left currency                                         |
| limit                 | 0                                                                                                                                      | number of pools displayed per page                                        |
| offset                | 0                                                                                                                                      | offset                                                                    |
| rightAddress          | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1                                                                     | root address of the right currency                                        |
| rightCurrency         | BRIDGE                                                                                                                                 | symbol representing right currency                                        |
| rottAddress           | 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1, 0:9f20666ce123602fd7a995508aeaa0ece4f92133503c0dfbd609b3239f3901e2 | lp address                                                                |
| tvlGe                 | 120177899                                                                                                                              | value used for filtering all pools with TVL greater than or equal to this |
| tvlLe                 | 12217899                                                                                                                               | value used for filtering all pools with TVL less than or equal to this    |
| userAddress           | 0:102cf118b6875d201a3011d5dc17a358ee4d4333ad7e167824515171ed8f6f63                                                                     | address of the user                                                       |

### Response field explanation

| Field name                | Example value | Comment |
| ------------------------- | ------------- | ------- |
| **favorite\_pools\_info** |               |         |
|                           |               |         |
|                           |               |         |

