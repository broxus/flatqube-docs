---
description: >-
  FlatQube offers a set of read-only APIs to facilitate obtaining data for your
  applications.
---

# Open API

{% hint style="warning" %}
**Unfinished article**\
\
This page is still in development. We are doing our best to finish it soon.\
If you are willing to help, feel free to reach us at hello@broxus.com.
{% endhint %}

The APIs below are used by FlatQube itself to facilitate user interfaces.\
Please refer to the attached Swagger schemes.

## FlatQube indexer

{% embed url="https://ton-swap-indexer.broxus.com/v1/swagger.yaml" %}

## Farming indexer

{% embed url="https://farming-pool-indexer.broxus.com/v1/swagger.yaml" %}

## Function calls

{% hint style="info" %}
The information below will allow you to familiarize yourself with the various function calls, as well as examples of their use.

All of the API call methods below are divided into 5 sections: [CMC](./#cmc), [currencies](./#currencies), [main](./#main), [pairs ](./#pairs-section)and [transactions](./#transactions-section).
{% endhint %}

## Node.js code snippets

The following examples use the libraries:

* [_Express (Node.js)_ ](https://expressjs.com/en/4x/api.html)\_\_
* [_**Axios**_](https://axios-http.com/docs/intro)
* [_**body-parser**_](https://www.npmjs.com/package/body-parser)

## **Cmc**

### /cmc/dex

This function is used to get all information about DEX pools.\
It can be used to tabulate all dex pools with their pairs and desired information about them.

`base_id`: root address of the base token in the certain dex pool\
`base_name`: full name of the base token (ie. SOON Token)\
`base_symbol`: symbol of the token (ie. SOON)\
`quote_id`: root address of the quote token in the pool\
`quote_name`: full name of the quote token (ie. Wrapped EVER)\
`quote_symbol`: symbol of the quote token (ie. WEVER)\
`last_price`: price of one base token in quote tokens (ie. 1 SOON = 12.1366 WEVER) `base_volume`: trading volume (in USD) of base token

**GET request**\
\*\*\*\*_No parameters required_

```javascript
  app.get('/cmc/dex', (req, res) => {
        axios({
            method: 'get',
            url: liveApiUrl + '/cmc/dex'
          })
        .then(function (response) {
            res.send(response.data)
        })
        .catch(function(error){
            console.error(error)
            res.send('Error')
        })
  })
```

### cmc/farming

This function helps you get farming pools information:\
\
`provider`: represents provider of the farming pool (ie. FlatQube)\
`provider_logo`: path to the provider logo provider\
`url`: url to the provider (ie. https://flatqube.io)\
`links`:\
`pools`: list of all the pools available on the provider, contains following information about each pool:\
`name`: name of the pool in format left pair/right pair (ie. WEVER/BRIDGE)\
`pair`: info about which two tokens are in pair for the given pool (ie. WEVER/BRIDGE)\
`pairLink`: URL to the farming pool where you can see all the details about that pool and start farming in it\
`logo`:\
`poolRewards`: tokens that are given as a reward for farming in that pool (ie. BRIDGE, QUBE)\
`apr`: apr (Annual Percentage Rate) for farming in that pool\
`totalStake`: TVL (Total Value Locked) in USD for the current pool

**GET request**\
\*\*\*\*No parameters required

```javascript
app.get('/cmc/farming', (req, res) => {
    axios({
        method: 'get',
        url: liveApiUrl + '/cmc/farming'
      })
    .then(function (response) {
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        res.send('Error')
    })
  })
```

## Currencies

### /currencies/{currencies}

Get currency data info by token root address.\
It can be used for representing data specific to each currency in detail.

Retrieves the following data about the certain currency:\
`currency`: currency symbol (ie. WEVER)\
`address`: root address of the desired currency price: price in USD\
`priceChange`: price change in the last 24h (percentage)\
`tvl`: total value locked (TVL in USD) of the currency\
`tvlChange`: TVL change in the last 24h (percentage)\
`volume24h`: trading volume (in USD) in the last 24h\
`volumeChange24h`: trading volume change (percentage) in the last 24h\
`volume7d`: trading volume (in USD) in the last 7 days

**POST request**\
\*\*\*\*_currencies parameter required - represents address of a specific currency. Value used for testing is WEVER address_: 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d

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

### /currencies\_usdt\_prices

Get currency prices in USD by token root address/addresses.\
It can be used anywhere where a conversion value of a certain currency should be shown in USDT.

**POST request**\
_Body required. Described in "data" field._

```javascript
 app.post('/currencies_usdt_prices', (req, res) => {
        console.log(`Request body data: ${req.body.currency_addresses}`)
 
        axios({
            method: 'post',
            url: `${liveApiUrl}/currencies_usdt_prices`,
            data: {
                currency_addresses: req.body.currency_addresses
              }
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

Data used for Postman tests:

```
{
  "currency_addresses": [
    "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1"  ]
}
```

### /currencies

Get currency data info.\
\*\*\*\*Retrieves all desired currencies based on their addresses and other requested body parameters.\
It can be used to show all currencies and their data in a list format.

Data retrieved:\
`count`: number of currencies per page\
`currencies`: list of all retrieved currencies with the following data:\
`address`: root address of the currency\
`currency`: symbol of the currency (ie. WEVER)\
`fee24h`: currency fees in the last 24h price: currency price in USD\
`priceChange`: price change in the last 24h (percentage)\
`transactionsCount24h`: number of the transactions in the last 24h\
`tvl`: TVL (total value locked) amount (in USD)\
`tvlChange`: TVL change (percentage) in the last 24h\
`volume24h`: trading volume amount (in USD) in the last 24h\
`volume7d`: trading volume amount (in USD) in the last 7 days\
`volumeChange24h`: trading volume change (percentage) in the last 24h\
`offset`: offset\
`totalCount`: number of all the currencies retrieved

**POST request**\
_Body required. Described in "data" field._

```javascript
app.post('/currencies', (req, res) => {
    console.log(`Request body data: ${req.body.currency_addresses}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies`,
        data: {
            currency_addresses: req.body.currency_addresses,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            whiteListUri: req.body.whiteListUri
          }
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

Data used for Postman tests:\
`currency_addresses`: address/addresses for which the data should be retrieved\
`limit`: number of currencies that should be retrieved\
`offset`: offset\
`ordering`: whether the currencies should be ordered by TVL ascending or descending `whiteListUri`: path to the white list

```java
{
  "currency_addresses": [
    "0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1"
  ],
  "limit": 0,
  "offset": 0,
  "ordering": "tvlascending",
  "whiteListUri": "https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json"
}
```

### /currencies/{currencies}/prices

Get currency price data info based on the timespan given.\
It can be used for graphic representation of price change over a certain period of time.

Retrieves a list of prices data each for a given timeframe (H1, D1…) in a desired period of time (from, to) for a desired currency :\
`close`: value of the currency (in USD) in the last moment of given timeframe\
`closeTimestamp`: date-time for the “close” value in UNIX format\
`high`: the highest currency price in the given timeframe\
`low`: the lowest currency price in the given timeframe open: value of the currency (in USD) in the first moment of the given timeframe\
`openTimestamp`: date-time for the “open” value in UNIX format\
`timeStamp`: date time in UNIX format, the round value of openTimestamp (ex. openTimeStamp is March 8, 2022 11:25:48 PM, timeStamp will be March 8, 2022 11:00:00 PM when converted to GMT)\
`volume`: trading volume (in USD) for the given currency between openTimeStamp and closeTimeStamp)

**POST request**\
_currencies parameter required - represents address of a specific currency. |_\
_Value used for testing is Dai Stablecoin address: 0:eb2ccad2020d9af9cec137d3146dde067039965c13a27d97293c931dae22b2b9_

Body required \*\*\*\* de\_scribed in the "data" field.\_

```javascript
 app.post('/currencies/:currencies/prices', (req, res) => {
    console.log(`Request params: ${req.params.currencies}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies/${req.params.currencies}/prices`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to
          }
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

Body parameters are required and these are the example data used for Postman tests:

`from`: date-time in UNIX format for the start of timeframe (ie. 1646741858511 or March 8, 2022 12:17:38.511 PM GMT time)\
`timeframe`: desired timeframe to retrieve prices data, could be set for hours, days, etc. (“H1”, “D1”...)\
`to`: date-time in UNIX format for the end of timeframe (ie. 1647346658513 or March 15, 2022 12:17:38.513 PM)

```javascript
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### /currencies/{currencies}/volume

Get currency volume data info. It can be used for graphic representation of trading volume (in USD) that has changed over the required period of time.\
Retrieves the following information:\
`data`: trading volume at the given moment inside of the given time span, based on the timeframe (hourly, daily etc.)\
`timestamp`: date-time of the retrieved trading volume data

**POST request**\
_currencies parameter required - represents address of a specific currency._\
_Value used for testing is Dai Stablecoin address:_ 0:eb2ccad2020d9af9cec137d3146dde067039965c13a27d97293c931dae22b2b9

Body required d\_escribed in the "data" field.\_

```javascript
app.post('/currencies/:currencies/volume', (req, res) => {
    console.log(`Request params: ${req.params.currencies}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies/${req.params.currencies}/volume`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to
          }
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

Body parameters are required and these -are the example data used for Postman tests:

`from`: date-time in UNIX format for the start of desired timespan (ie. 1646741858511 or March 8, 2022 12:17:38.511 PM GMT time)\
\_\_`timeframe`: desired timeframe to retrieve trading volume data, could be set for hours, days, etc. (“H1”, “D1”...)\
`to`: date-time in UNIX format for the end of timespan (ie. 1647346658513 or March 15, 2022 12:17:38.513 PM)

```javascript
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### /currencies/{currencies}/tvl

Get currency TVL data info. It can be used ie. for graphic representation of total value locked - TVL (in USD) change for the required period of time.\
Retrieves the following information:\
`data`: TVL for the given moment inside of the given time span, based on the timeframe (hourly, daily, etc.)\
`timestamp`: date time of the retrieved trading volume data

**POST request**\
\*\*\*\*_currencies parameter required - represents address of a specific currency._\
_Value used for testing is DAI address:_ 0:eb2ccad2020d9af9cec137d3146dde067039965c13a27d97293c931dae22b2b9\
\
_Body required \*\*\*\* described in the ‘data’ field._

```javascript
 app.post('/currencies/:currencies/tvl', (req, res) => {
    console.log(`Request params: ${req.params.currencies}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/currencies/${req.params.currencies}/tvl`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to
          }
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

Body parameters are required and these are the example data used for Postman tests:

`from`: date-time in UNIX format for the start of desired timespan (ie. 1646741858511 or March 8, 2022 12:17:38.511 PM GMT time) timeframe: desired timeframe to retrieve trading volume data, could be set for hours, days, etc. (“H1”, “D1”...)\
`to`: date-time in UNIX format for the end of timespan (ie. 1647346658513 or March 15, 2022 12:17:38.513 PM)

```
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

## Main

### /main/volume

Get main volume data info.\
Retrieves a list of all the main trading volume data for a given time span (from, to) in a certain timeframe (each hour, each day…).\
It can be used as well for a graphical representation of trading volumes over a period of time or any kind of monitoring of the trading volume.

Main trading volume data retrieved:\
`data`: trading volume amount (in USD)\
`timestamp`: timestamp when the data was retrieved

**POST request**\
_**No parameters.**_\
**\_**\_\
_\*\*\*\*Body required and described in the ‘data’ field._

```javascript
app.post('/main/volume', (req, res) => {
 
        axios({
            method: 'post',
            url: `${liveApiUrl}/main/volume`,
            data: {
                from: req.body.from,
                timeframe: req.body.timeframe,
                to: req.body.to,
            }
 
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

Data used for Postman tests:

`from`: date-time in UNIX format for the start of desired timespan (ie. 1646741858511 or March 8, 2022 12:17:38.511 PM GMT time)\
`timeframe`: desired timeframe to retrieve trading volume data, could be set for hours, days, etc. (“H1”, “D1”...)\
`to`: date-time in UNIX format for the end of timespan (ie. 1647346658513 or March 15, 2022 12:17:38.513 PM)

```javascript
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### /main/tvl

Get main TVL data info.\
Retrieves a list of all the main TVL (total value locked) data for a given time span (from, to) in a certain timeframe (each hour, each day…). It can be used as well for a graphical representation of trading volumes over a period of time or any kind of monitoring of the TVL.

Main TVL data retrieved:\
`data`: TVL amount (in USD)\
`timestamp`: time stamp when the data was retrieved\
\
**POST request**\
\*\*\*\*_No params._\
\_\_

_Body required and described in the ‘data’ field._

```javascript
app.post('/main/tvl', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/main/tvl`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to,
        }
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

Data used for Postman tests:

`from`: date-time in UNIX format for the start of desired timespan (ie. 1646741858511 or March 8, 2022 12:17:38.511 PM GMT time)\
\_\_`timeframe`: desired timeframe to retrieve trading volume data, could be set for hours, days, etc. (“H1”, “D1”...)\
`to`: date-time in UNIX format for the end of timespan (ie. 1647346658513 or March 15, 2022 12:17:38.513 PM)

```javascript
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

## Pairs

### /pairs

Get all Pairs data.\
It can be used for a table view of all the pairs and desired info about them.\
Retrieves following:\
`count`: number of pairs displayed on one page\
`offset`:\
`pairs`: list of pairs with following info:\
\- `fee24h`: total amount of fees (in USD) in the last 24h\
\- `fee7d`: total amount of fees (in USD) in the last 7 days\
\- `feeAllTime`: total amount of fees (in USD) ever\
\- `leftLocked`: tvl of the left pair (token) in USD\
\- `leftPrice`: price (in USD) of the left pair\
\- `meta`: object containing following data:\
\-- `base`: left token name (ie. WEVER)\
\-- `baseAddress`: root address of the left token\
\`\`-- `counter`: right token name (ie. BRIDGE)\
\-- `counterAddress`: root address of the right token\
\-- `fee`: fees for trading between left and right token\
\-- `poolAddress`: address of the pool of left and right pair\
\- `rightLocked`: TVL of the right pair (token) in USD\
\- `rightPrice`: price (in USD) of the left pair TVL: TVL in the pair’s pool\
\- `tvlChange`: TVL change (percentage) in the pool for the last 24h\
\- `volume24h`: trading volume of the pair in the last 24h (in USD)\
\- `volume7d`: trading volume of the pair in the last 7 days (in USD)\
\- `volumeChange24h`: trading volume change (percentage) in the last 24h\
`totalCount`: total number of pairs that satisfies search parameters

**POST request**\
\*\*\*\*_Body required. Described in the "data" field._

```javascript
app.post('/pairs', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs`,
        data: {
            currencyAddress: req.body.currencyAddress,
            currency_addresses: req.body.currency_addresses,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            tvlAmountGe: req.body.tvlAmountGe,
            tvlAmountLe: req.body.tvlAmountLe,
            whiteListUri: req.body.whiteListUri
          }
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

Data used for Postman tests:\
`currencyAddress`: address of the currency for the left pair\
`currencyAddresses`: list of addresses limit: number of pairs that should be retrieved\
`offset`: offset ordering: order by pair’s TVL ascending/descending\
`tvlAmountGe`: highest TVL amount\
`tvlAmountLe`: lowest TVL amount\
`whiteListUri`: path to a white list

```javascript
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

### **/pairs/address/{address}**

Get pair data info by liquidity pool address.\
\*\*\*\*It can be used for presenting a pair with all the details about it in the desired pool.\
Returns the following data:\
`meta`: object containing the following data:\
\- `base`: left token name (ie. WEVER)\
\- `baseAddress`: root address of the left token\
\- `counter`: right token name (ie. BRIDGE)\
\- `counterAddress`: root address of the right token fee: fees for trading between left and right token\
\- `poolAddress`: address of the pool containing left and right pair\
`tvl`: TVL in the pair’s pool\
`tvlChange`: TVL change (percentage) in the pool for the last 24h\
`leftLocked`: TVL of the left pair (token) in USD\
`leftPrice`: price (in USD) of the left pair\
`rightLocked`: TVL of the right pair (token) in USD\
`rightPrice`: price (in USD) of the left pair\
`volume24h`: trading volume of the pair in the last 24h (in USD)\
`volumeChange24h`: trading volume change (percentage) in the last 24h\
`volume7d`: trading volume of the pair in the last 7 days (in USD)\
`fee24h`: total amount of fees (in USD) in the last 24h\
`fee7d`: total amount of fees (in USD) in the last 7 days\
`feeAllTime`: total amount of fees (in USD) ever

**POST request**\
\*\*\*\*_Address parameter required - represents the pool address of a specific pair._\
\_\_

_Value used for testing is pool WEVER/BRIDGE address: 0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06_

```javascript
app.post('/pairs/address/:address', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/address/${req.params.address}`
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

### /pairs/cross\_pairs

Get cross pairs data.\
It can be used anywhere where certain details about one currency and how it affects the other one in the pair and vice versa are needed.\
Returns a list of pairs based on the given "from" currency address and "to" currency address/addresses along with some other data in the following form:\
`pairs`: a list of pairs based on the given addresses including details of the pairs:\
\- `meta`: object containing the following data:\
\-- `base`: left token name (ie. WEVER)\
\-- `baseAddress`: root address of the left token\
\-- `counter`: right token name (ie. BRIDGE)\
\-- `counterAddress`: root address of the right token\
\-- `fee`: fees for trading between left and right token\
\-- `poolAddress`: address of the pool containing left and right pair\
\- `tvl`: TVL in the pair’s pool\
\- `tvlChange`: TVL change (percentage) in the pool for the last 24h\
\- `leftLocked`**:** TVL of the left pair (token) in USD\
\- `leftPrice`: price (in USD) of the left pair\
\- `rightLocked`: TVL of the right pair (token) in USD\
\- `rightPrice`: price (in USD) of the left pair\
\- `volume24h`: trading volume of the pair in the last 24h (in USD)\
\- `volumeChange24h`: trading volume change (percentage) in the last 24h\
\- `volume7d`: trading volume of the pair in the last 7 days (in USD)\
\- `fee24h`: total amount of fees (in USD) in the last 24h\
\- `fee7d`: total amount of fees (in USD) in the last 7 days\
\- `feeAllTime`: total amount of fees (in USD) ever\
`offset`: offset\
`count`: number of pairs to display per page\
`totalCount`: total number of pairs retrieved\
\
**POST request**\
_Body required. Described in the "data" field._

```javascript
app.post('/pairs/cross_pairs', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/cross_pairs`,
        data: {
            fromCurrencyAddress: req.body.fromCurrencyAddress,
            toCurrencyAddresses: req.body.toCurrencyAddresses
        }
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

Data used for Postman tests:\
`fromCurrencyAddress`: currency address to retrieve cross pairs\
`toCurrencyAddresses`: currency address/addresses we use to check whether it is a pair with another currency in the fromCurrencyAddress parameter

```javascript
{
  "fromCurrencyAddress": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
  "toCurrencyAddresses": ["0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1"
  ]
}
```

### /pairs/left/{left}/right/{right}

Get pair data info by token root addresses.\
It can be used anywhere where details about the pairs are used and should be retrieved using their root addresses.\
Retrieves an object with the following data:\
`meta`: object containing the following data:\
\- `base`: left token name (ie. WEVER)\
\- `baseAddress`: root address of the left token\
\- `counter`: right token name (ie. BRIDGE)\
\- `counterAddress`: root address of the right token\
\- `fee`: fees for trading between left and right token\
\- `poolAddress`: address of the pool containing left and right pair\
`tvl`: TVL in the pair’s pool\
`tvlChange`: TVL change (percentage) in the pool for the last 24h\
`leftLocked`: TVL of the left pair (token) in USD\
`leftPrice`: price (in USD) of the left pair \
`rightLocked`: TVL of the right pair (token) in USD\
`rightPrice`: price (in USD) of the left pair\
`volume24h`: trading volume of the pair in the last 24h (in USD)\
`volumeChange24h`: trading volume change (percentage) in the last 24h\
`volume7d`: trading volume of the pair in the last 7 days (in USD)\
`fee24h`: total amount of fees (in USD) in the last 24h\
`fee7d`: total amount of fees (in USD) in the last 7 days\
`feeAllTime`: total amount of fees (in USD) ever

**POST request**\
\*\*\*\*\_left parameter and right parameter required - represents address of a specific currency.\_\
_Value used for testing are WEVER and BRIDGE addresses (respectively) :_\
_left = 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d_\
_right = 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1_

```javascript
 app.post('/pairs/left/:left/right/:right', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/left/${req.params.left}/right/${req.params.right}`
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

### /pairs/left/{left}/right/{right}/ohlcv

Get ohlcv pair data info by token root addresses.\
\_\_It can be used for graphic representation of price change of the right pair compared to the value of the left pair over a certain period of time (ie. 1 WEVER = 0.02245627 BRIDGE).\
Retrieves a list of price data each for a given timeframe (H1, D1…) in a desired period of time (from, to) for a right pair:\
`close`: value of the currency (in USD) in the last moment of a given timeframe\
`closeTimestamp`: date-time for the “close” value in UNIX format\
`high`: the highest currency price in the given timeframe\
`low`: the lowest currency price in the given timeframe\
`open`: value of the currency (in USD) in the first moment of the given timeframe\
`openTimestamp`: date-time for the “open” value in UNIX format\
`timeStamp`: date time in UNIX format, the round value of openTimestamp (ex. openTimeStamp is March 8, 2022 11:25:48 PM, timeStamp will be March 8, 2022 11:00:00 PM when converted to GMT)\
`volume`: trading volume (in USD) for the given currency between openTimeStamp and closeTimeStamp)

**POST request**\
\*\*\*\*_left parameter required - represents the address of a specific currency. Value used for testing is WEVER address: 0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d_\
\_\_\
_right parameter required - represents the address of a specific currency. Value used for testing is BRIDGE address: 0:f2679d80b682974e065e03bf42bbee285ce7c587eb153b41d761ebfd954c45e1_\
\_\_\
_Body required. Described in the "data" field._

```javascript
 app.post('/pairs/left/:left/right/:right/ohlcv', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/left/${req.params.left}/right/${req.params.right}/ohlcv`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to
        }
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

Data used for Postman tests:\
\_\_`from`: date-time in UNIX format for the start of timeframe (ie. 1646741858511 or March 8, 2022 12:17:38.511 PM GMT time)\
`timeframe`: desired timeframe to retrieve prices data, could be set for hours, days, etc. (“H1”, “D1”...)\
`to`: date-time in UNIX format for the end of timeframe (ie. 1647346658513 or March 15, 2022 12:17:38.513 PM)

```javascript
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### /pairs/address/{address}/ohlcv

Get ohlcv pair data info by liquidity pool address.\
It can be used for graphic representation of price change of the right pair compared to the value of the left pair over a certain period of time (ie. 1 WEVER = 0.02245627 BRIDGE).\
Retrieves a list of price data each for a given timeframe (H1, D1…) in a desired period of time (from, to) for a right pair:\
`close`: value of the currency (in USD) in the last moment of a given timeframe\
`closeTimestamp`: date-time for the “close” value in UNIX format\
`high`: the highest currency price in the given timeframe\
`low`: the lowest currency price in the given timeframe\
`open`: value of the currency (in USD) in the first moment of the given timeframe\
`openTimestamp`: date-time for the “open” value in UNIX format\
`timeStamp`: date time in UNIX format, the round value of openTimestamp (ex. openTimeStamp is March 8, 2022 11:25:48 PM, timeStamp will be March 8, 2022 11:00:00 PM when converted to GMT)\
`volume`: trading volume (in USD) for the given currency between openTimeStamp and closeTimeStamp)\
\
**POST request**\
_address parameter required - represents the pool address of a specific pair. Value used for testing is pool WEVER/BRIDGE address: 0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06_\
\_\_\
_Body required. Described in the "data" field._

```javascript
app.post('/pairs/address/:address/ohlcv', (req, res) => {
    console.log(`Request params: ${req.params.address}`)
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/address/${req.params.address}/ohlcv`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to
          }
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

Data used for Postman tests:\
`from`: date-time in UNIX format for the start of timeframe (ie. 1646741858511 or March 8, 2022 12:17:38.511 PM GMT time)\
`timeframe`: desired timeframe to retrieve prices data, could be set for hours, days, etc. (“H1”, “D1”...)\
`to`: date-time in UNIX format for the end of timeframe (ie. 1647346658513 or March 15, 2022 12:17:38.513 PM)

```javascript
{
  "from": 1646741858511,
  "timeframe": "H1",
  "to": 1647346658513
}
```

### /pairs/address/{address}/tvl

Get pair TVL data info using the liquidity pool address.\
It can be used for graphic representation of trading volume changes in the pair’s pool over a certain period of time.\
Retrieves a list of trading volume data each for a given timeframe (H1, D1…) in a desired period of time (from, to):\
`data`: trading volume for the given moment inside of the given time span, based on the timeframe (hourly, daily etc.)\
`timestamp`: date-time of the retrieved trading volume data

**POST request**\
\*\*\*\*_address parameter required - represents the pool address of a specific pair._\
\_\_\
_Value used for testing is pool WEVER/BRIDGE address: 0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06_

Body required. Described in the ‘data’ field.

```javascript
  app.post('/pairs/address/:address/tvl', (req, res) => {
 
    axios({
        method: 'post',
        url: `${liveApiUrl}/pairs/address/${req.params.address}/tvl`,
        data: {
            from: req.body.from,
            timeframe: req.body.timeframe,
            to: req.body.to
        }
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

Data used for Postman tests:\
\_\_`from`: date-time in UNIX format for the start of timeframe (ie. 1646741858511 or March 8, 2022 12:17:38.511 PM GMT time)\
`timeframe`: desired timeframe to retrieve prices data, could be set for hours, days, etc. (“H1”, “D1”...)\
`to`: date-time in UNIX format for the end of timeframe (ie. 1647346658513 or March 15, 2022 12:17:38.513 PM)

## Transactions

### /transactions

Get Transaction data of a certain user filtered by required parameters.\
It can be used anywhere where a list of transactions should be shown and filtered using body parameters.

Retrieves the following data:\
`count`: amount of transactions shown per page\
`offset`: offset\
`totalCount`: number of all transactions required transactions: retrieves list of transactions with following details:\
`createdAt`: date-time in UNIX format of transaction formation\
`eventType`: type of transaction (swap, add, remove)\
`fee`: transaction fee\
`feeCurrency`: currency of the transaction fee\
`left`: left pair currency\
`leftAddress`: left pair root address\
`leftValue`: left pair value\
`messageHash`: hash code of the transaction message\
`poolAddress`: address of the pair’s pool right: right pair currency\
`rightAddress`: right pair root address\
`rightValue`: right pair value\
`timestampBlock`: date-time of block formation `t`\
`ransactionHash`: hash of the transaction\
`tv`: total value in transaction (in USD)\
`userAddress`: address of the user that created the transaction

**POST reques**\
Body required. Described in "data" field.

```javascript
app.post('/transactions', (req, res) => {
    axios({
        method: 'post',
        url: `${liveApiUrl}/transactions`,
        data: {
            createdAtGe: req.body.createdAtGe,
            createdAtLe: req.body.createdAtLe,
            currencyAddress: req.body.currencyAddress,
            currencyAddresses: req.body.currencyAddresses,
            eventType: req.body.eventType,
            leftAmountGe: req.body.leftAmountGe,
            leftAmountLe: req.body.leftAmountLe,
            limit: req.body.limit,
            offset: req.body.offset,
            ordering: req.body.ordering,
            poolAddress: req.body.poolAddress,
            rightAmountGe: req.body.rightAmountGe,
            rightAmountLe: req.body.rightAmountLe,
            timestampBlockGe: req.body.timestampBlockGe,
            timestampBlockLe: req.body.timestampBlockLe,
            tvGe: req.body.tvGe,
            tvLe: req.body.tvLe,
            userAddress: req.body.userAddress,
            whiteListUri: req.body.whiteListUri,
          }
        })
    .then(function(response){
        res.send(response.data)
    })
    .catch(function(error){
        console.error(error)
        javares.send('Error') }) })
```

Data used for Postman tests:\
`createdAtGe`: date-time in UNIX format to filter all transaction that were created after or during that date time\
`createdAtLe`: date-time in UNIX format to filter all transactions that were created before or during that date-time\
`currencyAddress`: root address of the left currency in transaction pair\
`currencyAddresses`: root address/addresses of a right currency in transaction pair\
`eventType`: type of the transaction (swap, add, remove)\
`leftAmountGe`: amounts that are greater or equal to the given value of the left transaction pair\
`leftAmountLe`: amounts that are less or equal to the given value of the left transaction pair\
`limit`: amount limitation\
`offset`: offset ordering: order transactions by time ascending or descending\
`poolAddress`: address of the pair’s pool\
`rightAmountGe`: amounts that are greater or equal to the given value of the right transaction pair `rightAmountLe`: amounts that are less or equal to the given value of the right transaction pair `timestampBlockGe`: filter timestamp of the blocks that are greater or equal to this value `timestampBlockLe`: filter timestamp of the blocks that are less or equal to this value tvGe: filter transactions with total value greater than or equal to this value\
`tvLe`: filter transactions with total value less than or equal to this value\
`userAddress`: address of the user initiating transactions\
`whiteListUri`: path to a white list

```javascript
{
  "createdAtGe": 0,
  "createdAtLe": 0,
  "currencyAddress": "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d",
  "currencyAddresses": [
    "0:a49cd4e158a9a15555e624759e2e4e766d22600b7800d891e46f9291f044a93d"
  ],
  "eventType": [
    "swaplefttoright"
  ],
  "leftAmountGe": "0.194319663088308553962886430",
  "leftAmountLe": "1.194319663088308553962886435",
  "limit": 0,
  "offset": 0,
  "ordering": "blocktimeascending",
  "poolAddress": "0:83b88abbcd562c8d8dc4cab30ec1ded86a4ded99000ca02425715e5cec754f06",
  "rightAmountGe": "7.029870729776",
  "rightAmountLe": "9.029870729776",
  "timestampBlockGe": 0,
  "timestampBlockLe": 0,
  "tvGe": "8955040.156573434959",
  "tvLe": "8955043.156573434959",
  "userAddress": "0:3aeefed73a08979d5f7d489e7fe06f0d20a433e27f81b70a4e2e0d7f3968ede8",
  "whiteListUri": "https://raw.githubusercontent.com/broxus/ton-assets/master/manifest.json"
}
```
