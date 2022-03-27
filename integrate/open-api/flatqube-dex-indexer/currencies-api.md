# Currencies API

{% swagger method="post" path="/{currencies}" baseUrl="https://ton-swap-indexer.broxus.com/v1/currencies" summary="DEX currency info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Request succesfull" %}
```
{
  "currency": "WEVER",
  "address": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
  "price": "0.2282687283977780064244925674",
  "priceChange": "-3.71",
  "tvl": "12209750.651450054502",
  "tvlChange": "-2.45",
  "volume24h": "555590.207631653593",
  "volumeChange24h": "22.66",
  "volume7d": "3700214.440186123499",
  "fee24h": "1660.849630640965",
  "transactionsCount24h": 768
}
```
{% endswagger-response %}
{% endswagger %}

This function is used to get currency data info by token root address.\
\
It can be used for representing data specific to each currency in detail.

### Request parameters

_Currencies parameter required - represents address of a specific currency._ \
_Value used for testing is WEVER address: 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d_

### Response fields explanation <a href="#response-fields-explanation" id="response-fields-explanation"></a>

| Field name        | Example value                                                        | Comment                                                  |
| ----------------- | -------------------------------------------------------------------- | -------------------------------------------------------- |
| `currency`        | `WEVER`                                                              | currency symbol                                          |
| `address`         | `0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d` | root address of the desired currency price: price in USD |
| `priceChange`     | `-3.71`                                                              | price change in the last 24h (percentage)                |
| `tvl`             | `12209750.651450054`                                                 | total value locked (TVL in USD) of the currency          |
| `tvlChange`       | `-2.45`                                                              | TVL change in the last 24h (percentage)                  |
| `volume24h`       | `555590.207631653593`                                                | trading volume (in USD) in the last 24h                  |
| `volumeChange24h` | `22.66`                                                              | trading volume change (percentage) in the last 24h       |
| `volume7d`        | `3700214.4401861234`                                                 | trading volume (in USD) in the last 7 days               |

### Example

```java
app.post('/currencies/:currencies', (req, res) => {
        console.log(`Method params: ${req.params.currencies}`)
 
        axios({
            method: 'post',
            url: `${liveApiUrl}/currencies/${req.params.currencies}`
          })
        .then(function(response){
            res.send(response.data)
        })
        .catch(function(error){
            console.error(error)
            res.send('Error')
        })
  })
```

{% swagger method="post" path="" baseUrl="" summary="" %}
{% swagger-description %}

{% endswagger-description %}
{% endswagger %}
