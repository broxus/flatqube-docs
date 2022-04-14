# Pairs

{% swagger method="post" path="/pairs" baseUrl="https://ton-swap-indexer.broxus.com/v1" summary="Dex pairs data" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
 ...
"counter": "BRIDGE",
        "poolAddress": "0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06",
        "fee": "0.3000"
      },
      "tvl": "8955040.156573434959",
      "tvlChange": "3.26",
      "leftLocked": "22564291945792668",
      "leftPrice": "0.2323725625631798673951181204",
...
}
```
{% endswagger-response %}
{% endswagger %}

This function is used to get all Pairs data by \
\
It can be used for representing data specific to each currency in detail.

### Request parameters

Body required. Data used for Postman tests:

| Field name          | Example value                                                              | Comment                                     |
| ------------------- | -------------------------------------------------------------------------- | ------------------------------------------- |
| `currencyAddress`   | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1`       | `address of the currency for the left pair` |
| `currencyAddresses` | `0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1`       | `list of addresses`                         |
| `limit`             | `0`                                                                        | `number of pairs that should be retrieved`  |
| `offset`            | `0`                                                                        |                                             |
| `ordering`          | `tvlascending`                                                             | `order by pair’s TVL ascending/descending`  |
| `tvlAmountGe`       | `8955040.156573434959`                                                     | `highest TVL amount`                        |
| `tvlAmountLe`       | `8955043.156573434959`                                                     |  `lowest TVL amount`                        |
| `whiteListUri`      | `https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json` | `path to a white list`                      |

```
{
  "currencyAddress": "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1",
  "currencyAddresses": [
    "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1"
  ],
  "limit": 0,
  "offset": 0,
  "ordering": "tvlascending",
  "tvlAmountGe": "8955040.156573434959",
  "tvlAmountLe": "8955043.156573434959",
  "whiteListUri": "https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json"
}
```

### Response fields explanation

| Field name        | Example value | Comment                                       |
| ----------------- | ------------- | --------------------------------------------- |
| `count`           |               | number of pairs displayed on one page         |
| `offset`          |               |                                               |
| `pairs`           |               | list of pairs with following info:            |
| `fee24h`          |               | total amount of fees (in USD) in the last 24h |
| `fee7d`           |               |                                               |
| `feeAllTime`      |               |                                               |
| `leftLocked`      |               |                                               |
| `leftPrice`       |               |                                               |
| `meta`            |               |                                               |
| `base`            |               |                                               |
| `baseAddress`     |               |                                               |
| `counter`         |               |                                               |
| `counterAddress`  |               |                                               |
| `fee`             |               |                                               |
| `poolAddress`     |               |                                               |
| `rightLocked`     |               |                                               |
| `rightPrice`      |               |                                               |
| `tvl`             |               |                                               |
| `tvlChange`       |               |                                               |
| `volume24h`       |               |                                               |
| `volume7d`        |               |                                               |
| `volumeChange24h` |               |                                               |
| `totalCount`      |               |                                               |

