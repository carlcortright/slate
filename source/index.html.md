---
title: Paradex API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - curl
  - Ruby
  - Python
  - Javascript

toc_footers:
  - <a href='https://paradex.io/developers' class='btn btn-api' target='_blank'>Get an API key</a>
  - <h4>Additional Resources</h4>
  - <a href='mailto:contact@paradex.io'>Contact us</a>
  - <a href='mailto:contact@paradex.io'>Our Github</a>
  - <a href='mailto:contact@paradex.io'>0x Project Wiki</a>
  - <a href='mailto:contact@paradex.io'>0x Tracker</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Paradex API! The Paradex API is a powerful toolset used to interact with Paradex over http or websocket. 

It allows you to submit trades, view orders, view the orderbook for different markets and more. It's an ideal tool for automatically trading tokens directly from your wallet, making it easy for both beginners and experts to get started trading tokens.

# Authentication

The Paradex API has four levels of authentication, public access, basic access, account access, and private key access. Most of the time you will be working with basic access and account access as these protect most of the endpoints. 

### Basic Access

```shell
curl "http://api.paradex.io/v2/nonce"
  -H "HTTP_API_KEY: <your-api-key>"
```

Basic access is used to any non-account endpoint. To query these endpoints you must include the `HTTP_API_KEY` header on your request that includes an API key generated for your account. Information about generating API keys can be found our our [API key page](https://paradex.io/developers). 

### Account Access

```
 # TODO: Curl request that get's secret
```

Account access is required for any action that changes or queries the state of your account. We do this to add an extra layer of security to keep your data and trades safe. In order to access endpoints protected by basic access you must first request a secret from the generate secret endpoint. This secret is used to sign any data sent to the Paradex API to verify you are the sender. 

```
# TODO: Example account access request signature
```

Once you have your secret key you can use it to authorize requests to account access endpoints. This is done by signing a string containing the current nonce and including that signature in the request under the header `paradex_request_sig` along with the `paradex_request_nonce` header so the api knows which nonce was signed. These signatures are the same as ethereum personal signatures in web3 so hopefully no extra imports are necessary in your code. 

# Websocket API

```json
// Example WS Request
{
    'version': '2.0'
    'type': 'request', 
    'target': 'endpoint', 
    'method': 'GET', 
    'params': {},
    'message_id': 1, 
}

// Example WS Response
{
    'message_id': 1, 
    'version': '2.0',
    'status_code': '200',
    'content': {//Same as HTTP},
}
```

Our websocket API is a powerful way to trade in real-time. It offers all the same endpoints as HTTP over a secure websocket connection, allowing traders to connect once and send as many requests as they need. Websockets follow the same standards of security as the HTTP API. A websocket request is a HTTP request parameters encoded in JSON. 

Security for the websocket API is the same as the regular HTTP API, the only difference is how authentication requests are sent. 

```
TODO: Document security for WS
```

# Endpoints


## Get Nonce

```
curl "http://api.paradex.io/v2/nonce"
  -H "HTTP_API_KEY: <your-api-key>"
```


```json
{
	'version': '2.0'
	'type': 'request', 
	'target': 'nonce', 
	'method': 'GET', 
	'id': 1, 
}
```

<b>Access Level:</b> Basic Access

Gets the current nonce associated with the API key. Used for debugging nonce-related issues.

<aside class="notice">
The recommended nonce is a unix timestamp at the current moment the request is sent. 
</aside>

### HTTP Request 

`GET http://api.paradex.io/v2/nonce`

### Query Parameters

None

### Returns

<pre class="center-column-code">
{
  'nonce': your-nonce
}
</pre>

## Get Order Expiration Times

```
curl "http://api.paradex.io/v2/expirations"
  -H "HTTP_API_KEY: <your-api-key>"
```


```json
{
	'version': '2.0'
	'type': 'request', 
	'target': 'expirations', 
	'method': 'GET', 
	'id': 1, 
}
```

<b>Access Level:</b> Basic Access

Gets the order expiration times min and max.

### HTTP Request 

`GET http://api.paradex.io/v2/expirations` 

### Query Parameters

None

### Returns


<pre class="center-column-code">
{
  'minExpirationMinutes': min-expiration,
  'maxExpirationMinutes': max-expiration
}
</pre>

## Get Tokens

```
curl "http://api.paradex.io/v2/tokens"
  -H "HTTP_API_KEY: <your-api-key>"
```


```json
{
	'version': '2.0'
	'type': 'request', 
	'target': 'tokens', 
	'method': 'GET', 
	'id': 1, 
}
```

<b>Access Level:</b> Basic Access

Get all of the tokens listed on paradex. Returns a list of objects with the name symbol and address of each token

### HTTP Request 

`GET http://api.paradex.io/v2/tokens` 

### Query Parameters

None

### Returns

<pre class="center-column-code">
[
  {
    name: 'Wrapped Ether',
    symbol: 'WETH',
    address: '0xd0a1e359811322d97991e03f863a0c30c2cf029c'
  },
  ...
]
</pre>

## Get Markets

```
curl "http://api.paradex.io/v2/markets"
  -H "HTTP_API_KEY: <your-api-key>"
```


```json
{
	'version': '2.0'
	'type': 'request', 
	'target': 'markets', 
	'method': 'GET', 
	'id': 1, 
}
```

<b>Access Level:</b> Basic Access

Get all of the markets listed on paradex. Returns a list of markets and their key parameters.

### HTTP Request 

`GET http://api.paradex.io/v2/markets` 

### Query Parameters

None

### Returns

<pre class="center-column-code">
[
  {
    id: '1',
    symbol: 'ZRX/WETH',
    baseToken: 'ZRX',
    quoteToken: 'WETH',
    minOrderSize: '0.001',
    maxOrderSize: '10000',
    priceMaxDecimals: 5,
    amountMaxDecimals: 6
  },
  ...
]
</pre>

## Get OHLCV

```
curl "http://api.paradex.io/v2/ohlcv?market=weth-zrx&period=1d&amount=100"
  -H "HTTP_API_KEY: <your-api-key>"
```


```json
{
	'version': '2.0'
	'type': 'request', 
	'target': 'ohlcv', 
	'method': 'GET', 
	'id': 1, 
    'params': [
      'market': 'weth-zrx',
      'period': '1d',
      'amount': 100
    ]

}
```

<b>Access Level:</b> Basic Access

Get open, high, low, close, and volume data for a market. 

### HTTP Request 

`GET http://api.paradex.io/v2/ohlcv` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market
period  | '1m' '5m' '15m' '1h' '6h' '1d' | time period to fetch ohlcv data
amount  | int | how many candles to be returned

### Returns

<pre class="center-column-code">
[
  {
    id: '1',
    symbol: 'ZRX/WETH',
    baseToken: 'ZRX',
    quoteToken: 'WETH',
    minOrderSize: '0.001',
    maxOrderSize: '10000',
    priceMaxDecimals: 5,
    amountMaxDecimals: 6
  },
  ...
]
</pre>


## Get Ticker Snapshot

```
curl "http://api.paradex.io/v2/ticker?market=weth-zrx"
  -H "HTTP_API_KEY: <your-api-key>"
```


```json
{
	'version': '2.0'
	'type': 'request', 
	'target': 'ticker', 
	'method': 'GET', 
	'id': 1, 
    'params': [
      'market': 'weth-zrx',
    ]

}
```

<b>Access Level:</b> Basic Access

Gets a ticker snapshot of the specified market 

### HTTP Request 

`GET http://api.paradex.io/v2/ticker` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market

### Returns

<pre class="center-column-code">
{
  'bid': '0.004',
  'ask': '0.005',
  'last': '0.0045'
}
</pre>

## View Orderbook

```
curl "http://api.paradex.io/v2/orderbook?market=rep-weth"
  -H "HTTP_API_KEY: <your-api-key>"
```


```json
{
	'version': '2.0'
	'type': 'request', 
	'target': 'orderbook', 
	'method': 'GET', 
	'id': 1, 
    'params': [
      'market': 'rep-weth',
    ]

}
```

<b>Access Level:</b> Basic Access

Gets a snapshot of the order book of the given market

### HTTP Request 

`GET http://api.paradex.io/v2/orderbook` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market

### Returns

<pre class="center-column-code">
{
    marketId: 1,
    marketSymbol: 'REP-WETH',
    bids:[
        { amount: '300', price: '0.004' },
        { amount: '440', price: '0.003' },
        { amount: '500', price: '0.002' },
        ...
    ],
    asks:[
        { amount: '200', price: '0.005' },
        { amount: '360', price: '0.006' },
        { amount: '445', price: '0.007' },
        ...
    ]
}
</pre>

## List Open Orders

```
curl "http://api.paradex.io/v2/orderbook?market=rep-weth"
  -H "HTTP_API_KEY: <your-api-key>"
```


```json
{
	'version': '2.0'
	'type': 'request', 
	'target': 'orderbook', 
	'method': 'GET', 
	'id': 1, 
    'params': [
      'market': 'rep-weth',
    ]

}
```

<b>Access Level:</b> Account Access

Gets a snapshot of the order book of the given market

### HTTP Request 

`GET http://api.paradex.io/v2/orderbook` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market

### Returns

<pre class="center-column-code">
{
    marketId: 1,
    marketSymbol: 'REP-WETH',
    bids:[
        { amount: '300', price: '0.004' },
        { amount: '440', price: '0.003' },
        { amount: '500', price: '0.002' },
        ...
    ],
    asks:[
        { amount: '200', price: '0.005' },
        { amount: '360', price: '0.006' },
        { amount: '445', price: '0.007' },
        ...
    ]
}
</pre>
