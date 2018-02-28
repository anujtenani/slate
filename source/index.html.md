---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  
toc_footers:
  - <a href='https://oxybit.com/profile/api'>Sign Up for a Developer Key</a>

search: true
---

# Introduction

Welcome to OxyBit API ! You can use our API to access the entire functionality of our trading platform. From algorithmic trading to end-to-end payments for merchants, you can build it all.

We have language bindings in Shell, PHP, and Javascript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, first generate a API key at [https://oxybit.com/profile/api](https://oxybit.com/profile/api)

> For all the authenticated endpoints, pass token as request header

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "token: my-api-key"
```

```javascript

```

> Make sure to replace `my-api-key` with your API key.

You can register a new OxyBit API key at our [developer portal](http://example.com/developers).

OxyBit expects for the API key to be included in all Authenticated API requests to the server in a header that looks like the following:

`token: my-api-key`

<aside class="notice">
You must replace <code>my-api-key</code> with your personal API key.
</aside>

# Ticker
## Get Ticker

```shell
curl "https://api.oxybit.com/trade/ticker" -X GET
```

```javascript
fetch("https://api.oxybit.com/trade/ticker").then((result)=>result.json());
```
> The above command returns JSON structured like this:

```json
[
   {"<trading pair>": {
          "pair": "<pair>",
          "bidprice": "<price at which you can sell in the market>",
          "bidvol": "<total volume of bid orders>",
          "bidtotal": "<total value of the bid orders>",
          "rank": "<rank of the coin as per market cap>",
          "askprice": "<price at which you can buy from the market>",
          "askvol": "<total volume of ask orders>",
          "asktotal": "<total value of the ask orders>",
          "hi": "<highest price of last 24 hours>",
          "lo": "<lowest price of last 24 hours>",
          "open": "<market open price i.e. price 24 hours ago>",
          "last": "<price of last trade>",
          "percent": "<percentage change in price the last 24 hours>",
          "vol": "<total amount of coins that exchanged hands>"
        }
   }
 ]

```
This endpoint gets the latest ticker data.

### HTTPS Request

`GET http://api.oxubit.com/trade/ticker`

## Get Ticker (Simpler)

```shell
curl "https://api.oxybit.com/trade/ticker/simple" -X GET
```

```javascript
fetch("https://api.oxybit.com/trade/ticker/simple").then((result)=>result.json());
```
> The above command returns JSON structured like this:

```json
[
   {
      "symbol": "<pair>",
      "bidprice": "<price at which you can sell in the market>",
      "askprice": "<price at which you can buy from the market>",
    }
]

```
This endpoint gets a simpler version of ticker data

### HTTPS Request

`GET https://api.oxubit.com/trade/ticker/simple`


# Orders
## Get Order book

```shell
curl "https://api.oxybit.com/trade/orderbook/btc-inr" -X GET
```

```javascript
fetch("https://api.oxybit.com/trade/orderbook/btc-inr").then((result)=>result.json());
```
> The above command returns JSON structured like this:

```json
{
  "pair":"<pair>",
  "buy": [
      {
        "amount":"<amount>",
        "price":"<price>"
      }
  ],
  "sell":[
      {
        "amount":"<amount>",
        "price":"<price>" 
      }
  ]
}
```
This endpoint gets the order book for a particular pair

<aside class="notice">
You must replace <code>pair</code> with the desired pair. For list of pairs see /trade/ticker
</aside>

### HTTPS Request

`GET https://api.oxybit.com/trade/orderbook/<pair>`

## Get Trade History

```shell
curl "https://api.oxybit.com/trade/history/btc-inr" -X GET
```

```javascript
fetch("https://api.oxybit.com/trade/history/btc-inr").then((result)=>result.json());
```
> The above command returns JSON structured like this:

```json
{
    "pair" : "<pair>",
    "items" : [
        {
          "uuid": "<uniq id of this trade>",
          "amount": "<Amount>",
          "price": "<Price>",
          "created": "<UNIX timestamp>",
          "type": "<0 = buy, 1 = sell>"
        }
    ]
}
```
This endpoint gets the order book for a particular pair

<aside class="notice">
You must replace <code>pair</code> with the desired pair. For list of pairs see /trade/ticker
</aside>

### HTTPS Request

`GET https://api.oxybit.com/trade/history/<pair>`

## Get Your Open Orders
> Requires authorization. See Authentication

```shell
curl "https://api.oxybit.com/trade/openorders/btc-inr" -X GET -H "token:my-api-token"
```

```javascript

```
> The above command returns JSON structured like this:

```json
{
    "pair" : "<pair>",
    "items" : [
        {
          "uuid": "<uniq id of this trade>",
          "amount": "<Amount>",
          "price": "<Price>",
          "created": "<UNIX timestamp>",
          "type": "<0 = buy, 1 = sell>"
        }
    ]
}
```
This endpoint gets the your open orders for a particular pair

<aside class="notice">
You must replace <code>pair</code> with the desired pair. For list of pairs see /trade/ticker
</aside>

<aside class="notice">
You must replace <code>my-api-key</code> with your generated API key
</aside>

### HTTPS Request

`GET https://api.oxybit.com/trade/openorders/<pair>`

## Cancel Order
> Requires authorization. See Authentication

```shell
curl "https://api.oxybit.com/trade/cancelorder/" -X POST -H "token:my-api-token"  -d "uuid=<uuid>"
```

```javascript

```
> The above command returns JSON structured like this:

```json
{
    "pair" : "<pair>",
    "items" : [
        {
          "uuid": "<uniq id of this trade>",
          "amount": "<Amount>",
          "price": "<Price>",
          "created": "<UNIX timestamp>",
          "type": "<0 = buy, 1 = sell>"
        }
    ]
}
```
This endpoint cancels your open orders

<aside class="notice">
You must replace <code>uuid</code> with the order uuid. For list of uuid see your Open Orders
</aside>

<aside class="notice">
You must replace <code>my-api-key</code> with your generated API key
</aside>

### HTTPS Request

`POST https://api.oxybit.com/trade/cancelorder/`
### URL Parameters

Parameter | Description
--------- | -----------
uuid | The uuid of the order to cancel


## Place Order
> Requires authorization. See Authentication

```shell
curl "https://api.oxybit.com/trade/placeorder/" -X POST  -H "token:my-api-token" -d "type=0&amount=1&price=1&pair=btc-inr"
```
```javascript

```
> The above command returns JSON structured like this:

```json
{
    "ret" : "<the return value>",
    "error" : "<If any error was there in placing order>"
}
```
This endpoint places a new order

<aside class="notice">
You must replace <code>my-api-key</code> with your generated API key
</aside>

### HTTPS Request

`POST https://api.oxybit.com/trade/placeorder/`
### URL Parameters

Parameter | Description
--------- | -----------
type      | The type of order to place. 0 = buy order, 1 = sell order
price     | The price per unit of amount
amount    | The total amount of order
pair      | The trading pair to place order in (eg. btc-inr). For list of pairs see /trade/ticker

# Wallet
## Get Wallet Balance

```shell
curl -X GET https://api.oxybit.com/wallet -H "token:my-api-token"
```
> This returns JSON structured like

```json
  {
    "items" : [
      {
        "currency" : "inr",
        "available": "0",
        "locked": "0"
      }
    ]    
  }
```
Get balance of your wallet

<aside class="notice">
You must replace <code>my-api-key</code> with your generated API key
</aside>

### HTTPS Request

`GET https://api.oxybit.com/wallet/`

## Get Deposit Address

```shell
curl -X GET https://api.oxybit.com/wallet/depositaddress/btc -H "token:my-api-token"
```
> This returns JSON structured like

```json
{
    "address" : "<address>",
    "currency": "<currency>",
    "tag": "<in case of Stellar, Ripple, Monero>"
    
}
```
Get deposit address for that particular currency

<aside class="notice">
You must replace <code>my-api-key</code> with your generated API key
</aside>
<aside class="notice">
You must replace <code>currency</code> with the desired currency
</aside>


### HTTPS Request

`GET https://api.oxybit.com/wallet/depositaddress/<currency>`
