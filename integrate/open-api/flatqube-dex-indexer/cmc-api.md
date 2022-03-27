# CMC API

{% swagger method="get" path="" baseUrl="https://ton-swap-indexer.broxus.com/v1/cmc/dex" summary="CMC DEX pools info" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-response status="200: OK" description="Successful request" %}
```
{
    "0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2_0:c37b3fafca5bf7d3704b081fde7df54f298736ee059bf6d32fac25f5e6085bf6": {
            "base_id": "0:a519f99bb5d6d51ef958ed24d337ad75a1c770885dcd42d51d6663f9fcdacfb2",
            "base_name": "Tether",
            "base_symbol": "USDT",
            "quote_id": "0:c37b3fafca5bf7d3704b081fde7df54f298736ee059bf6d32fac25f5e6085bf6",
            "quote_name": "USD Coin",
            "quote_symbol": "USDC",
            "last_price": "1.001259244956",
            "base_volume": "2210.44204800",
            "quote_volume": "2213.22553600"
    },
    "0:0cfa60f9454b1b619938c4da6a138b1cc62da937b3f6c0506405daf2a88e0115_0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d": {
            "base_id": "0:0cfa60f9454b1b619938c4da6a138b1cc62da937b3f6c0506405daf2a88e0115",
            "base_name": "EUR-Fiat-Based",
            "base_symbol": "EUPI",
            "quote_id": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
            "quote_name": "Wrapped EVER",
            "quote_symbol": "WEVER",
            "last_price": "5.547157916853",
            "base_volume": "359.90566477",
            "quote_volume": "1996.453557649000"
    },
    ...
}
```
{% endswagger-response %}
{% endswagger %}

